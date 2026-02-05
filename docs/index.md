---
hide:
  - navigation
  - toc
---

<style>
  /* 1. CONFIGURAÇÃO DO FUNDO (BLINDADO) */
  body {
    /* A Imagem de Fundo */
    /* ATENÇÃO: Se sua imagem for PNG, mude o final para .png */
    background-image: url('imagens/fundo-ciss.png') !important;
    
    background-repeat: no-repeat !important;
    background-position: center center !important;
    background-attachment: fixed !important;
    background-size: cover !important;
  }

  /* 2. Deixa o conteúdo transparente para ver o fundo */
  .md-main, .md-content, .md-container {
    background: transparent !important;
  }

  /* 3. Cabeçalho Transparente */
  .md-header {
    background-color: transparent !important;
    border-bottom: none !important;
    box-shadow: none !important;
  }
  
  /* Força os textos do menu a serem brancos na Home */
  .md-header__title, .md-tabs__link, .md-header__button {
      color: white !important;
      text-shadow: 0 1px 3px rgba(0,0,0,0.5);
  }

  /* Centraliza verticalmente */
  .md-content__inner {
      margin-top: 8vh;
      text-align: center;
  }
</style>

<div class="md-grid md-typeset" style="max-width: 900px; margin: 0 auto; text-align: center;">

  <h1 style="color: white; font-size: 3.5rem; font-weight: 800; margin-bottom: 20px;">
    Documentação TI Ciss
  </h1>
  
  <p style="color: #f0f0f0; font-size: 1.4rem; font-weight: 500; margin-bottom: 50px;">
    Tudo o que você precisa saber sobre nossos processos, infraestrutura e sistemas em um só lugar.
  </p>

  <div style="display: flex; gap: 20px; justify-content: center; flex-wrap: wrap;">
    
    <a href="Documentos/documentos/" class="md-button" 
       style="background-color: #3f51b5; color: white; border: none; padding: 15px 30px; border-radius: 50px; font-weight: bold; font-size: 1.1rem;">
      Acessar Documentos
    </a>

    <a href="Processos/processos/" class="md-button" 
       style="background-color: rgba(255,255,255,0.1); color: white; border: 2px solid white; padding: 13px 30px; border-radius: 50px; font-weight: bold; font-size: 1.1rem; backdrop-filter: blur(5px);">
      Ver Processos
    </a>

  </div>
</div>