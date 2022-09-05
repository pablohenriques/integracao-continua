# Alura: Integração Contínua
---

## Problemas
    - Quebra de código durante a sincronização de ramificações com a ramificação principal.
    - Testes que não testam o contexto real da aplicação contruída
    - Etapas de desenvolvimento burocráticas.

## Sistema de Controle de Versão
    - Ferramentas: Git, SVN
    - "Commitar" as configurações necessárias para construção do projeto:
        - código; 
        - scripts (automação de build etc.)
        - migrações e schemas
        - IDE config (plugins etc.)

## Organização dos Repositórios
    - Multi-repo: projetos com contextos específicos e separados em seus repositórios. Quanto maior o número de repositórios, maior a complexidade em mantê-los 
    - Mono-repo: vários projetos em um único repositório, o que torna a administração do projeto. Contudo, builds, clone do projeto e outras ações são mais complexas devido ao tamanho  do projeto. 
    - Mono-repo: refatorações no projeto são refletidas de forma global. 

## Branching models
    - A utilização de ferramentas de versionamento popularizou a criação de ramificações. Para um desenvolvimento organizado são necessárias estratégias para as criação dos branchs.
    Atenção:
        -   Commits simples e lançáveis, orientado a tarefas
        -   Branches de vida curta -> merge mais simples
        -   Estratégias devem ser combinadas pela equipe
        -   * branches atrasam integração, seguram código
        -   * muitos branches, mais burocracia

## Comparando Branches
    -   Temporários (branches locais)
    -   Feature Branches
    -   Historical Branches (Master e Develop)
    -   Environment Branches (Staging e Production)
    -   Maintenance Branches (Release e Hotfix)
    -   Complexidade ferramentas (menor -> maior):
        -   trunked-based
        -   feature branch
        -   github flow
        -   gitlab flow
        -   git flow


## Branch by abstraction
    -   Evitando branches de vida longa:
        -   Feature Flags
            - Configuração que permite testar parte de uma aplicação
        -   Branch by abstraction
            -   Camada de isolamento para desenvolvimento em sistemas legados


# Merge e Rebase
    -   Merge: representa um evento de sincronização entre a branch auxiliar e branch master/main. Não representa alteração, representa junção. A branch main e auxiliar devem ser levadas em considerção no histórico de commits
```
    main-main-main
        -feat-feat
    --------------
    main-main-main-(main/feat)
        -feat-feat
```
    - Rebase: cria um fluxo único de commits, por exemplo, na branch auxiliar obtem os commits da main e adiciona os commits da auxiliar. O rebase reescrve a história dos commits e deve ser feito na branch local e não na branch pública (recomendação)
```
    main-main-main
        -feat-feat
    --------------
    main-main-main
        -main-main-feat-feat
```

## Self testing
    -   Teste automatizado (teste contínuos)
    -   Rodas antes do commit
    -   Desempenho importa
    -   TDD
    -   Unit Tests < Integrations Tests < Functional Tests
        -   Quantidade: maior -> menor
        -   Tempo Execução: menor -> maior
    -   Todo commit deve ser acompanho por teste
    -   Smoke Tests: testa as funcionalidades principais e após a execução desses testes são executados os testes restantes
    -   Testes fazem parte do build
    -   Aplicar boas práticas
    - Feedback

## Build automatizado
    -   Etapas do build
        -   clean
        -   compile
        -   unit tests
        -   static analysis
        -   package software
        -   integrate database
    - não depender de IDE
    - tudo está no repositório
    - build a cada commit
    - usar uma build machine

## Servidor de integração contínua
    -   O servidor de integração (CI Daemon) verifica constantemente as alterações e contrói e testa as modificações

## Build quebrado
    -   A maior prioridade da equipe com o build quebrado é refatorara o build e resolver os erros (hotfix)
