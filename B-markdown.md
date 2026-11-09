# B — Markdown e sintaxe

**Objetivo:** escrever documentação e materiais em Markdown.

**Ao final deste capítulo você terá:** escrito um documento completo em Markdown e visto como ele aparece formatado no GitHub.

---

## B.1 O que é Markdown

O **Markdown** é uma forma de formatar texto usando caracteres comuns do teclado. Em vez de clicar em botões de negrito ou título, você escreve símbolos como `**` e `#`, e um programa transforma o texto em uma página formatada (esse processo se chama *renderizar*).

Arquivos Markdown terminam em `.md`. Usamos Markdown:

- no `README.md`, a página de apresentação de todo repositório no GitHub;
- na descrição de Pull Requests e Issues no GitHub (Pull Request é o pedido para incorporar alterações em um projeto; Issue é um registro de tarefa ou problema);
- nas células de texto dos Jupyter Notebooks, usados na trilha de Análise de Dados.

> Existem pequenas variações de Markdown. Este material segue o **GitHub Flavored Markdown (GFM)**, a versão usada pelo GitHub. Tabelas, checklists, texto tachado e alertas são recursos do GFM.

---

## B.2 Onde praticar

Você precisa de um lugar para escrever um arquivo `.md` e ver o resultado. A forma mais simples não exige instalar nada:

