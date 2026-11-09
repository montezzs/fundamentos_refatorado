# D — Ambiente de trabalho (uv)

## D.1 Por que Python e por que uv?

O **Python** é a linguagem mais usada em ciência de dados: tem bibliotecas maduras para coletar dados, automatizar processos, analisar, visualizar e treinar modelos.

O **[uv](https://docs.astral.sh/uv/)** é um gerenciador de projetos e pacotes Python, escrito em Rust e muito mais rápido que o `pip`. Em uma só ferramenta ele:

- **instala versões do Python** (não é obrigatório baixar do python.org);
- **cria ambientes virtuais**: cada projeto tem suas próprias bibliotecas, sem conflito entre versões;
- **gerencia dependências**: instala, atualiza e remove bibliotecas e registra tudo em arquivos versionáveis;
- **reproduz o ambiente**: qualquer pessoa da equipe recria exatamente o mesmo ambiente com um comando.

Os dois arquivos centrais de um projeto uv são:

| Arquivo | O que é | Vai para o Git? |
| :--- | :--- | :--- |
| `pyproject.toml` | Metadados do projeto e dependências declaradas (ex.: `pandas>=2`) | ✅ Sim |
| `uv.lock` | Versões exatas resolvidas de todas as dependências | ✅ Sim |
| `.python-version` | Versão do Python do projeto | ✅ Sim |
| `.venv/` | O ambiente virtual em si | ❌ Não (recriável) |

## D.2 Instalando o uv

Verifique se já existe: `uv --version`. Se não existir:

**macOS / Linux / Codespaces:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Feche e reabra o terminal e confirme com `uv --version`. Outros métodos (pip, Homebrew, WinGet) estão na [página de instalação](https://docs.astral.sh/uv/getting-started/installation/).

## D.3 Python

Usaremos **Python 3.10 ou superior**. O uv encontra o Python já instalado na máquina e, se não houver uma versão compatível, baixa uma automaticamente. Para instalar uma versão específica explicitamente:

```bash
uv python install 3.12
uv python list          # mostra as versões disponíveis e instaladas
```

## D.4 Dois cenários: criar ou entrar em um projeto

**Cenário 1 — o repositório já tem `pyproject.toml` e `uv.lock`** (é o caso de todos os alunos neste curso):

```bash
uv sync
```

Esse comando cria a `.venv` e instala exatamente as versões do `uv.lock`. É assim que o ambiente se torna reproduzível.

**Cenário 2 — você está criando um projeto do zero** (feito **uma única vez pelos responsáveis** no repositório compartilhado, ou por você em projetos pessoais):

```bash
uv init --python 3.12
```

Isso cria `pyproject.toml`, `.python-version`, `README.md`, um `main.py` de exemplo e inicializa um repositório Git (se ainda não houver um).

> ⚠️ **No repositório da equipe, não rode `uv init` nem `uv add` por conta própria.** Cada execução altera `pyproject.toml` e `uv.lock`, e PRs de várias pessoas mexendo nesses arquivos entram em conflito. Se precisar de uma biblioteca nova, peça aos responsáveis ou abra uma Issue.

> ⚠️ **Importante:** `uv add` só funciona dentro de um projeto, isto é, onde existe um `pyproject.toml`. Rodar apenas `uv venv` e depois `uv add` em uma pasta sem `pyproject.toml` resulta em erro. O `uv venv` sozinho serve para o fluxo antigo, compatível com pip (`uv pip install ...`), que não usaremos.

## D.5 Instalando as dependências do treinamento

**Alunos:** as dependências já estão declaradas no repositório, e o `uv sync` do Cenário 1 já instalou todas. Siga direto para a instalação dos navegadores do Playwright, logo abaixo.

**Responsáveis (uma única vez), ou em um projeto pessoal**, dentro do projeto:

```bash
uv add scrapy playwright httpx pandas jupyter matplotlib seaborn wordcloud networkx python-dotenv
```

O `uv add` instala os pacotes na `.venv` (criando-a se necessário) e atualiza `pyproject.toml` e `uv.lock`. Para remover: `uv remove <pacote>`.

Ferramentas usadas só no desenvolvimento podem ir em um grupo separado, por exemplo: `uv add --dev ipykernel`.

Em seguida, instale os navegadores do Playwright (trilha de Coleta):

```bash
uv run playwright install
```

No Linux/Codespaces, se o Playwright reclamar de bibliotecas do sistema ausentes, use `uv run playwright install --with-deps` (pode pedir senha de administrador na máquina local).

## D.6 Executando código: `uv run`

A forma recomendada é usar `uv run`, que **dispensa ativar o ambiente** e garante que ele esteja sincronizado com o `uv.lock` antes de executar:

```bash
uv run python teste_conexao.py
uv run jupyter lab
```

### Alternativa: ativar a `.venv` manualmente

Se preferir chamar `python` diretamente, ative o ambiente:

| Sistema | Comando |
| :--- | :--- |
| macOS / Linux / Codespaces | `source .venv/bin/activate` |
| Windows (PowerShell) | `.venv\Scripts\Activate.ps1` |
| Windows (CMD) | `.venv\Scripts\activate.bat` |

Após ativar, `(.venv)` aparece no início da linha do terminal. Para sair: `deactivate`.

**Erro de permissão no PowerShell** ("a execução de scripts foi desabilitada neste sistema"): é uma política de segurança do Windows. A solução menos invasiva, que **não exige administrador** e vale só para o seu usuário:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Confirme com `S`. Se preferir não alterar a política, use `uv run`, que não depende de ativação.

## D.7 Configurando o VS Code para usar a `.venv`

1. Abra a Paleta de Comandos: `Ctrl+Shift+P` (`Cmd+Shift+P` no macOS).
2. Selecione **Python: Select Interpreter**.
3. Escolha o Python da `.venv`:
   - `./.venv/Scripts/python.exe` (Windows)
   - `./.venv/bin/python` (macOS / Linux / Codespaces)

   Geralmente aparece marcado como **Recommended**. Se não aparecer, use **Enter interpreter path...** e selecione o executável manualmente.

**Jupyter (trilha de Análise):** com a extensão Jupyter instalada, abra o notebook, clique em **Select Kernel** no canto superior direito e escolha o Python da `.venv`. O pacote `jupyter` instalado em D.5 já inclui o `ipykernel` necessário.

## D.8 Segurança: arquivo `.env` e `.gitignore`

Alguns projetos usam chaves de API, senhas ou tokens. Esses dados **nunca** devem ir para o GitHub.

1. Crie um arquivo chamado exatamente `.env` na raiz do projeto.
2. Coloque as credenciais nele:
   ```
   TWOCAPTCHA_API_KEY=sua_chave_aqui
   ```
3. Garanta que o `.gitignore` contém:
   ```
   .env
   .venv/
   ```
4. Leia as variáveis no código com `python-dotenv`:
   ```python
   import os
   from dotenv import load_dotenv

   load_dotenv()
   chave = os.getenv("TWOCAPTCHA_API_KEY")
   ```

> Se uma chave for commitada por engano, apagar o arquivo depois **não basta**: ela continua no histórico do Git. Revogue a chave no serviço e gere uma nova. No Codespaces, prefira cadastrar segredos em **Settings → Codespaces → Secrets** da sua conta.

## D.9 Script de teste

Crie `teste_conexao.py` na raiz do projeto:

```python
import httpx
import pandas as pd


def testar_ambiente():
    print("Iniciando testes do ambiente virtual...\n")

    # 1. Coleta (HTTPX)
    url = "https://practicesoftwaretesting.com/"
    try:
        response = httpx.get(url, timeout=10, follow_redirects=True)
        if response.status_code == 200:
            print("✅ Coleta: conexão HTTPX ativa.")
        else:
            print(f"⚠️ Coleta: conexão estabelecida, mas o status foi {response.status_code}")
    except httpx.HTTPError as e:
        print(f"❌ Coleta: falha ao conectar: {e}")

    # 2. Análise (Pandas)
    print(f"✅ Análise: Pandas importado com sucesso. Versão: {pd.__version__}")


if __name__ == "__main__":
    testar_ambiente()
```

Execute:

```bash
uv run python teste_conexao.py
```

> Um erro de importação acontece no topo do arquivo, antes de qualquer `try`; por isso o teste do Pandas não precisa de `try/except`: se o Pandas não estiver instalado, o script para com `ModuleNotFoundError` logo no início.

**Se der `ModuleNotFoundError`:**

1. Você está na pasta do projeto (onde está o `pyproject.toml`)?
2. Rodou `uv sync` ou `uv add` com os pacotes?
3. Executou com `uv run` (ou com a `.venv` ativada)?
4. No VS Code, o interpretador/kernel selecionado é o da `.venv`?
5. O arquivo foi salvo antes de executar?

## D.10 Resumo de comandos

| Comando | Função |
| :--- | :--- |
| `uv init` | Cria um novo projeto |
| `uv sync` | Recria o ambiente a partir do `uv.lock` |
| `uv add <pacote>` | Adiciona uma dependência |
| `uv remove <pacote>` | Remove uma dependência |
| `uv run <comando>` | Executa no ambiente do projeto |
| `uv lock --upgrade` | Atualiza as versões travadas |
| `uv python install <versão>` | Instala uma versão do Python |
| `uv tree` | Mostra a árvore de dependências |

## Exercício da Parte D

1. Crie a branch:
   ```bash
   git switch main && git pull origin main
   git switch -c exercicio/ambiente-uv
   ```
2. Sincronize o ambiente: `uv sync` (no Codespaces com devcontainer isso já foi feito; rodar de novo não causa problema).
3. Instale os navegadores do Playwright: `uv run playwright install` (já feito no Codespaces com devcontainer).
4. Crie `fundamentos/seu-nome/teste_conexao.py` com o script da seção D.9 e execute:
   ```bash
   uv run python fundamentos/seu-nome/teste_conexao.py
   ```
5. Confira que `.env` e `.venv/` estão no `.gitignore` e envie **apenas** o seu script:
   ```bash
   git add fundamentos/seu-nome/teste_conexao.py
   git commit -m "feat: adiciona teste de ambiente"
   git push -u origin exercicio/ambiente-uv
   ```
6. Abra o Pull Request. Se `git status` mostrar `pyproject.toml` ou `uv.lock` alterados, **não os inclua**: desfaça com `git restore pyproject.toml uv.lock`.

## Checklist da Parte D

- [ ] Instalou o uv e confirmou com `uv --version`
- [ ] Tem Python 3.10+ disponível (do sistema ou via `uv python install`)
- [ ] Entende o papel de `pyproject.toml`, `uv.lock` e `.venv`
- [ ] Sincronizou o ambiente com `uv sync`, sem alterar `pyproject.toml` e `uv.lock`
- [ ] Instalou as dependências do treinamento e os navegadores do Playwright
- [ ] Selecionou o interpretador/kernel da `.venv` no VS Code
- [ ] Configurou `.env` e `.gitignore`
- [ ] Executou o script de teste com sucesso
