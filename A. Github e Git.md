A — GitHub e Git
A.1 O que são
Git é um sistema de controle de versões que roda na sua máquina. Ele registra cada versão do código, permite voltar a versões antigas e organiza o trabalho de várias pessoas sem que uma sobrescreva a outra.
GitHub é uma plataforma online que hospeda repositórios Git. Serve para armazenar, compartilhar e, principalmente, colaborar em um mesmo projeto.

As boas práticas a seguir podem parecer burocráticas no início, mas existem por um motivo: se qualquer pessoa editasse e enviasse direto para o código principal, duas pessoas poderiam enviar ao mesmo tempo ou trabalhar sobre versões diferentes, e funcionalidades seriam perdidas. Por isso, cada participante trabalha em uma branch própria e, antes de enviar, garante que partiu da versão mais atual do código principal.

A.2 Configuração inicial (apenas uma vez por máquina)
bash
git --version
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"

No GitHub Codespaces o Git já vem instalado e autenticado com a sua conta.

A.3 Fluxo de contribuição padrão
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

Passo 1 — Clonar o repositório
bash
git clone https://github.com/colabhd/material-didatico-trilhas.git
cd material-didatico-trilhas

Substitua o link pelo repositório oficial da sua trilha.

Passo 2 — Criar uma branch para a atividade

Uma branch é uma linha de desenvolvimento separada: você altera o projeto sem modificar o código principal (main). Crie uma branch para cada tarefa, por menor que seja.

Sempre parta da versão mais recente da main:

bash
git switch main
git pull origin main
git switch -c exercicio/nome-aluno-modulo-0

Para trocar entre branches existentes:

bash
git switch exercicio/nome-aluno-modulo-0
git switch main

git switch é o comando moderno. Os equivalentes antigos, ainda válidos, são git checkout -b <branch> (criar) e git checkout <branch> (trocar).

Lembre-se: a branch criada existe só no seu computador até você fazer push. E mudanças na main não aparecem automaticamente na sua branch — por isso o git pull antes de criar uma nova.

Passo 3 — Registrar e enviar as mudanças
bash
git status                 # mostra o que mudou
git add exemplo.py         # adiciona um arquivo específico
git add .                  # ou adiciona todos os arquivos alterados
git commit -m "feat: adiciona script de validacao do ambiente local"
git push -u origin exercicio/nome-aluno-modulo-0
git add escolhe quais alterações vão para o próximo commit (área de staging). Prefira adicionar arquivos específicos quando houver alterações que não devem ir junto.
git commit -m registra as alterações com uma mensagem descritiva. Use prefixos como feat:, fix:, doc:, refactor:.
git push -u envia a branch ao GitHub; o -u vincula a branch local à remota, então nos próximos envios basta git push.

⚠️ Jupyter Notebooks (.ipynb): antes de commitar, limpe as saídas das células (botão Clear All Outputs no topo do notebook no VS Code). Isso evita salvar tabelas pesadas e imagens no histórico do Git.

⚠️ Nunca commite o arquivo .env nem a pasta .venv/. Veja a parte D.

Passo 4 — Abrir o Pull Request

No GitHub, um banner sugerirá criar o PR da branch enviada. Clique em Compare & pull request, descreva a entrega (em Markdown — parte B), vincule a Issue correspondente (por exemplo, Closes #12) e envie para revisão.

A.4 Conflitos de merge (consulta futura)

⚠️ Por enquanto você não precisa se preocupar com isso. Esta seção fica para consulta.

Conflitos ocorrem quando duas pessoas alteram as mesmas linhas de um arquivo em branches diferentes e o Git não consegue decidir qual versão manter. Ao fazer git pull ou git merge, o Git interrompe o processo e marca o arquivo:

<<<<<<< HEAD
Seu código local
=======
O código vindo da outra branch
>>>>>>> main

Resolvendo no VS Code:

Abra o arquivo. O VS Code mostra opções acima do bloco:
Accept Current Change — mantém a sua versão;
Accept Incoming Change — mantém a versão da outra branch;
Accept Both Changes — mantém as duas.
Se nenhuma opção resolver a lógica, apague os marcadores (<<<<<<<, =======, >>>>>>>) e edite manualmente.
Finalize:
bash
git add nome_do_arquivo.py
git commit -m "merge: resolve conflitos de integracao no arquivo X"
git push
A.5 Links de apoio
Referência rápida de Git e GitHub (Sisproex)
Oh Shit, Git!?! — como desfazer situações comuns
Checklist da Parte A
 Configurou nome e e-mail no Git
 Clonou o repositório e acessou a pasta localmente
 Criou uma branch exclusiva, no padrão do projeto, a partir da main atualizada
 Fez o commit com mensagem descritiva
 Enviou a branch com git push
 Abriu o Pull Request vinculando a Issue correspondente
