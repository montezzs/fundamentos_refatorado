# C — Codespace / VS Code

**Objetivo:** configurar o editor de código, usar o terminal integrado e instalar as extensões essenciais.

**Ao final deste capítulo você terá:** um VS Code pronto para os projetos (no navegador, pelo Codespaces, ou no seu computador), com as extensões instaladas e sabendo usar o terminal e o painel do Git.

---

## C.1 Conceitos antes de começar

| Termo | O que é |
| :--- | :--- |
| **Editor de código** | Programa para escrever código, com cores por tipo de palavra, sugestões automáticas e atalhos. Diferente de um editor de texto comum, ele entende a linguagem que você está escrevendo. |
| **VS Code** | O editor de código gratuito da Microsoft que usamos. É nele que escrevemos Python, Markdown e notebooks. |
| **Extensão** | Um complemento instalado no VS Code que adiciona recursos, como suporte a uma linguagem. O VS Code sozinho é simples; as extensões o adaptam ao trabalho com dados. |
| **Terminal** | Janela onde você digita comandos de texto. O VS Code tem um terminal embutido, então não é preciso abrir outro programa. |
| **Repositório** | A pasta de um projeto controlada pelo Git (o programa que registra o histórico de alterações), hospedada no GitHub. |
| **GitHub Codespaces** | Um computador na nuvem, oferecido pelo GitHub, que abre um VS Code no navegador já com o seu repositório. Nada precisa ser instalado na sua máquina. |

---

## C.2 Preparação: conta e repositório

Os dois jeitos de usar o VS Code neste curso partem de um repositório no GitHub. Se ainda não tiver:

1. Crie uma conta em [github.com/signup](https://github.com/signup).
2. Clique no **+** no canto superior direito → **New repository**.
3. Nome: `modulo-0-fundamentos`. Marque **Add a README file** e, em **Add .gitignore**, escolha **Python**.
4. Clique em **Create repository**.

---

## C.3 Escolher: Codespaces ou VS Code local

| | GitHub Codespaces | VS Code local |
| :--- | :--- | :--- |
| Onde roda | Em um computador na nuvem, pelo navegador | No seu computador |
| Instalação | Nenhuma | VS Code, Git e Python |
| Git e login no GitHub | Já vêm prontos | Você configura |
| Custo | Cota mensal gratuita; acima dela é cobrado | Gratuito |
| Quando usar | Para começar rápido, em máquina fraca ou sem permissão de instalar programas | Para uso diário em um computador próprio |

> [!WARNING]
> **Cota do Codespaces:** as horas gratuitas são contadas enquanto o codespace está ligado. Ao terminar, pare-o em [github.com/codespaces](https://github.com/codespaces) (menu **⋯ → Stop codespace**) e apague os que não usar mais. Ele também para sozinho após um tempo sem uso. Os limites atuais estão na [documentação de cobrança do GitHub](https://docs.github.com/pt/billing/managing-billing-for-your-products/managing-billing-for-github-codespaces/about-billing-for-github-codespaces). Estudantes podem pedir mais horas pelo [GitHub Education](https://education.github.com/pack).

### Opção 1 — Abrir no Codespaces

1. Na página do repositório, clique no botão verde **Code**.
2. Aba **Codespaces → Create codespace on main**.
3. Aguarde: o VS Code abre no navegador, com os arquivos do repositório à esquerda.

### Opção 2 — Instalar e abrir no computador

1. Baixe e instale o VS Code em [code.visualstudio.com](https://code.visualstudio.com/).
2. Instale o Git em [git-scm.com/downloads](https://git-scm.com/downloads), com as opções padrão.
3. Baixe o repositório pelo próprio VS Code: abra a Paleta de Comandos (`Ctrl+Shift+P`, ou `Cmd+Shift+P` no macOS), digite **Git: Clone**, escolha **Clone from GitHub**, autorize o login no navegador quando pedido e selecione `modulo-0-fundamentos`. Escolha uma pasta no computador para guardá-lo.
4. Quando o VS Code perguntar, clique em **Open** para abrir o repositório clonado.

> A **Paleta de Comandos** é a caixa de busca de todas as ações do VS Code. Sempre que não souber onde fica algo, abra-a e digite o que procura.

**A regra de ouro no computador: abra a pasta, não o arquivo.** Se você abrir o projeto depois, use **File → Open Folder** e selecione a pasta do repositório. Abrir arquivos soltos (**File → Open File**) impede o VS Code de entender o projeto: ele não encontra o ambiente Python, o Git e os caminhos entre arquivos.

---

## C.4 A interface

A barra de ícones à esquerda abre os painéis principais:

| Painel | Atalho | Função |
| :--- | :--- | :--- |
| Explorer | `Ctrl+Shift+E` | Árvore de pastas e arquivos do projeto. Clique com o botão direito para criar arquivos e pastas. |
| Search | `Ctrl+Shift+F` | Busca uma palavra em todos os arquivos do projeto. |
| Source Control | `Ctrl+Shift+G` | Mostra o que mudou e permite registrar e enviar alterações pelo Git sem digitar comandos. |
| Extensions | `Ctrl+Shift+X` | Busca e instala extensões. |

No macOS, troque `Ctrl` por `Cmd`. No Codespaces pelo navegador, alguns atalhos podem ser capturados pelo navegador; nesse caso, use o menu **☰** no canto superior esquerdo.

---

## C.5 Extensões essenciais

| Extensão | Para quê |
| :--- | :--- |
| **Python** (Microsoft) | Cores, sugestões automáticas, escolha do Python usado no projeto e execução de scripts. |
| **Jupyter** (Microsoft) | Abrir e executar notebooks `.ipynb` (documentos que misturam código, resultados e texto) dentro do editor. |
| **Markdown All in One** | Atalhos e pré-visualização para arquivos `.md`, o formato de documentação. |
| **Rainbow CSV** | Colore cada coluna de arquivos `.csv`/`.tsv` (tabelas em texto), facilitando conferir dados. |

Para instalar: abra o painel **Extensions** (`Ctrl+Shift+X`), busque pelo nome, confira o autor e clique em **Install**. O processo é igual no Codespaces e no computador.

---

## C.6 Terminal integrado

Abra com ``Ctrl+` `` (a tecla da crase) ou pelo menu **Terminal → New Terminal**. Ele aparece na parte de baixo da tela, já dentro da pasta do projeto.

Teste alguns comandos:

```bash
pwd       # mostra em qual pasta você está (no PowerShell: Get-Location)
ls        # lista os arquivos da pasta
git status
```

- No **Codespaces**, o terminal é Linux (programa *bash*).
- No **Windows**, o padrão é o PowerShell. A maioria dos comandos deste curso funciona igual; quando houver diferença, o material indica.

---

## C.7 Registrar e enviar alterações pelo painel do Git

O painel **Source Control** faz, com cliques, o mesmo ciclo de comandos do Git:

1. Altere ou crie um arquivo e salve (`Ctrl+S`). Ele aparece no painel com a letra **M** (modificado) ou **U** (novo).
2. Passe o mouse sobre o arquivo e clique em **+** para escolhê-lo para o próximo registro (*stage*).
3. Escreva uma mensagem curta no campo de texto, descrevendo a alteração.
4. Clique em **Commit** para criar o registro no histórico (*commit*).
5. Clique em **Sync Changes** (ou **Publish Branch**, se a branch for nova) para enviar ao GitHub. No computador, na primeira vez, o VS Code pede para entrar na conta do GitHub pelo navegador.

Para criar uma **branch** (uma linha de trabalho separada da principal, `main`), clique no nome da branch no canto inferior esquerdo da tela → **Create new branch...**.

---

## C.8 Pré-visualizar Markdown

Com um arquivo `.md` aberto:

- `Ctrl+K` e depois `V` abre a pré-visualização **ao lado** do texto;
- `Ctrl+Shift+V` abre a pré-visualização em uma nova aba.

A pré-visualização acompanha o que você digita.

---

## C.9 Codespace pré-configurado (devcontainer) — opcional

Toda vez que você cria um codespace, ele começa "limpo": é preciso instalar as extensões de novo. Um arquivo de configuração chamado **devcontainer** resolve isso: ele descreve o ambiente, e o Codespaces o monta automaticamente.

1. No repositório, crie a pasta `.devcontainer` e, dentro dela, o arquivo `devcontainer.json`:

```json
{
  "name": "Modulo 0 - Python + uv",
  "image": "mcr.microsoft.com/devcontainers/python:3.12",
  "postCreateCommand": "curl -LsSf https://astral.sh/uv/install.sh | sh && export PATH=\"$HOME/.local/bin:$PATH\" && if [ -f pyproject.toml ]; then uv sync && uv run playwright install --with-deps chromium; fi",
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "ms-toolsai.jupyter",
        "yzhang.markdown-all-in-one",
        "mechatroner.rainbow-csv"
      ],
      "settings": {
        "python.defaultInterpreterPath": "${containerWorkspaceFolder}/.venv/bin/python"
      }
    }
  }
}
```

O que cada parte faz:

- `image`: o sistema de base do codespace, já com Python 3.12.
- `postCreateCommand`: comandos rodados uma vez, ao criar o codespace. Instalam o **uv** (o gerenciador de pacotes Python usado no capítulo D) e, se o projeto já tiver dependências declaradas em um `pyproject.toml`, instalam essas dependências e o navegador usado pela biblioteca Playwright.
- `extensions`: as quatro extensões da seção C.5, instaladas automaticamente.
- `python.defaultInterpreterPath`: faz o VS Code usar o Python do ambiente do projeto.

2. Registre e envie o arquivo (seção C.7).
3. Crie um **novo** codespace, ou, no atual, abra a Paleta de Comandos e rode **Codespaces: Rebuild Container**. A primeira montagem leva alguns minutos.

No VS Code local, esse arquivo é ignorado, a menos que você use a extensão Dev Containers com Docker, o que não é necessário neste curso.

---

## Exercício do Capítulo C

1. Abra o seu repositório no Codespaces ou no VS Code local (C.3).
2. Instale as quatro extensões (C.5).
3. Crie uma branch chamada `exercicio/vscode` (C.7).
4. Pelo Explorer, crie o arquivo `participante.md` com seu nome, sua trilha e uma frase sobre você.
5. Abra a pré-visualização ao lado (C.8), tire um print do editor mostrando o texto e a pré-visualização, e envie no grupo de trabalho.
6. No terminal (C.6), rode `git status` e veja o arquivo listado.
7. Registre e envie a alteração pelo painel Source Control (C.7).
8. No GitHub, abra o Pull Request da branch `exercicio/vscode` para a `main` (aparece um botão **Compare & pull request** na página do repositório) e faça o merge.

## Checklist do Capítulo C

- [ ] Sei a diferença entre VS Code local e Codespaces, incluindo a cota
- [ ] Abri o projeto corretamente (Codespaces ou **Open Folder**)
- [ ] Navego pelos painéis da barra lateral e uso a Paleta de Comandos
- [ ] Instalei as extensões de Python, Jupyter, Markdown e CSV
- [ ] Abro e uso o terminal integrado
- [ ] Fiz commit e enviei alterações pelo painel Source Control
- [ ] Usei a pré-visualização de Markdown

## Links de apoio

- [Documentação do VS Code](https://code.visualstudio.com/docs)
- [Documentação do GitHub Codespaces](https://docs.github.com/pt/codespaces)
- [Dev Containers — referência do `devcontainer.json`](https://containers.dev/implementors/json_reference/)