1. Tenha uma conta no GitHub ([github.com/signup](https://github.com/signup)).
2. Tenha um repositório. Se ainda não tiver: clique no **+** no canto superior direito → **New repository** → nome `modulo-0-fundamentos` → marque **Add a README file** → **Create repository**.
3. Na página do repositório, clique em **Add file → Create new file**.
4. Dê um nome terminado em `.md`, por exemplo `teste.md`.
5. Escreva na aba **Edit** e clique na aba **Preview** para ver o resultado formatado.

Use esse editor para testar cada exemplo deste capítulo. Para salvar, clique em **Commit changes...** (o *commit* registra o arquivo no histórico do repositório).

> Se você já usa o VS Code, também pode criar o arquivo nele e abrir a pré-visualização com `Ctrl+Shift+V` (`Cmd+Shift+V` no macOS).

---

## B.3 Formatação básica

| Estilo | Você escreve | Resultado |
| :--- | :--- | :--- |
| Itálico | `*texto*` ou `_texto_` | *texto* |
| Negrito | `**texto**` ou `__texto__` | **texto** |
| Negrito e itálico | `***texto***` | ***texto*** |
| Tachado | `~~texto~~` | ~~texto~~ |

**Parágrafos:** deixe uma linha em branco entre eles. Apenas pular uma linha, sem a linha em branco, junta as duas frases no mesmo parágrafo.

---

## B.4 Títulos

Use `#` seguido **obrigatoriamente** de um espaço. Quanto mais `#`, menor o título, do nível 1 ao 6:

```markdown
# Título principal (nível 1)
## Seção (nível 2)
### Subseção (nível 3)
#### Detalhe (nível 4)
```

Use apenas um título de nível 1 por documento e não pule níveis (de `##` direto para `####`). O GitHub usa os títulos para montar um sumário automático do arquivo.

---

## B.5 Listas e checklists

```markdown
- Item de lista
- Outro item
  - Subitem (dois espaços antes do traço)

1. Primeiro passo
2. Segundo passo

- [ ] Tarefa pendente
- [x] Tarefa concluída
```

- **Lista simples:** `-` ou `*` seguido de espaço.
- **Lista numerada:** número, ponto e espaço.
- **Checklist:** `- [ ]` para pendente e `- [x]` para concluído. No GitHub, os itens viram caixas de seleção.

---

## B.6 Links, imagens e citações

```markdown
[Acesse o LabRI](https://labriunesp.org/)

![Logo do Python](https://www.python.org/static/community_logos/python-logo.png)

> "O código limpo é aquele que parece ter sido escrito por alguém que se importa."
```

- **Link:** o texto visível entre `[ ]` e o endereço entre `( )`.
- **Imagem:** igual ao link, com `!` na frente. O texto entre colchetes é o *texto alternativo*, lido por leitores de tela e exibido se a imagem não carregar.
- **Citação:** `>` seguido de espaço no início da linha.

Para usar uma imagem que está no próprio repositório, use o caminho do arquivo: `![Diagrama](imagens/diagrama.png)`.

---

## B.7 Alertas do GitHub

O GitHub tem caixas de destaque coloridas para avisos. Elas são escritas como uma citação com um marcador especial na primeira linha:

```markdown
> [!NOTE]
> Informação útil.

> [!TIP]
> Uma dica opcional.

> [!IMPORTANT]
> Algo essencial para o leitor.

> [!WARNING]
> Atenção a um risco.

> [!CAUTION]
> Consequência negativa de uma ação.
```

> [!NOTE]
> Os alertas só aparecem formatados no GitHub. Em outros visualizadores, viram citações comuns.

---

## B.8 Código

- **Na própria linha:** envolva com uma crase. Escrever `` `git status` `` mostra `git status`.
- **Bloco de várias linhas:** três crases antes e três depois. Escreva o nome da linguagem logo após as primeiras crases para colorir o código:

````markdown
```python
def saudar():
    print("Olá, Markdown!")
```
````

Linguagens comuns: `python`, `bash` (comandos de terminal), `json`, `html`, `markdown`.

---

## B.9 Tabelas

Barras verticais `|` separam as colunas, e a segunda linha separa o cabeçalho. Os `:` nessa linha definem o alinhamento:

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

As colunas não precisam estar alinhadas no texto; basta ter o mesmo número de `|` em cada linha.

---

## B.10 HTML dentro do Markdown

O Markdown é convertido em HTML (a linguagem das páginas web) quando renderizado, e algumas tags HTML podem ser usadas diretamente:

- **Quebra de linha dentro de um parágrafo:** `<br>`
- **Centralizar:** a antiga tag `<center>` é obsoleta e **o GitHub não a aceita**. Use o atributo `align`:

```html
<p align="center">Texto centralizado</p>
<div align="center"><img src="logo.png" width="200"></div>
```

- **Caixa retrátil**, útil para esconder respostas de exercícios ou códigos longos. Deixe uma linha em branco depois de `</summary>` para o Markdown de dentro funcionar:

```html
<details>
<summary>Clique para ver a resposta</summary>

Este texto só aparece quando o leitor abre a caixa.

</details>
```

---

## Exercício do Capítulo B

No seu repositório, crie o arquivo `aula_markdown.md` (pelo GitHub, em **Add file → Create new file**, ou pelo seu editor) contendo:

1. um título de nível 1 centralizado com `<p align="center">` ou `<div align="center">`;
2. um parágrafo com termos em negrito e em itálico;
3. uma tabela de 3 colunas listando 3 ferramentas de dados, suas funções e o status de instalação;
4. um bloco de código Python com destaque de sintaxe;
5. um alerta `> [!TIP]`;
6. uma caixa retrátil (`<details>` / `<summary>`) com um aviso dentro.

Confira o resultado na aba **Preview** e salve com **Commit changes...**.

> [!TIP]
> Se você já fez o capítulo A, pratique o fluxo completo: escolha **Create a new branch for this commit and start a pull request** na hora de salvar, abra o Pull Request e veja o arquivo renderizado na aba **Files changed** antes de fazer o merge.

## Checklist do Capítulo B

- [ ] Sei o que é Markdown e onde ele é usado
- [ ] Aplico negrito, itálico, tachado e combinações
- [ ] Estruturo títulos na hierarquia correta
- [ ] Crio listas simples, numeradas e checklists
- [ ] Insiro links, imagens, citações e alertas
- [ ] Formato código na linha e em blocos com destaque de linguagem
- [ ] Crio tabelas e uso HTML básico (`<br>`, `align`, `<details>`)
- [ ] Criei e salvei o arquivo do exercício no meu repositório

## Links de apoio

- [Sintaxe básica de escrita e formatação no GitHub](https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Especificação do GitHub Flavored Markdown](https://github.github.com/gfm/)
