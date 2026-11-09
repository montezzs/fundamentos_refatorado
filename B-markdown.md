# B — Markdown e sintaxe

O **Markdown** é uma linguagem de marcação leve que formata textos usando caracteres comuns do teclado. Usamos Markdown no `README.md`, na descrição de Pull Requests e Issues e nas células de texto dos Jupyter Notebooks.

> Existem variações do Markdown. Este material segue o **GitHub Flavored Markdown (GFM)**, que é o que o GitHub renderiza. Tabelas, checklists e texto tachado são extensões do GFM.

## B.1 Formatação básica

| Estilo | Sintaxe | Resultado |
| :--- | :--- | :--- |
| Itálico | `*texto*` ou `_texto_` | *texto* |
| Negrito | `**texto**` ou `__texto__` | **texto** |
| Negrito e itálico | `***texto***` | ***texto*** |
| Tachado | `~~texto~~` | ~~texto~~ |

## B.2 Títulos (hierarquia)

Use `#` seguido **obrigatoriamente** de um espaço. Vai do nível 1 (maior) ao 6 (menor). Use apenas um H1 por documento.

```markdown
# Título principal (H1)
## Seção (H2)
### Subseção (H3)
#### Detalhe (H4)
```

## B.3 Listas e checklists

```markdown
- Item não ordenado
- Outro item
  - Subitem (recuo de 2 espaços)

1. Primeiro passo
2. Segundo passo

- [ ] Tarefa pendente
- [x] Tarefa concluída
```

## B.4 Links, imagens e citações

```markdown
[Acesse o LabRI](https://labriunesp.org/)

![Logo do Python](https://www.python.org/static/community_logos/python-logo.png)

> "O código limpo é aquele que parece ter sido escrito por alguém que se importa."
```

- **Link**: texto entre `[ ]`, endereço entre `( )`.
- **Imagem**: igual ao link, com `!` na frente. O texto entre colchetes é o texto alternativo (acessibilidade).
- **Citação**: `>` seguido de espaço no início da linha.

## B.5 Código

- **Inline**: envolva com uma crase — `` `git status` ``.
- **Bloco**: três crases antes e depois, com o nome da linguagem para ativar o destaque:

````markdown
```python
def saudar():
    print("Olá, Markdown!")
```
````

## B.6 Tabelas

Barras `|` separam colunas; a segunda linha separa o cabeçalho. Os `:` definem o alinhamento:

```markdown
| Esquerda | Centro | Direita |
| :--- | :---: | ---: |
| Dado A | Dado B | Dado C |
| Info 1 | Info 2 | Info 3 |
```

Resultado:

| Esquerda | Centro | Direita |
| :--- | :---: | ---: |
| Dado A | Dado B | Dado C |
| Info 1 | Info 2 | Info 3 |

## B.7 HTML dentro do Markdown

Algumas tags HTML funcionam diretamente:

- **Quebra de linha**: `<br>`
- **Centralizar**: a tag `<center>` é obsoleta e **o GitHub não a renderiza**. Use o atributo `align`:

```html
<p align="center">Texto centralizado</p>
<div align="center"><img src="logo.png" width="200"></div>
```

- **Caixa retrátil** (útil para respostas de exercícios ou código longo). Deixe uma linha em branco após `</summary>` para o Markdown interno funcionar:

```html
<details>
<summary>Clique para expandir a resposta</summary>

Este texto só aparece quando o leitor expande a caixa.

</details>
```

## Exercício da Parte B

1. Crie a branch (a partir da `main` atualizada):
   ```bash
   git switch main && git pull origin main
   git switch -c exercicio/sintaxe-markdown
   ```
2. Crie o arquivo `fundamentos/seu-nome/aula_markdown.md` (troque `seu-nome` pelo seu nome, sem acentos nem espaços) contendo:
   - um título principal (H1) centralizado com `<p align="center">` ou `<div align="center">`;
   - um parágrafo com termos em negrito e itálico;
   - uma tabela de 3 colunas listando 3 ferramentas de dados, suas funções e o status de instalação;
   - um bloco de código Python com destaque de sintaxe;
   - uma caixa retrátil (`<details>`/`<summary>`) com um aviso dentro.
3. Envie:
   ```bash
   git add fundamentos/seu-nome/aula_markdown.md
   git commit -m "doc: adiciona exercicio sobre sintaxe markdown"
   git push -u origin exercicio/sintaxe-markdown
   ```
4. Abra o Pull Request e confira na aba **Files changed** se o arquivo renderizou como esperado.

## Checklist da Parte B

- [ ] Entende onde o Markdown é usado (README, PRs, Issues, notebooks)
- [ ] Aplica negrito, itálico, tachado e combinações
- [ ] Estrutura títulos na hierarquia correta
- [ ] Cria listas simples, ordenadas e checklists
- [ ] Insere links, imagens e blocos de código com destaque
- [ ] Cria tabelas e usa HTML básico (`<br>`, `align`, `<details>`)
- [ ] Enviou o exercício por Pull Request
