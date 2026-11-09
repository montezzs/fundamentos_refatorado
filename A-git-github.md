# A - GitHub e Git

**Objetivo:** criar um repositório do zero e dominar o ciclo de trabalho com branches, commits e Pull Requests.

**Ao final deste capítulo você terá:** uma conta no GitHub, um repositório seu, e terá feito alterações nele pelo mesmo fluxo que a equipe usa nos projetos.

---

## A.1 Conceitos antes de começar

| Termo | O que é |
| :--- | :--- |
| **Git** | Programa de *controle de versões*: registra cada versão dos seus arquivos, permite voltar a versões antigas e organiza o trabalho de várias pessoas sem que uma sobrescreva a outra. Roda no seu computador. |
| **GitHub** | Site que guarda repositórios Git na internet. Serve para armazenar, compartilhar e colaborar em projetos. O Git funciona sem o GitHub; o GitHub é onde os projetos ficam publicados para a equipe. |
| **Repositório (repo)** | A pasta de um projeto controlada pelo Git, com todo o histórico de alterações. Existe uma cópia no GitHub (o *remoto*) e uma no seu computador (a *local*). |
| **Commit** | Um "ponto de salvamento" no histórico: um conjunto de alterações com uma mensagem explicando o que foi feito. |
| **Branch** | Uma linha de trabalho paralela. A branch principal se chama `main`. Você cria uma branch para cada tarefa e altera os arquivos sem mexer na `main`. |
| **Push / Pull** | `push` envia seus commits para o GitHub; `pull` traz para o seu computador as alterações que estão no GitHub. |
| **Pull Request (PR)** | Um pedido, feito no GitHub, para juntar (*merge*) as alterações de uma branch na `main`. É onde a equipe revisa o trabalho antes de ele entrar no projeto. |
| **Terminal** | Janela onde você digita comandos de texto em vez de clicar. No Windows se chama PowerShell ou Prompt de Comando; no macOS e no Linux, Terminal. |

**Por que tanto cuidado?** Se todos editassem e enviassem direto para a `main`, duas pessoas poderiam enviar ao mesmo tempo ou trabalhar sobre versões diferentes, e funcionalidades seriam perdidas. Branches e Pull Requests garantem que cada alteração seja feita em separado, revisada e só depois incorporada.

---

## A.2 Criar a conta no GitHub

