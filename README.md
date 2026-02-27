# Versionamento

1) Preparação: escolha do ambiente
- Certifique-se de ter:
  - Git instalado (git --version)
  - Conta no GitHub
  - Acesso via terminal/ prompt de comando (ou Git Bash no Windows)
- Opcional: configure seu usuário global (faça apenas uma vez)
  - git config --global user.name "Seu Nome"
  - git config --global user.email "seu.email@example.com"
- Opcional: escolha um editor padrão (ex.: code, vim)
  - git config --global core.editor code --wait

2) Fluxo básico: criar um repositório local e publicá-lo no GitHub
Exercício A: projeto simples (ex.: "portfolio-primeiro-projeto")

- Passo 1: criar a pasta do projeto e inicializar o repositório
  - mkdir portfolio-primeiro-projeto
  - cd portfolio-primeiro-projeto
  - git init

- Passo 2: criar conteúdo inicial
  - echo "# Meu Portfólio" > README.md
  - mkdir docs
  - echo "Notas do projeto" > docs/NOTAS.md
  - git add README.md docs/NOTAS.md
  - git commit -m "Estrutura inicial: README e notas"

- Passo 3: criar um repositório no GitHub (semμού)  
  - Acesse GitHub → New repository → Nome: portfolio-primeiro-projeto
  - Não crie README ou .gitignore ainda (você já tem local)
  - Copie a URL do repositório (ex.: https://github.com/seu-usuario/portfolio-primeiro-projeto.git)

- Passo 4: conectar o remoto e enviar
  - git remote add origin https://github.com/seu-usuario/portfolio-primeiro-projeto.git
  - git branch -M main
  - git push -u origin main

Observação: se o GitHub exigir duas etapas de autenticação, use HTTPS com token ou configure SSH (recomendado para fluidez).

3) Mantendo o repositório limpo: .gitignore e licença
Exercício B: adicionar ignored, licença e README completo

- Passo 1: criar .gitignore (ex.: ignore node_modules, logs)
  - cat > .gitignore << 'EOF'
  - node_modules/
  - logs/
  - dist/
  - .DS_Store
  - EOF
  - git add .gitignore
  - git commit -m "Add .gitignore"

- Passo 2: adicionar licença (opcional, recomendado)
  - echo "MIT License" > LICENSE
  - git add LICENSE
  - git commit -m "Add MIT license"

- Passo 3: melhorar README (seções usuais)
  - edite README.md com: descrição, como instalar, como usar, exemplos, como contribuir
  - git add README.md
  - git commit -m "Atualiza README com seções iniciais"

4) Fluxo de trabalho com branches: features, tags e pull requests (PRs)
Exercício C: usar branches para uma feature

- Passo 1: criar uma branch de feature
  - git checkout -b feature-estrutura-pastas

- Passo 2: adicionar conteúdo da feature
  - mkdir src
  - echo "console.log('Olá, mundo!');" > src/index.js
  - git add src
  - git commit -m "Adiciona estrutura de pastas e index.js"

- Passo 3: abrir PR/merge (local)
  - git checkout main
  - git merge --no-ff feature-estrutura-pastas -m "Merge feature-estrutura-pastas"
  - git push origin main

Dicas:
- Use git branch -M main para manter o nome principal como main (em vez de master).
- Enquadre commits com mensagens descritivas: "feat: adiciona index.js" ou "docs: atualiza README".

5) Sincronização com o GitHub quando há colaboração (forks, PRs)
Exercício D: sincronizar fork com upstream

- Suponha que você tenha um fork: você quer manter seu fork atualizado com o repositório original.
- Passos:
  - git remote add upstream https://github.com/original-owner/projeto.git
  - git fetch upstream
  - git checkout main
  - git merge --ff-only upstream/main
  - git push origin main

Se você estiver trabalhando sozinho, esse passo é útil para praticar entendimento de upstream.

6) Resolução de conflitos (quando houver)
Exercício E: simulação de conflito simples

