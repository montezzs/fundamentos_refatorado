# D — Ambiente de trabalho (uv)

**Objetivo:** criar um projeto Python com dependências isoladas e reproduzíveis usando o uv.

**Ao final deste capítulo você terá:** um projeto Python com as bibliotecas do curso instaladas, um script de teste funcionando e os arquivos certos guardados no Git para que qualquer pessoa recrie o mesmo ambiente.

---

## D.1 Conceitos antes de começar

| Termo | O que é |
| :--- | :--- |
| **Python** | A linguagem de programação mais usada em ciência de dados, com bibliotecas prontas para coletar, analisar e visualizar dados. |
| **Pacote (biblioteca)** | Código pronto, escrito por outras pessoas, que você instala e usa no seu projeto. Exemplo: o `pandas`, para tabelas de dados. |
| **Dependência** | Um pacote de que o seu projeto precisa para funcionar. Pacotes também têm dependências próprias, instaladas junto. |
| **Ambiente virtual (venv)** | Uma pasta isolada (aqui, `.venv`) com uma cópia do Python e os pacotes de **um** projeto. Assim, um projeto pode usar o `pandas` 2.1 e outro o 2.2 no mesmo computador, sem conflito. |
| **Gerenciador de pacotes** | Programa que instala, atualiza e remove pacotes e registra quais o projeto usa. |
| **uv** | O gerenciador que usamos. Cria o ambiente virtual, instala pacotes (muito mais rápido que o `pip`, o instalador tradicional do Python), instala versões do próprio Python e garante que todos da equipe tenham exatamente o mesmo ambiente. Documentação: [docs.astral.sh/uv](https://docs.astral.sh/uv/). |

Um projeto uv é formado por estes arquivos:

| Arquivo | O que é | Vai para o Git? |
| :--- | :--- | :--- |
| `pyproject.toml` | Descrição do projeto e lista das dependências que você pediu (ex.: `pandas>=2.2`). | ✅ Sim |
| `uv.lock` | Registro das versões **exatas** de todos os pacotes instalados, incluindo as dependências das dependências. É o que torna o ambiente reproduzível. | ✅ Sim |
| `.python-version` | Versão do Python usada no projeto. | ✅ Sim |
| `.venv/` | O ambiente virtual com os pacotes instalados. É grande e pode ser recriado a qualquer momento. | ❌ Não |

---

## D.2 Preparação: terminal e pasta do projeto

Você precisa de um **terminal** (janela para digitar comandos) aberto dentro da pasta do projeto. Escolha uma opção:

- **GitHub Codespaces (sem instalar nada):** um computador na nuvem que abre um editor com terminal no navegador. Crie uma conta em [github.com/signup](https://github.com/signup), crie um repositório (**+ → New repository**, nome `modulo-0-fundamentos`, marque **Add a README file** e escolha o **.gitignore** do tipo **Python**) e, na página dele, clique em **Code → Codespaces → Create codespace on main**. O terminal fica na parte de baixo da tela (se não aparecer: menu **☰ → Terminal → New Terminal**).
- **No seu computador:** abra a pasta do projeto no VS Code (**File → Open Folder**) e abra o terminal com ``Ctrl+` ``. Sem VS Code, use o PowerShell (Windows) ou o Terminal (macOS/Linux) e entre na pasta com `cd caminho/da/pasta`.

Confira em que pasta está com `pwd` (no PowerShell: `Get-Location`). Todos os comandos deste capítulo são rodados nela.

---

## D.3 Instalar o uv

Veja se já está instalado:

```bash
uv --version
```

Se aparecer um número de versão, pule para D.4. Se não:

**macOS, Linux e Codespaces:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

(`curl` baixa o instalador oficial, e `sh` o executa.)

**Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Feche e reabra o terminal** para ele reconhecer o novo comando, e rode `uv --version` de novo. Outros métodos de instalação estão na [página de instalação do uv](https://docs.astral.sh/uv/getting-started/installation/).

---

## D.4 Python

Usamos **Python 3.10 ou superior**. Você não precisa instalar o Python separadamente: o uv usa o que já existe no computador e, se não houver uma versão compatível, baixa uma automaticamente.

Para escolher uma versão específica:

```bash
uv python install 3.12   # instala o Python 3.12
uv python list           # mostra as versões disponíveis e instaladas
```

---

## D.5 Criar o projeto

Dentro da pasta do projeto:

```bash
uv init --python 3.12
```

Esse comando cria `pyproject.toml`, `.python-version` e um `main.py` de exemplo. Se a pasta ainda não for um repositório Git, ele também cria um; se já tiver um `README.md`, ele não é substituído.

Abra o `pyproject.toml` para conhecê-lo. Por enquanto, a lista `dependencies` está vazia.

---

## D.6 Instalar as bibliotecas do curso

```bash
uv add scrapy playwright httpx pandas jupyter matplotlib seaborn wordcloud networkx python-dotenv
```

O `uv add` cria a `.venv` (se ainda não existir), instala os pacotes nela e atualiza o `pyproject.toml` e o `uv.lock`. Para que serve cada um, de forma resumida (veremos em detalhe nas próximas aulas):

| Pacote | Uso |
| :--- | :--- |
| `httpx` | Fazer requisições a sites e APIs |
| `scrapy` | Raspagem de sites em grande escala |
| `playwright` | Controlar um navegador automaticamente, para sites que dependem de JavaScript |
| `pandas` | Manipular tabelas de dados |
| `jupyter` | Notebooks interativos |
| `matplotlib`, `seaborn` | Gráficos |
| `wordcloud` | Nuvens de palavras |
| `networkx` | Análise de redes (grafos) |
| `python-dotenv` | Ler senhas e chaves de um arquivo `.env` |

Para remover um pacote: `uv remove nome-do-pacote`.

O Playwright precisa baixar os navegadores que ele controla (usados na trilha de Coleta):

```bash
uv run playwright install
```

> [!NOTE]
> No Linux ou no Codespaces, se aparecer um erro sobre bibliotecas do sistema ausentes, rode `uv run playwright install --with-deps`. No computador local, isso pode pedir a senha de administrador.

---

## D.7 Executar código: `uv run`

O `uv run` executa um comando usando o Python e os pacotes do projeto. Ele também confere, antes, se o ambiente está de acordo com o `uv.lock`:

```bash
uv run python main.py
uv run jupyter lab
```

É a forma recomendada, porque dispensa *ativar* o ambiente.

### Alternativa: ativar a `.venv`

*Ativar* o ambiente faz com que o comando `python` daquele terminal passe a usar a `.venv`:

| Sistema | Comando |
| :--- | :--- |
| macOS / Linux / Codespaces | `source .venv/bin/activate` |
| Windows (PowerShell) | `.venv\Scripts\Activate.ps1` |
| Windows (CMD) | `.venv\Scripts\activate.bat` |

Após ativar, `(.venv)` aparece no começo da linha do terminal. Para desativar: `deactivate`.

**Erro no PowerShell: "a execução de scripts foi desabilitada neste sistema".** É uma proteção do Windows que bloqueia scripts, como o de ativação. Para liberar apenas para o seu usuário, sem precisar de administrador:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Confirme com `S`. Se preferir não mudar a configuração, use `uv run`, que não depende de ativação.

---

## D.8 Fazer o VS Code usar a `.venv`

O VS Code precisa saber qual Python usar; senão, ele não encontra os pacotes instalados e marca os `import` como erro.

1. Abra a Paleta de Comandos (a caixa de busca de ações do VS Code): `Ctrl+Shift+P` (`Cmd+Shift+P` no macOS).
2. Digite e selecione **Python: Select Interpreter**.
3. Escolha o Python da `.venv`:
   - `./.venv/Scripts/python.exe` (Windows)
   - `./.venv/bin/python` (macOS / Linux / Codespaces)

   Ele costuma aparecer marcado como **Recommended**. Se não aparecer, escolha **Enter interpreter path...** e selecione o arquivo manualmente.

Isso exige a extensão **Python** da Microsoft (painel de extensões: `Ctrl+Shift+X`).

**Notebooks (trilha de Análise):** com a extensão **Jupyter** instalada, abra ou crie um arquivo `.ipynb`, clique em **Select Kernel** no canto superior direito e escolha o Python da `.venv`. O *kernel* é o Python que executa as células do notebook.

---

## D.9 Senhas e chaves: o arquivo `.env`

Alguns projetos usam chaves de API (códigos de acesso a serviços), senhas ou tokens. Eles **nunca** devem ir para o GitHub.

1. Na pasta do projeto, crie um arquivo chamado exatamente `.env` (com o ponto no início).
2. Escreva as credenciais, uma por linha:
   ```
   TWOCAPTCHA_API_KEY=sua_chave_aqui
   ```
3. Confira se o arquivo `.gitignore` (a lista de arquivos que o Git ignora) contém as linhas abaixo. Se não existir, crie-o:
   ```
   .env
   .venv/
   ```
4. No código, leia as variáveis com o `python-dotenv`:
   ```python
   import os
   from dotenv import load_dotenv

   load_dotenv()
   chave = os.getenv("TWOCAPTCHA_API_KEY")
   ```

> [!CAUTION]
> Se uma chave for enviada ao GitHub por engano, apagar o arquivo depois não resolve: ela continua no histórico. Cancele a chave no serviço que a forneceu e gere uma nova. No Codespaces, você pode guardar segredos em **Settings → Codespaces → Secrets** da sua conta, e eles ficam disponíveis como variáveis de ambiente.

---

## D.10 Testar o ambiente

Crie o arquivo `teste_conexao.py` na pasta do projeto:

```python
import httpx
import pandas as pd


def testar_ambiente():
    print("Iniciando testes do ambiente virtual...\n")

    # 1. Coleta (HTTPX): tenta acessar um site
    url = "https://practicesoftwaretesting.com/"
    try:
        response = httpx.get(url, timeout=10, follow_redirects=True)
        if response.status_code == 200:
            print("✅ Coleta: conexão HTTPX ativa.")
        else:
            print(f"⚠️ Coleta: conexão estabelecida, mas o status foi {response.status_code}")
    except httpx.HTTPError as e:
        print(f"❌ Coleta: falha ao conectar: {e}")

    # 2. Análise (Pandas): mostra a versão instalada
    print(f"✅ Análise: Pandas importado com sucesso. Versão: {pd.__version__}")


if __name__ == "__main__":
    testar_ambiente()
```

Salve e execute:

```bash
uv run python teste_conexao.py
```

Se o `httpx` ou o `pandas` não estiverem instalados, o script para logo na primeira linha com `ModuleNotFoundError`, antes de qualquer teste.

**Se der `ModuleNotFoundError`:**

1. O terminal está na pasta do projeto (onde fica o `pyproject.toml`)? Confira com `pwd` ou `ls`.
2. Você rodou o `uv add` da seção D.6?
3. Executou com `uv run` (ou com a `.venv` ativada)?
4. No VS Code, o interpretador selecionado é o da `.venv` (D.8)?
5. O arquivo foi salvo antes de executar?

---

## D.11 Guardar o projeto no Git

Para que outras pessoas recriem o seu ambiente, `pyproject.toml`, `uv.lock` e `.python-version` precisam estar no repositório. Se a pasta for um repositório Git com cópia no GitHub:

```bash
git status
git add pyproject.toml uv.lock .python-version teste_conexao.py
git commit -m "feat: configura ambiente com uv"
git push
```

- `git status` mostra o que mudou. Confira que `.venv/` e `.env` **não** aparecem; se aparecerem, falta incluí-los no `.gitignore`.
- `git add` escolhe os arquivos que vão para o registro.
- `git commit -m` cria o registro no histórico com uma mensagem.
- `git push` envia para o GitHub.

---

## D.12 Entrando em um projeto que já existe

Quando você baixa um projeto que já usa uv (por exemplo, um repositório da equipe), **não** rode `uv init` nem `uv add`. Basta:

```bash
uv sync
```

O `uv sync` cria a `.venv` e instala exatamente as versões registradas no `uv.lock`. Em seguida, se o projeto usar Playwright, rode `uv run playwright install`.

> [!WARNING]
> Em repositórios compartilhados, só adicione ou remova dependências se isso fizer parte da sua tarefa. Cada `uv add` ou `uv remove` altera `pyproject.toml` e `uv.lock`, e várias pessoas alterando esses arquivos ao mesmo tempo causa conflitos. Na dúvida, pergunte aos responsáveis. Se alterou sem querer, desfaça com `git restore pyproject.toml uv.lock`.

---

## D.13 Resumo de comandos

| Comando | Função |
| :--- | :--- |
| `uv init` | Cria um novo projeto |
| `uv add <pacote>` | Adiciona uma dependência |
| `uv remove <pacote>` | Remove uma dependência |
| `uv sync` | Recria o ambiente a partir do `uv.lock` |
| `uv run <comando>` | Executa um comando no ambiente do projeto |
| `uv lock --upgrade` | Atualiza as versões registradas no `uv.lock` |
| `uv tree` | Mostra a árvore de dependências |
| `uv python install <versão>` | Instala uma versão do Python |

---

## Exercício do Capítulo D

1. Abra um terminal na pasta do seu projeto (D.2).
2. Instale o uv (D.3) e crie o projeto com `uv init --python 3.12` (D.5).
3. Instale as bibliotecas do curso e os navegadores do Playwright (D.6).
4. Selecione o interpretador da `.venv` no VS Code (D.8).
5. Crie o `.env` com uma chave de exemplo e confira o `.gitignore` (D.9).
6. Crie e execute o `teste_conexao.py` (D.10).
7. Guarde o projeto no Git (D.11), conferindo que `.venv/` e `.env` ficaram de fora.
8. Teste a reprodutibilidade: apague a pasta `.venv`, rode `uv sync` e execute o script de novo.

## Checklist do Capítulo D

- [ ] Sei explicar o que são pacote, dependência e ambiente virtual
- [ ] Instalei o uv e confirmei com `uv --version`
- [ ] Sei o papel de `pyproject.toml`, `uv.lock`, `.python-version` e `.venv`
- [ ] Criei o projeto e instalei as dependências do curso
- [ ] Instalei os navegadores do Playwright
- [ ] Selecionei o interpretador (e o kernel, se uso notebooks) da `.venv` no VS Code
- [ ] Configurei `.env` e `.gitignore`
- [ ] Executei o script de teste com sucesso
- [ ] Recriei o ambiente com `uv sync`

## Links de apoio

- [Documentação do uv](https://docs.astral.sh/uv/)
- [Guia de projetos com uv](https://docs.astral.sh/uv/guides/projects/)
- [Instalação do Playwright para Python](https://playwright.dev/python/docs/intro)
