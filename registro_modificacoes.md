# Registro de Modificações - 30 de Abril de 2026

Este documento contém o passo a passo de todas as implementações e refatorações realizadas no projeto da Oficina Senac durante as sessões de hoje.

## 1. Implementação do Scroll Reveal (Animações ao rolar a página)
**Objetivo:** Melhorar a experiência do usuário criando transições visuais suaves para que o conteúdo não apareça de forma bruta na tela, mas sim "deslizando e revelando" de baixo para cima conforme a rolagem do usuário.

*   **CSS (`assets/css/style.css`):**
    *   Foram criadas duas novas classes: `.revelar-ao-rolar` (que define a opacidade em 0 e empurra o item sutilmente para baixo) e a classe `.ativo` (que define a opacidade em 1 e traz o elemento para sua posição original em Y = 0).
    *   Adicionada propriedade `transition` configurada para controlar o movimento (`transform`) e aparecimento (`opacity`) das divs.
*   **JavaScript (`assets/js/script.js`):**
    *   Implementação nativa usando a Web API **IntersectionObserver**. Este script escuta sempre que um elemento entra na visão do usuário (Viewport) e automaticamente adiciona a classe `.ativo` ao referido elemento.
*   **HTML:**
    *   Aplicação das classes `.revelar-ao-rolar` nas seções principais da página `index.html` para habilitar o efeito.

## 2. Refatoração de Arquitetura: Navbar Dinâmica
**Objetivo:** Evitar redundância de código através da adoção do conceito Single Source of Truth ("Única Fonte da Verdade"). Com isso, em vez de ter o código de menus copiado em todas as páginas, tudo passaria a ser lido de um único arquivo.

*   **JavaScript (`assets/js/navbar.js`):**
    *   Criação do script global dedicado para inserir dinamicamente a barra de navegação.
    *   Todo o bloco de código HTML do menu principal e secundário foi incluído dentro deste arquivo.
    *   Foi implementado um detector de rotas inteligente que lê a URL/Página (ex: `/servicos.html` ou `/index.html#sobre`) e insere automaticamente a classe `--active` no link correspondente do menu, destacando a seção certa visualmente.

## 3. Padronização e Limpeza nas demais Páginas
**Objetivo:** Remover a duplicação dos antigos elementos de `<nav>` manuais dos arquivos HTML secundários, substituindo-os pelo componente global, padronizando os arquivos do projeto.

*   **`index.html`**:
    *   Limpeza total da `<nav>` original.
    *   Inserção do container-alvo `<div id="header-global"></div>`.
    *   Inserção do link para o `navbar.js` no final do header.
*   **`projetos.html` e `servicos.html`**:
    *   Adição da importação do `assets/css/style.css` ausente.
    *   Adição do import e referência `assets/js/navbar.js`.
    *   Deleção total de ambos os blocos `bem-navbar` e `bem-navbar--secundaria`.
    *   Inclusão da `<div id="header-global"></div>` em substituição aos menus de topo.
    *   Aplicação das classes CSS `.revelar-ao-rolar` nos containers locais para sincronizar o efeito de scroll revelador através de múltiplas páginas de forma fluida.

---

**Resumo Final:** 
O projeto passou de um emaranhado de arquivos com os menus e animações duplicados para uma base de código modularizada, onde a navegação só precisa ser atualizada em um único script JavaScript (`navbar.js`), que instantaneamente replica o resultado para todas as páginas com um menu interativo sincronizado, leve e bem-animado.