- Passo 1: em uma branch, edite README.md para adicionar uma linha:
  - Em branch main: adicione "Versão inicial"
  - Em branch feature-conflito: adicione "Conteúdo da feature"

- Passo 2: faça commit em cada branch
  - Em main: git add README.md; git commit -m "main: adiciona versão inicial"
  - Em feature-conflito: git add README.md; git commit -m "feature: adiciona conteúdo da feature"

- Passo 3: tente merge na branch main
  - git checkout main
  - git merge feature-conflito
  - O Git mostrará conflito. Edite README.md para resolver, depois:
  - git add README.md
  - git commit -m "Resolves merge conflict entre main e feature-conflito"

7) Tags, releases e versionamento
Exercício F: tags para versões

- Passo 1: após uma entrega está estável, crie uma tag
  - git tag -a v0.1.0 -m "Versão inicial do portfolio"
- Passo 2: empurre a tag para o GitHub
  - git push origin v0.1.0
- Passo 3: se estiver usando releases no GitHub, crie uma Release apontando para essa tag via interface web.

8) Integração de CI simples (opcional)
Exercício G: configuração básica de GitHub Actions

- Crie .github/workflows/ci.yml com um fluxo simples:
  - name: CI
  - on: [push, pull_request]
  - jobs:
    - build:
      - runs-on: ubuntu-latest
      - steps:
        - uses: actions/checkout@v3
        - name: Setup Node.js
          uses: actions/setup-node@v4
          with:
            node-version: '16'
        - name: Install
          run: npm ci || echo "Sem package.json ainda"
        - name: Test
          run: npm test || echo "Nenhum teste definido"

Observação: adapte para a sua stack (Python, Go, etc.).

9) Boas práticas para o portfólio
- Estruture o repositório com uma pasta clara de exercícios, por exemplo:
  - exercises/
    - 01-setup/
      - README.md
      - solution/
    - 02-branching/
      - README.md
      - solution/
- Inclua um README no nível raiz com:
  - Objetivo do repositório
  - Como navegar pelos exercícios
  - Como contribuir (se houver)
  - Como rodar testes/build locally
- Use um LICENSE clara (MIT, Apache-2.0, etc.)
- Mensure apenas mudanças relevantes nos commits (evite "workspace changes" desnecessários).

10) Sessão prática sugerida (um dia de prática)
- Dia 1: crie o repositório local, conecte ao GitHub, publique.
- Dia 2: adicione uma nova feature via branch, faça merge em main.
- Dia 3: crie um README completo, .gitignore adequado, LICENSE.
- Dia 4: pratique resolução de conflitos com uma pequena alteração concorrente.
- Dia 5: configure uma workflow simples de CI (opcional, para aprender).
- Dia 6: crie uma tag de versão e publique uma Release no GitHub.
- Dia 7: crie uma nota de portfólio explicando o que foi aprendido, com links para commits importantes.

11) Modelos de notas que você pode colocar no seu repositório
- Anotações de comandos:
  - Git basics:
    - git init, git add, git commit, git status
  - Branching:
    - git checkout -b nome-da-branch, git merge, git branch
  - Remotos:
    - git remote add origin URL, git pull, git push
  - Resolução de conflitos:
    - editar arquivo, git add, git commit
- Exercícios resolvidos (com trechos de código/conteúdo gerado)
- Referências rápidas:
  - Fluxo recomendado: main -> feature-branch -> PR -> merge -> sync

12) Quer adaptar este desafio ao seu objetivo?
- Diga-me:
  - Seu sistema operacional (Windows/macOS/Linux)
  - Linguagem/stack da prática (JavaScript, Python, Go, etc.)
  - Se você já tem um repositório existente (nome, tipo de conteúdo)
  - Se deseja usar SSH ao invés de HTTPS
- Eu adapto o guia com comandos específicos, scripts de automação e um modelo de README pronto para você publicar no seu portfólio.