1. Acesse [github.com/signup](https://github.com/signup).
2. Informe e-mail, senha e nome de usuário. O nome de usuário aparece em todos os seus projetos; prefira algo profissional.
3. Confirme o e-mail.

> **Estudantes:** o [GitHub Education](https://education.github.com/pack) oferece benefícios gratuitos, incluindo mais horas de Codespaces. Pode pedir com o e-mail institucional.

---

## A.3 Criar o repositório

1. No GitHub, clique no **+** no canto superior direito e escolha **New repository**.
2. Preencha:
   - **Repository name:** `modulo-0-fundamentos`
   - **Description:** opcional, uma frase sobre o projeto.
   - **Visibility:** *Public* (qualquer pessoa vê) ou *Private* (só você e quem você convidar).
   - Marque **Add a README file**. O `README.md` é a página de apresentação do repositório.
   - Em **Add .gitignore**, escolha o modelo **Python**. O `.gitignore` é uma lista de arquivos que o Git deve ignorar (como senhas e pastas geradas automaticamente). O modelo Python já inclui `.env` e `.venv/`, que vamos usar mais tarde.
3. Clique em **Create repository**.

Pronto: o repositório existe no GitHub, com a branch `main` e um primeiro commit.

---

## A.4 Escolher onde trabalhar

Você precisa de um lugar com Git e terminal para editar o repositório. Há duas opções. **Escolha uma.**

### Opção 1 - GitHub Codespaces (recomendada para começar)

O **Codespaces** é um computador na nuvem, oferecido pelo GitHub, que abre no navegador com um editor (VS Code) e um terminal. O Git já vem instalado, o repositório já vem baixado e você já está autenticado: não é preciso instalar nada.

1. Na página do seu repositório, clique no botão verde **Code**.
2. Abra a aba **Codespaces** e clique em **Create codespace on main**.
3. Aguarde abrir. O terminal fica na parte de baixo da tela; se não aparecer, use o menu **☰ → Terminal → New Terminal**.

> O Codespaces tem uma cota gratuita mensal de horas. Ao terminar, pare o codespace em [github.com/codespaces](https://github.com/codespaces) (menu **⋯ → Stop codespace**). Ele também para sozinho após um tempo sem uso.

Com o Codespaces aberto, **pule para a seção A.5**.

### Opção 2 - No seu computador

**1. Instale o Git.** Baixe em [git-scm.com/downloads](https://git-scm.com/downloads) e instale com as opções padrão. No macOS, também pode rodar `xcode-select --install`.

**2. Abra o terminal.**
- Windows: menu Iniciar → digite **PowerShell** → abrir.
- macOS: `Cmd+Espaço` → digite **Terminal**.
- Linux: `Ctrl+Alt+T`.

Confira a instalação:

```bash
git --version
```

**3. Identifique-se para o Git** (uma vez por computador). Cada commit registra o autor; use o mesmo e-mail da sua conta do GitHub:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

**4. Autentique-se no GitHub com o GitHub CLI.**

O GitHub **não aceita a senha da conta** quando você envia arquivos pelo terminal. É preciso autorizar o computador de outra forma, e a mais simples é o GitHub CLI.

O **GitHub CLI** (comando `gh`) é um programa oficial do GitHub para usar o site pelo terminal: fazer login, criar repositórios, abrir Pull Requests etc. Aqui vamos usá-lo apenas para o login.

- Instale pelo site [cli.github.com](https://cli.github.com/) (Windows e macOS têm instalador; no Linux, siga as instruções da página para a sua distribuição).
- Feche e reabra o terminal e rode:

```bash
gh auth login
```

Responda às perguntas: **GitHub.com** → **HTTPS** → **Yes** (autenticar o Git) → **Login with a web browser**. O terminal mostra um código; o navegador abre, você cola o código e autoriza. Confira com:

```bash
gh auth status
```

**5. Baixe o repositório para o computador (clonar).** *Clonar* é copiar o repositório do GitHub para uma pasta local, já ligada ao remoto. Na página do repositório, clique em **Code → HTTPS** e copie o link. No terminal:

```bash
git clone https://github.com/SEU-USUARIO/modulo-0-fundamentos.git
cd modulo-0-fundamentos
```

O `cd` (*change directory*) entra na pasta criada. Todos os comandos a seguir devem ser rodados dentro dela.

---

## A.5 O ciclo de trabalho

Este é o ciclo que você vai repetir em toda tarefa:

```
Atualizar a main
    │
    ▼
Criar uma branch para a tarefa
    │
    ▼
Alterar arquivos
    │
    ▼
Registrar as alterações (add + commit)
    │
    ▼
Enviar a branch para o GitHub (push)
    │
    ▼
Abrir o Pull Request e fazer o merge
```

Vamos percorrê-lo criando um arquivo de anotações.

### Passo 1 - Atualizar a main

```bash
git switch main
git pull origin main
```

- `git switch main` vai para a branch `main`.
- `git pull origin main` traz o que houver de novo no GitHub. `origin` é o apelido que o Git dá ao repositório remoto de onde você clonou.

Faça isso **sempre antes de criar uma branch**, para começar da versão mais recente.

### Passo 2 - Criar uma branch

```bash
git switch -c tarefa/primeiras-notas
```

O `-c` (*create*) cria a branch e já muda para ela. Use nomes curtos que descrevam a tarefa, como `tarefa/...`, `exercicio/...` ou `correcao/...`. Para ver em qual branch você está:

```bash
git branch
```

A branch atual aparece com `*`.

> Você pode encontrar em outros materiais `git checkout -b <nome>` (criar) e `git checkout <nome>` (trocar). Fazem o mesmo; `git switch` é a forma mais nova e mais clara.

### Passo 3 - Alterar arquivos

Crie um arquivo `notas.md` com algum texto. Pelo terminal:

```bash
echo "# Minhas notas de Git" > notas.md
```

(ou crie e edite o arquivo pelo editor, se estiver no Codespaces). Veja o que mudou:

```bash
git status
```

O `git status` lista arquivos novos, modificados e o que já está preparado para o commit. Use-o o tempo todo.

### Passo 4 - Registrar as alterações (add + commit)

```bash
git add notas.md
git commit -m "doc: cria arquivo de notas"
```

- `git add` escolhe **quais** alterações entram no próximo commit (essa seleção se chama *staging*). `git add .` adiciona todas de uma vez; prefira listar os arquivos quando houver alterações que não devem ir juntas.
- `git commit -m "mensagem"` cria o ponto de salvamento. Escreva o que foi feito. Um padrão útil é começar com um prefixo: `feat:` (novidade), `fix:` (correção), `doc:` (documentação), `refactor:` (reorganização).

Para ver o histórico:

```bash
git log --oneline
```

### Passo 5 - Enviar a branch (push)

```bash
git push -u origin tarefa/primeiras-notas
```

Até aqui a branch só existia no seu computador; agora ela está no GitHub. O `-u` liga a branch local à remota, então nos próximos envios dessa branch basta `git push`.

### Passo 6 - Abrir o Pull Request e fazer o merge

1. Abra a página do repositório no GitHub. Aparece um aviso amarelo com o botão **Compare & pull request**; clique nele. (Se não aparecer: aba **Pull requests → New pull request**, e escolha sua branch.)
2. Confira que está pedindo para juntar **`tarefa/primeiras-notas` → `main`**.
3. Escreva um título e uma descrição do que foi feito. A descrição aceita Markdown, a formatação explicada no capítulo B.
4. Clique em **Create pull request**.
5. Na aba **Files changed** dá para ver exatamente o que mudou. Em projetos da equipe, é aqui que os revisores comentam.
6. Como o repositório é seu, você mesmo pode aprovar: clique em **Merge pull request → Confirm merge**. Depois, **Delete branch** para remover a branch do GitHub (o histórico continua guardado).

### Passo 7 - Trazer o resultado de volta

O merge aconteceu no GitHub. Atualize seu computador:

```bash
git switch main
git pull origin main
git branch -d tarefa/primeiras-notas
```

O último comando apaga a branch local, que já foi incorporada. O ciclo recomeça no Passo 1 na próxima tarefa.

---

## A.6 Notebooks e arquivos que não devem ir para o Git

- **Jupyter Notebooks (`.ipynb`):** antes de commitar, limpe as saídas das células (no VS Code, botão **Clear All Outputs** no topo do notebook). Isso evita guardar tabelas pesadas e imagens no histórico.
- **Senhas e chaves** ficam em um arquivo `.env`, que nunca deve ser commitado. O `.gitignore` criado em A.3 já o ignora. Se uma chave for commitada por engano, apagar o arquivo depois não basta (ela continua no histórico): troque a chave no serviço que a forneceu.

---

## A.7 Trabalhando no repositório da equipe

Nos projetos do laboratório o repositório não é seu, mas o ciclo é o mesmo. Muda só o começo:

- **Se você foi adicionado como colaborador** (chega um convite por e-mail ou em [github.com/notifications](https://github.com/notifications) - aceite-o): clone o repositório da equipe e siga o ciclo A.5 normalmente. A diferença é que o merge do PR é feito por quem revisa, não por você.
- **Se você não é colaborador**, o `push` dá erro `403 / Permission denied`. Nesse caso, crie um **fork** - uma cópia do repositório da equipe na sua conta - pelo botão **Fork** no GitHub. Clone o *seu* fork, trabalhe nele e, ao abrir o PR, escolha como destino a `main` do repositório original.

---

## A.8 Erros comuns

| Situação | O que fazer |
| :--- | :--- |
| `Authentication failed` ou o terminal pede senha no `push` | Faça o login com o GitHub CLI (`gh auth login`), como em A.4. |
| `403` / `Permission denied` no `push` | Você não tem permissão no repositório. Veja A.7. |
| `fatal: not a git repository` | Você não está dentro da pasta do repositório. Entre nela com `cd nome-da-pasta`. |
| Fiz commits na `main` por engano (sem `push`) | Crie a branch a partir de onde está: `git switch -c tarefa/minha-branch`, envie essa branch e depois realinhe a `main` local: `git switch main` e `git reset --hard origin/main`. ⚠️ O `reset --hard` descarta alterações não commitadas na `main`. |
| `push` rejeitado: `Updates were rejected` | Existe algo no GitHub que você ainda não tem nessa branch. Rode `git pull` e depois `git push`. |
| Esqueci um arquivo no último commit (sem `push`) | `git add arquivo` e `git commit --amend --no-edit`. |

---

## A.9 Conflitos de merge (para consulta)

> Você provavelmente não vai encontrar conflitos no seu repositório pessoal. Esta seção fica para quando trabalhar com a equipe.

Um **conflito** acontece quando duas branches alteram as mesmas linhas de um arquivo e o Git não sabe qual versão manter. Ao rodar `git pull` ou `git merge`, o Git para e marca o trecho no arquivo:

```
<<<<<<< HEAD
A sua versão
=======
A versão que veio da outra branch
>>>>>>> main
```

Para resolver no VS Code:

1. Abra o arquivo. Acima do trecho aparecem as opções:
   - **Accept Current Change** - fica a sua versão;
   - **Accept Incoming Change** - fica a versão da outra branch;
   - **Accept Both Changes** - ficam as duas.
2. Se nenhuma servir, apague os marcadores (`<<<<<<<`, `=======`, `>>>>>>>`) e escreva a versão correta à mão.
3. Salve e finalize:

```bash
git add nome_do_arquivo
git commit -m "merge: resolve conflito em nome_do_arquivo"
git push
```

---

## Exercício do Capítulo A

1. Crie a conta e o repositório `modulo-0-fundamentos` (A.2 e A.3).
2. Abra o repositório no Codespaces ou clone-o no computador (A.4).
3. Siga o ciclo completo (A.5) com uma branch `exercicio/git`, criando um arquivo `sobre-mim.md` com seu nome e sua trilha.
4. Abra o Pull Request, confira a aba **Files changed** e faça o merge.
5. Atualize a `main` local e confirme com `git log --oneline` que o seu commit aparece.

## Checklist do Capítulo A

- [ ] Sei explicar o que são Git, GitHub, repositório, commit, branch e Pull Request
- [ ] Criei conta e repositório com README e `.gitignore` Python
- [ ] Tenho um ambiente com Git funcionando (Codespaces, ou Git + GitHub CLI no computador)
- [ ] Criei uma branch a partir da `main` atualizada
- [ ] Fiz commit com mensagem descritiva e enviei com `git push`
- [ ] Abri e fiz o merge de um Pull Request
- [ ] Sei o que fazer para contribuir no repositório da equipe (colaborador ou fork)

## Links de apoio

- [Documentação do GitHub em português](https://docs.github.com/pt/get-started)
- [GitHub CLI - manual](https://cli.github.com/manual/)
- Referência rápida de Git e GitHub (Sisproex)
- [Oh Shit, Git!?!](https://ohshitgit.com/) - como desfazer situações comuns
