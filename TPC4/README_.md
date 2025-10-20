## 🧃 TPC 4 — Simulação de Máquina de Vending (com PLY)

### 📖 Descrição do Problema

O objetivo deste trabalho é desenvolver, em **Python**, uma aplicação que reproduza o comportamento de uma **máquina de vending**, fazendo uso da biblioteca **`ply.lex`** para criar um **analisador léxico** que interprete os comandos fornecidos pelo utilizador.

A máquina deve permitir listar os produtos disponíveis, inserir moedas, escolher um produto e terminar a sessão (devolvendo o troco).  
Toda a informação sobre o stock é lida e atualizada num ficheiro **`stock.json`**.

---

### ⚙️ Estrutura e Armazenamento de Dados

O stock inicial é guardado no ficheiro `stock.json`, cujo formato segue o exemplo abaixo:

```json
[
    {"cod": "A01", "nome": "Água 0.5L", "quant": 10, "preco": 0.7},
    {"cod": "A02", "nome": "Coca-Cola 0.33L", "quant": 6, "preco": 1.2},
    {"cod": "B01", "nome": "Bolacha Maria", "quant": 8, "preco": 0.5}
]
```

Quando a aplicação inicia, o conteúdo é carregado para memória.  
Ao terminar, o stock é atualizado e novamente escrito no mesmo ficheiro, preservando o estado.

---

### 🔤 Tokens Reconhecidos pelo Lexer

O analisador léxico, desenvolvido com `ply.lex`, identifica os seguintes **tokens**:

| Token | Expressão Regular | Exemplo |
|--------|------------------|----------|
| `LISTAR` | `r'LISTAR'` | `LISTAR` |
| `MOEDA` | `r'MOEDA'` | `MOEDA 1e 20c` |
| `SELECIONAR` | `r'SELECIONAR'` | `SELECIONAR A01` |
| `SAIR` | `r'SAIR'` | `SAIR` |
| `ADICIONAR` | `r'ADICIONAR'` | `ADICIONAR A05 Água 5 0.7` |
| `CODIGO` | `r'[A-D]\d{2}'` | `A01`, `B10`, `C07` |
| `VALOR` | `r'((2e)|(1e)|(50c)|(20c)|(10c)|(5c)|(2c)|(1c))+'` | `1e`, `20c`, `2e` |

Espaços, tabulações e quebras de linha são ignorados (`t_ignore = " \t\n"`).

---

### 💡 Comandos Disponíveis

| Comando | Função | Exemplo |
|----------|--------|----------|
| **LISTAR** | Mostra os produtos e respetivas quantidades/preços. | `LISTAR` |
| **MOEDA** | Permite inserir uma ou mais moedas. | `MOEDA 1e 50c` |
| **SELECIONAR** | Escolhe um produto através do código. | `SELECIONAR B01` |
| **ADICIONAR** | Introduz ou altera um item no stock. | `ADICIONAR C10 Água 5 0.8` |
| **SAIR** | Encerra o programa e devolve o troco. | `SAIR` |

---

### 🧠 Lógica de Funcionamento

1. **Leitura inicial do stock:**  
   O ficheiro `stock.json` é carregado ao iniciar o programa; caso não exista, é criado de raiz.

2. **Interação com o utilizador:**  
   O utilizador introduz comandos no terminal, que são processados pelo lexer.

3. **Gestão de saldo:**  
   O valor inserido em moedas é acumulado e descontado no momento da compra.

4. **Cálculo e devolução do troco:**  
   Ao sair, o sistema devolve o troco usando as moedas disponíveis (2€, 1€, 50c, 20c, 10c, 5c, 2c, 1c).

5. **Atualização do stock:**  
   O estado final do stock é guardado novamente no ficheiro `stock.json`.

---

### 🧾 Exemplo de Execução

```
maq: 2025-10-14, Stock carregado.
maq: Olá! Aguardando o seu comando.

>> LISTAR
maq:
cod   | nome                | quant | preço
--------------------------------------------
A01   | Água 0.5L           | 10    | 0.7€
A02   | Coca-Cola 0.33L     | 6     | 1.2€
B01   | Bolacha Maria       | 8     | 0.5€

>> MOEDA 2e
maq: Saldo atual = 2e0c

>> SELECIONAR A02
maq: Produto "Coca-Cola 0.33L" dispensado.
maq: Saldo restante = 0e80c

>> SAIR
maq: Troco devolvido: 1x 50c, 1x 20c, 1x 10c.
maq: Até breve!
```

---

### 🧩 Código da Solução
O ficheiro principal da implementação encontra-se em:  
- [`maq_vending.py`](maq_vending.py)
