# A — GitHub e Git

**Objetivo:** branches, commits e Pull Requests do fluxo da equipe.

## A.0 Pré-requisitos

Para seguir esta parte você precisa de um terminal e de uma conta no GitHub. Escolha uma das opções (os detalhes estão na parte C):

- **Codespaces (mais simples):** na página do repositório, clique em **Code → Codespaces → Create codespace on main**. O Git já vem instalado, o repositório já vem clonado e você já está autenticado. Pule para o [Passo 2](#passo-2--criar-uma-branch-para-a-atividade).
- **Máquina local:** instale o [Git](https://git-scm.com/downloads) e o [VS Code](https://code.visualstudio.com/). Abra o terminal integrado do VS Code com ``Ctrl+` `` (crase).

## A.1 O que são

- **Git** é um sistema de controle de versões que roda na sua máquina. Ele registra cada versão do código, permite voltar a versões antigas e organiza o trabalho de várias pessoas sem que uma sobrescreva a outra.
- **GitHub** é uma plataforma online que hospeda repositórios Git. Serve para armazenar, compartilhar e, principalmente, colaborar em um mesmo projeto.

As boas práticas a seguir podem parecer burocráticas no início, mas existem por um motivo: se qualquer pessoa editasse e enviasse direto para o código principal, duas pessoas poderiam enviar ao mesmo tempo ou trabalhar sobre versões diferentes, e funcionalidades seriam perdidas. Por isso, cada participante trabalha em uma **branch própria** e, antes de enviar, garante que partiu da versão mais atual do código principal.

## A.2 Configuração inicial (apenas uma vez por máquina local)

```bash
git --version
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

Use o mesmo e-mail da sua conta do GitHub, para que os commits apareçam vinculados ao seu perfil.

### Autenticação no GitHub

O GitHub **não aceita a senha da conta** em `git push`. Se você não se autenticar de outra forma, o primeiro envio vai falhar com erro de autenticação. Escolha uma das opções:

- **GitHub CLI (recomendado):** instale o [GitHub CLI](https://cli.github.com/) e rode:
  ```bash
  gh auth login
  ```
  Escolha **GitHub.com → HTTPS → Login with a web browser** e siga as instruções.
- **Pelo VS Code:** no primeiro `push` feito pelo painel Source Control, o VS Code abre o navegador para você entrar na conta do GitHub.
- **Windows:** o instalador do Git inclui o Git Credential Manager, que abre uma janela de login no primeiro `push`.

> No Codespaces nada disso é necessário: a autenticação já vem configurada.

## A.3 Fluxo de contribuição padrão

```
GitHub (repositório central)
    │
    ▼
Clonar o projeto (apenas na primeira vez)
    │
    ▼
Atualizar a main e criar uma branch para o exercício
    │
    ▼
Desenvolver o exercício / análise
    │
    ▼
Salvar as alterações (add + commit)
    │
    ▼
Enviar a branch para o GitHub (push)
    │
    ▼
Abrir um Pull Request (PR)
```

> **Permissão de escrita:** este fluxo pressupõe que você foi adicionado como colaborador do repositório (aceite o convite que chega por e-mail ou em github.com/notifications). Se o `git push` retornar **403 / Permission denied**, você ainda não tem permissão: fale com os responsáveis. Sem permissão, o caminho alternativo é criar um **fork** (botão **Fork** no GitHub), clonar o seu fork e abrir o PR do fork para o repositório original.

### Passo 1 — Clonar o repositório

```bash
git clone https://github.com/colabhd/material-didatico-trilhas.git
cd material-didatico-trilhas
```

Substitua o link pelo repositório oficial da sua trilha.

### Passo 2 — Criar uma branch para a atividade

Uma **branch** é uma linha de desenvolvimento separada: você altera o projeto sem modificar o código principal (`main`). Crie uma branch para **cada tarefa**, por menor que seja.

Sempre parta da versão mais recente da `main`:

```bash
git switch main
git pull origin main
git switch -c exercicio/nome-aluno-modulo-0
```

Para trocar entre branches existentes:

```bash
git switch exercicio/nome-aluno-modulo-0
git switch main
```

> `git switch` é o comando moderno. Os equivalentes antigos, ainda válidos, são `git checkout -b <branch>` (criar) e `git checkout <branch>` (trocar).

Lembre-se: a branch criada existe só no seu computador até você fazer `push`. E mudanças na `main` não aparecem automaticamente na sua branch — por isso o `git pull` antes de criar uma nova.

### Passo 3 — Registrar e enviar as mudanças

```bash
git status                 # mostra o que mudou
git add exemplo.py         # adiciona um arquivo específico
git add .                  # ou adiciona todos os arquivos alterados
git commit -m "feat: adiciona script de validacao do ambiente local"
git push -u origin exercicio/nome-aluno-modulo-0
```

- `git add` escolhe quais alterações vão para o próximo commit (área de *staging*). Prefira adicionar arquivos específicos quando houver alterações que não devem ir junto.
- `git commit -m` registra as alterações com uma mensagem descritiva. Use prefixos como `feat:`, `fix:`, `doc:`, `refactor:`.
- `git push -u` envia a branch ao GitHub; o `-u` vincula a branch local à remota, então nos próximos envios basta `git push`.

> ⚠️ **Jupyter Notebooks (`.ipynb`)**: antes de commitar, limpe as saídas das células (botão **Clear All Outputs** no topo do notebook no VS Code). Isso evita salvar tabelas pesadas e imagens no histórico do Git.

> ⚠️ **Nunca commite** o arquivo `.env` nem a pasta `.venv/`. Veja a parte D.

### Passo 4 — Abrir o Pull Request

No GitHub, um banner sugerirá criar o PR da branch enviada. Clique em **Compare & pull request**, descreva a entrega (em Markdown — parte B), vincule a Issue correspondente (por exemplo, `Closes #12`) e envie para revisão.

## A.4 Erros comuns

| Situação | O que fazer |
| :--- | :--- |
| `Authentication failed` / pede senha no `push` | Autentique-se como em [A.2](#autenticação-no-github). |
| `403` / `Permission denied` no `push` | Você não é colaborador do repositório. Veja o aviso de permissão em A.3. |
| Fiz commits na `main` por engano (sem `push`) | Crie a branch a partir de onde está (`git switch -c exercicio/minha-branch`), envie essa branch e depois realinhe a `main` local com `git switch main` e `git reset --hard origin/main`. ⚠️ O `reset --hard` apaga alterações não commitadas na `main`. |
| `push` rejeitado: `Updates were rejected` | Alguém enviou alterações na mesma branch. Rode `git pull` e depois `git push` de novo. |
| Minha branch está desatualizada em relação à `main` | Na sua branch: `git pull origin main`. Se houver conflito, veja A.5. |
| Esqueci um arquivo no último commit (sem `push`) | `git add arquivo` e `git commit --amend --no-edit`. |

## A.5 Conflitos de merge (consulta futura)

> ⚠️ Por enquanto você não precisa se preocupar com isso. Esta seção fica para consulta.

Conflitos ocorrem quando duas pessoas alteram as mesmas linhas de um arquivo em branches diferentes e o Git não consegue decidir qual versão manter. Ao fazer `git pull` ou `git merge`, o Git interrompe o processo e marca o arquivo:

```
<<<<<<< HEAD
Seu código local
=======
O código vindo da outra branch
>>>>>>> main
```

**Resolvendo no VS Code:**

1. Abra o arquivo. O VS Code mostra opções acima do bloco:
   - **Accept Current Change** — mantém a sua versão;
   - **Accept Incoming Change** — mantém a versão da outra branch;
   - **Accept Both Changes** — mantém as duas.
2. Se nenhuma opção resolver a lógica, apague os marcadores (`<<<<<<<`, `=======`, `>>>>>>>`) e edite manualmente.
3. Finalize:

```bash
git add nome_do_arquivo.py
git commit -m "merge: resolve conflitos de integracao no arquivo X"
git push
```

## A.6 Links de apoio

- Referência rápida de Git e GitHub (Sisproex)
- [Oh Shit, Git!?!](https://ohshitgit.com/) — como desfazer situações comuns
- [GitHub CLI — `gh auth login`](https://cli.github.com/manual/gh_auth_login)

## Checklist da Parte A

- [ ] Configurou nome e e-mail no Git (ou está usando o Codespaces)
- [ ] Autenticou-se no GitHub
- [ ] Aceitou o convite de colaborador do repositório
- [ ] Clonou o repositório e acessou a pasta localmente
- [ ] Criou uma branch exclusiva, no padrão do projeto, a partir da `main` atualizada
- [ ] Fez o commit com mensagem descritiva
- [ ] Enviou a branch com `git push`
- [ ] Abriu o Pull Request vinculando a Issue correspondente
