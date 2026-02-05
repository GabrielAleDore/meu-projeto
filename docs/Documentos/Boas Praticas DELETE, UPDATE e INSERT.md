# Boas praticas

## **Introdução**

As operações **DELETE**, **UPDATE** e **INSERT** são essenciais para a manipulação de dados no Banco de dados **IBM DB2**, mas também representam riscos significativos se não forem executadas com cuidado.  
Esta documentação aborda boas práticas para garantir a **integridade**, **segurança** e **disponibilidade** dos dados durante essas operações.

## **Riscos Associados a DELETE, UPDATE e INSERT**

| Operação   | Principais Riscos                                                 |
| ---------- | ----------------------------------------------------------------- |
| **DELETE** | Perda irreversível de dados, violação de integridade referencial. |
| **UPDATE** | Sobrescrita acidental de registros, inconsistência de dados.      |
| **INSERT** | Inserção de dados inválidos, duplicação indevida.                 |

## **Boas Práticas para Operações Seguras**

Antes de executar qualquer operação, é fundamental realizar uma análise detalhada:

**Verificar o impacto**: Usar `SELECT` e a criação de um `BACKUP` antes de `DELETE` ou `UPDATE` para confirmar quais registros serão

### Boas práticas DELETE
!!! note "Delete"
    1. **Validar dados que vão ser deletados**
    ```
    SELECT * FROM CONTAS_RECEBER_BAIXAS WHERE IDPLANILHA 1234567
    ```

    2. **Criar uma table temporaria para backup**
    ```
    CREATE TABLE TMP.CONTAS_RECEBER_BAIXAS_BKP250101 LIKE CONTAS_RECEBER_BAIXAS;
    INSERT INTO TMP.CONTAS_RECEBER_BAIXAS_BKP250101
    SELECT * FROM CONTAS_RECEBER_BAIXAS WHERE IDPLANILHA 1234567
    ```
    3. **Delete da informação**
    ```
    DELETE FROM CONTAS_RECEBER_BAIXAS WHERE IDPLANILHA 1234567
    ```

    !!! warning "é de extrema importância a criação de um backup para evitarmos Perda irreversível de dados e quebra de integridade."

### Boas práticas UPDATE
!!! note "Update"
    1. **validar o dados que serão atualizados**
    ```
    SELECT * 
    FROM PRODUTO_GRADE 
    WHERE TIPOBAIXAMESTRE = 'M' 
    AND IDSUBPRODUTO = 7800
    ```

    2. **Criação de backup para salver os dados de antes da atualização**
    ```
    CREATE TABLE TMP.PRODUTO_GRADE_BKP250101 LIKE PRODUTO_GRADE;
    INSERT INTO TMP.PRODUTO_GRADE_BKP250101
    SELECT * FROM PRODUTO_GRADE WHERE TIPOBAIXAMESTRE = 'M' AND IDSUBPRODUTO = 7800
    ```

    3. **Atualizando informação**
    ```
    UPDATE PRODUTO_GRADE
    SET TIPOBAIXAMESTRE = 'I'
    WHERE IDSUBPRODUTO = 7800
    ```
    !!! warning "É de extrema importância a criação de um backup para evitarmos a sobrescrita acidental de registros, inconsistência de dados."

### Boas práticas INSERT
!!! note "Insert"
    
    1. **insert comum**
    ```
    CREATE TABLE TMP.REGISTROS_LOG290525 LIKE REGISTROS
    INSERT INTO TMP.REGISTROS_LOG290525 (id, data, valor) VALUES (1, CURRENT_DATE, 100.50)

    INSERT INTO REGISTROS (id, data, valor) VALUES 
    SELECT * FROM TMP.REGISTROS_LOG290525 WHERE IDLINHA = 1
    ```

    2. **Insert com multiplos registros **
    ```
    CREATE TABLE TMP.REGISTROS_LOG290525 LIKE REGISTROS
    INSERT INTO TMP.REGISTROS_LOG290525 (id, data, valor) VALUES 
    (1, CURRENT DATE, 100.50),
    (2, CURRENT DATE, 200.75),
    (3, CURRENT DATE, 300.25);

    INSERT INTO REGISTROS (id, data, valor) VALUES 
    SELECT * FROM TMP.REGISTROS_LOG290525 WHERE IDLINHAS IN (1, 2, 3)
    ```

    !!! warning "Revisar dados antes de uma inserção, o uso de uma tabela de log é importante para termos a certeza que os dados que vão ser inseridos estão corretos e para evitar o insert de dados invalidos ou duplicados."

!!! warning
    **Importante reforçar que os exemplos apresentados acima são meramente ilustrativos.**  
    Em ambientes de produção, as operações são consideravelmente mais complexas e técnicas, e a realização de um backup completo de uma tabela geralmente não é viável, seja por questões de desempenho, volume de dados ou políticas de governança. Por isso, é fundamental sempre realizar backups pontuais e direcionados apenas aos dados que efetivamente serão manipulados. 
    Além disso, é **imprescindível** adotar uma postura de extrema cautela ao executar qualquer alteração em ambientes de produção, especialmente considerando que se trata de sistemas críticos e de responsabilidade direta com o cliente.  

    

