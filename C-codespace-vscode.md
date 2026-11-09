# C — Codespace / VS Code

O **VS Code** é um editor de código gratuito e leve da Microsoft. É nele que escrevemos Python, editamos Markdown, abrimos notebooks e usamos o terminal.

Há duas formas de trabalhar:

| | VS Code local | GitHub Codespaces |
| :--- | :--- | :--- |
| Onde roda | No seu computador | Em uma máquina virtual na nuvem, pelo navegador ou pelo VS Code |
| Instalação | Instalar VS Code, Git e Python | Nenhuma: abre direto do repositório |
| Git | Precisa configurar | Já vem instalado e autenticado |
| Custo | Gratuito | Cota mensal gratuita para contas pessoais; acima dela é cobrado |
| Quando usar | Máquina com bom desempenho e uso frequente | Máquina fraca, sem permissão de instalação, ou para começar rápido |

> **Atenção à cota do Codespaces**: pare o codespace quando terminar de usar (ele também para sozinho após um período de inatividade) e apague os que não for mais usar. Os limites atuais estão na [documentação de cobrança do GitHub](https://docs.github.com/pt/billing/managing-billing-for-your-products/managing-billing-for-github-codespaces/about-billing-for-github-codespaces).

## C.1 Abrindo o projeto

**No Codespaces:** na página do repositório no GitHub, clique em **Code → Codespaces → Create codespace on main**. O editor abre já com a pasta do projeto e o terminal disponível.

**No VS Code local — a regra de ouro: "Abrir Pasta".** Não abra arquivos isolados (*File > Open File*). Abra sempre a **pasta raiz** do projeto:

1. **File → Open Folder**;
2. selecione a pasta do repositório clonado.

Assim o VS Code entende a estrutura do projeto, detecta o ambiente virtual (`.venv`) e executa os scripts sem erros de caminho.

## C.2 Barra lateral

| Painel | Atalho | Função |
| :--- | :--- | :--- |
| Explorer | `Ctrl+Shift+E` | Árvore de pastas e arquivos do projeto |
| Search | `Ctrl+Shift+F` | Busca termos em todos os arquivos |
| Source Control | `Ctrl+Shift+G` | Interface visual do Git: alterações, commits, push |
| Extensions | `Ctrl+Shift+X` | Instalar extensões |

No macOS, troque `Ctrl` por `Cmd`.

## C.3 Extensões essenciais

| Extensão | Para quê |
| :--- | :--- |
| **Python** (Microsoft) | Destaque de sintaxe, autocomplete, seleção de interpretador, depuração |
| **Jupyter** (Microsoft) | Abrir e executar notebooks `.ipynb` dentro do editor |
| **Markdown All in One** | Atalhos e pré-visualização de Markdown |
| **Rainbow CSV** | Colore as colunas de `.csv`/`.tsv` para conferência rápida |

Para instalar: `Ctrl+Shift+X`, pesquise pelo nome e clique em **Install**. No Codespaces o processo é o mesmo.

> **Dica para a equipe:** o repositório pode ter um arquivo `.vscode/extensions.json` listando essas extensões; o VS Code e o Codespaces sugerem instalá-las automaticamente ao abrir o projeto.

## C.4 Terminal integrado

Abra com ``Ctrl+` `` (crase) ou pelo menu **Terminal → New Terminal**. Ele já abre na pasta do projeto. No Codespaces, o terminal é Linux (bash), então use os comandos de macOS/Linux deste material.

## C.5 Ambiente pré-configurado (devcontainer)

O repositório tem um arquivo `.devcontainer/devcontainer.json`. Ao criar um codespace, ele já instala automaticamente o Python, o uv, as dependências do projeto, os navegadores do Playwright e as 4 extensões recomendadas. A primeira criação leva alguns minutos; as seguintes são rápidas.

> Se você criou o codespace antes de esse arquivo existir, recrie-o (ou use **Ctrl+Shift+P → Codespaces: Rebuild Container**).

No VS Code local o arquivo é ignorado, a menos que você use a extensão **Dev Containers** com Docker, o que não é necessário neste curso.

## Exercício da Parte C

1. Crie a branch:
   ```bash
   git switch main && git pull origin main
   git switch -c exercicio/configuracao-vscode
   ```
2. Abra o projeto via **Open Folder** (local) ou crie um codespace.
3. Instale as 4 extensões recomendadas (no Codespaces elas já vêm instaladas; confira no painel de Extensões).
4. Crie o arquivo `participantes/seu-nome.md` (troque `seu-nome` pelo seu nome, sem acentos nem espaços) com o seu nome, sua trilha e uma frase sobre você.
5. Abra o arquivo e a pré-visualização lado a lado com `Ctrl+K` e depois `V` (ou `Ctrl+Shift+V` para abrir em nova aba).
6. Tire um print do editor com o Markdown e a pré-visualização lado a lado e envie no grupo de trabalho.
7. Envie pelo fluxo de Pull Request:
   ```bash
   git add participantes/seu-nome.md
   git commit -m "doc: adiciona ficha de participante"
   git push -u origin exercicio/configuracao-vscode
   ```

> Cada pessoa cria um arquivo próprio para que os Pull Requests não entrem em conflito entre si.

## Checklist da Parte C

- [ ] Sabe a diferença entre VS Code local e Codespaces, incluindo a cota
- [ ] Entende por que abrir o projeto com **Open Folder**
- [ ] Navega pelos painéis da barra lateral
- [ ] Instalou as extensões de Python, Jupyter, Markdown e CSV
- [ ] Abre e usa o terminal integrado
- [ ] Usou a pré-visualização de Markdown
- [ ] Enviou a ficha de participante por Pull Request
