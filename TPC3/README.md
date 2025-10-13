## 📝 TPC 3 — Tokenizador SPARQL em Python
### 📌 Descrição do Problema

Criar um analisador léxico simples (tokenizer) em Python que identifique os tokens essenciais de queries SPARQL. O analisador deve detetar e categorizar os componentes fundamentais da linguagem, de modo a permitir uma análise estrutural da consulta.

**O programa deve reconhecer os seguintes elementos:**

- **Keywords (Palavras-chave):** `SELECT, WHERE, PREFIX, OPTIONAL, FILTER`<br>
Ex: `SELECT ?a ?b ?c` → `[('SELECT', 'SELECT', 0, (0, 6)), ('VAR', '?a', 0, (7, 9)), ...]`

- **Variáveis (Variables):** iniciadas por `?`<br>
Ex: `?a` → `('VAR', '?a', linha, (start, end))`

- **Identificadores (Identifiers):** iniciados por `:`<br>
Ex: `:Pessoa` → `('IDENT', ':Pessoa', linha, (start, end))`

- **URIs (Uniform Resource Identifiers):** delimitadas por `< >`<br>
Ex: `<http://exemplo.org>` → `('URI', '<http://exemplo.org>', linha, (start, end))`

- **Strings literais:** delimitados por aspas `" "`<br>
Ex: `"texto"` → `('STRING', '"texto"', linha, (start, end))`

- **Operadores (Operators):** `=, !=, <, >`<br>
Ex: `?a = ?b` → `('VAR', '?a', ...), ('OP', '=', ...), ('VAR', '?b', ...)`

- **Símbolos de pontuação:** `{, }, ., ;, ,`<br>
Ex: `{ ?a :temIdade ?b . }` → `('PUNCT', '{', ...), ('PUNCT', '.', ...), ('PUNCT', '}', ...)`

- **Quebras de linha:** `\n`<br>
Ex: cada nova linha incrementa o contador de linha.

- **Erro (Error):** qualquer caractere não reconhecido é classificado como `ERRO`.

### 🧩 Exemplo de Input
```
SELECT ?a ?b ?c WHERE {
  ?a a :Pessoa ;
  :temIdade ?b ;
  :eIrmaoDe ?c .
}
```

### 💡 Exemplo de Output
```
[
    ('SELECT', 'SELECT', 0, (0, 6)),
    ('VAR', '?a', 0, (7, 9)),
    ('VAR', '?b', 0, (10, 12)),
    ('VAR', '?c', 0, (13, 15)),
    ('WHERE', 'WHERE', 0, (16, 21)),
    ('NEWLINE', '\n', 1, (22, 23)),
    ('PUNCT', '{', 1, (23, 24)),
    ('NEWLINE', '\n', 2, (24, 25)),
    ('VAR', '?a', 2, (27, 29)),
    ('ERRO', 'a', 2, (30, 31)),
    ('IDENT', ':Pessoa', 2, (32, 39)),
    ('PUNCT', ';', 2, (40, 41)),
    ('NEWLINE', '\n', 3, (41, 42)),
    ('IDENT', ':temIdade', 3, (47, 56)),
    ('VAR', '?b', 3, (57, 59)),
    ('PUNCT', ';', 3, (60, 61)),
    ('NEWLINE', '\n', 4, (61, 62)),
    ('IDENT', ':eIrmaoDe', 4, (67, 76)),
    ('VAR', '?c', 4, (77, 79)),
    ('PUNCT', '.', 4, (80, 81)),
    ('NEWLINE', '\n', 5, (81, 82)),
    ('PUNCT', '}', 5, (82, 83)),
    ('NEWLINE', '\n', 6, (83, 84))
]
```

### ✏️ Solução

- [TPC 3 — Tokenizador SPARQL em Python](tpc3.ipynb)
