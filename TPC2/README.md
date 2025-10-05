# TPC 2 — Conversor simples de Markdown para HTML

### Enunciado

O objetivo é desenvolver um pequeno conversor em Python que transforme um subconjunto da sintaxe Markdown (de acordo com a Basic Syntax da Cheat Sheet) em código HTML.  
O conversor deve identificar e traduzir os seguintes elementos:

- **Cabeçalhos:** linhas que começam com `#`, `##` ou `###`.  
  Exemplo: `# Exemplo` → `<h1>Exemplo</h1>`

- **Negrito:** texto entre `**`.  
  Exemplo: `Este é um **exemplo** ...` → `Este é um <b>exemplo</b> ...`

- **Itálico:** texto entre `*`.  
  Exemplo: `Este é um *exemplo* ...` → `Este é um <i>exemplo</i> ...`

- **Lista numerada:** linhas consecutivas iniciadas por `1.`, `2.` ... devem ser convertidas numa lista ordenada `<ol>` com elementos `<li>`.

- **Link:** `[texto](url)` → `<a href="url">texto</a>`

- **Imagem:** `![alt](url)` → `<img src="url" alt="alt"/>`

### Resolução

- [Resolução](tpc2.ipynb)


