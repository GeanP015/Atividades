## INF0056B_ES-SI_2026/2 - Engenharia de Software
### Encontro 21 - Semana 12 - Dia 26/10/2026

<div align="center"><b><h1>Atividade Supervisionada - U5-A3</b></div>

* **Grupo: 3**    
* **Alunos:**  
Daniel Mendonça Garcia  
Gean Pablo Pereira Camargo  
Paulo César Ribeiro  
Pedro Carlos da Conceição  

--- 

## Estudo de Caso - Quarto Produto: Gerência de Configuração do Projeto

### Contextualização do Problema:

#### Tema: Sistema de Gestão de Voluntariado e Resposta a Desastres Naturais e Emergências Locais - ApoiaRede

#### Problema:

Em emergências e desastres locais, há um descompasso entre a oferta de voluntários e a real demanda nos pontos de apoio, gerando gargalos como excesso de um tipo de doação (ex: roupas) e falta de outros itens essenciais (ex: água ou remédios).

#### Solução:

Uma plataforma Web/Mobile que mapeia necessidades em tempo real por geolocalização, permitindo que abrigos cadastrem suas demandas exatas e voluntários se inscrevam para tarefas específicas ou doações pontuais.

---

### 1. Preparação do Ambiente de Desenvolvimento

* **Ferramenta de Controle de Versão (DVCS):** Git (modelo distribuído), hospedado no GitHub, garantindo que cada um dos 4 membros do grupo possua o histórico local completo e trabalhe offline quando necessário.

* **Ambiente de Execução Local:** Utilização do Docker e Docker Compose para orquestração do banco de dados relacional e da aplicação Spring Boot.

* **Arquivo .gitignore:** Configurado no repositório raiz para garantir a segurança e a limpeza do versionamento. Ele ignora explicitamente:

    * Binários e artefatos de compilação (pastas target/, .class, .jar).
    * Arquivos de configuração de IDEs (.idea/, .vscode/, .settings/).
    * Variáveis de ambiente (arquivos .env, senhas de banco de dados e chaves API), atendendo à norma de privacidade e LGPD.

### 2. Estrutura dos Itens de Configuração e Linhas de Base

* **Itens de Configuração (ICs):** Tudo o que compõe o projeto possui identificação unívoca e histórico de alteração rastreável.

    * Código-Fonte: Classes Java (Backend Spring Boot), Controllers, Services e Repositories.
    * Modelos e Documentação: Diagramas PlantUML (.puml) dos Marcos de Engenharia, arquivos de Requisitos (.md) e Histórias de Usuário. 
    * Artefatos de Infraestrutura: Dockerfile, docker-compose.yml e scripts SQL de migração.

* **Linhas de Base (Baselines):** Definidas formalmente a cada entrega/sprint:

    * Baseline_M1: Escopo, Requisitos e Histórias de Usuário aprovados.
    * Baseline_M2: Estratégia de Gerenciamento Scrum.
    * Baseline_M3: Diagramas UML (Casos de Uso, Classes e Sequência).
    * Baseline_M4: Configuração de Ambiente e Repositório GCS.
    * Baselina_M5: Consolidação dos Critério de Aceitação e Testes.

### 3. Estratégia de Branching: GitHub Flow

* **GitHub Flow:** oferece ramificações curtas (feature branches) com integração contínua para a branch principal main, mantendo o repositório sempre pronto para compilação.

* **Política de Concorrência:** Adota-se o modelo Copia-Modifica-Resolve (Copy-Modify-Merge), permitindo trabalho simultâneo nos componentes do backend com resolução explícita de eventuais conflitos de merge.

* **Pull Requests (PRs) e Inspeção:** A branch main é protegida contra commits diretos. Nenhuma alteração entra na linha de base sem a abertura de um Pull Request.

    * O PR deve ser pequeno e focado em um requisito/HU.
    * Exige aprovação de ao menos 1 par da equipe via Code Review.

* **Estrutura de branches:**

```
main (Linha de Produção / Protegida)
  │
  ├──► feature/HU01-autenticacao ─────(PR + Review)─────► Merge na main
  │
  ├──► fix/bug-xxx ─────(PR + Review)─────► Merge na main
  |
  ├──► docs/documentacao-yyy ─────(PR + Review)─────► Merge na main
  |
  ├──► refactor/refatoracao-zzz ─────(PR + Review)─────► Merge na main
  |
  ├──► chore/arquivo-www ─────(PR + Review)─────► Merge na main
  |
  └──► feature/HU08-confirmacao-recebimento ─(PR + Review)──► Merge na main
```

### 4. Padronização de Commits

Para garantir rastreabilidade, geração automática de históricos e comunicação clara entre os desenvolvedores, adotou-se a convenção Conventional Commits:

* **Sintaxe:** `<tipo>(<escopo>): <descrição curta em português>`

* **Prefixos Utilizados:**

    * **feat(demanda):** Adiciona funcionalidade de publicar demandas com nível de urgência (ex: feat(demanda): implementa busca por proximidade).

    * **fix(compromisso):** Corrige bug no cálculo de limite de 100% da meta (ex: fix(compromisso): ajusta excecao ao tentar doar em demanda cheia).

    * **docs(uml):** Atualização de documentação ou diagramas PlantUML.

    * **refactor(usuario):** Reestruturação da classe abstrata de usuário sem alterar funcionalidade externa.

    * **chore(config):** Alterações nos arquivos do Docker, .gitignore ou dependências do Maven/Gradle. 

### 5. Fluxo de Controle de Mudanças

A alteração de requisitos ou regras de negócio no ApoiaRede segue o fluxo formal de GCS ensinado no curso:

* Solicitação de Mudança: Qualquer membro da equipe identifica a necessidade e abre uma Issue no repositório.

* Análise (CCB): O grupo avalia a viabilidade, impacto no escopo da disciplina e dependências de banco de dados.

* Ordem de Modificação (ECO): A alteração é aprovada, associada a uma nova branch feature/ e implementada com Conventional Commits.

* Auditoria e Incorporação: O PR é revisado, testado localmente via Docker e mesclado à main.

### 6. Integração e Entrega Contínuas (CI/CD) com GitHub Actions

Para operacionalizar a governança de entregas descrita na GCS e garantir que a branch principal (main) permaneça sempre estável e compilável, foi escolhida uma esteira de CI/CD (Continuous Integration / Continuous Deployment) automatizada utilizando o GitHub Actions.

#### 6.1. Pipeline de Integração Contínua (CI)

A esteira de CI é disparada automaticamente a cada abertura de Pull Request ou Push direcionado às branches de funcionalidade (feature/*) e à branch main. O fluxo executa as seguintes etapas em um ambiente conteinerizado isolado:

1. **Validação de Mensagens de Commit (Linting):** Execução da validação de regras de Conventional Commits para impedir que mensagens fora do padrão sejam incorporadas à linha de base.

2. **Setup do Ambiente e Dependências:** Resolução do ambiente Java/Spring Boot e cache do Maven/Gradle para otimizar o tempo de execução do pipeline.

3. **Verificação de Compilação e Build:** Compilação do código-fonte backend e checagem de erros de sintaxe ou incompatibilidade de classes.

4. **Execução de Testes Automatizados:** Bateria de testes unitários e de integração (validando regras como o bloqueio automático de metas de doação a 100%). Se qualquer teste falhar, o Pull Request tem o merge bloqueado automaticamente no GitHub.

#### 6.2. Estratégia de Deploy e Mitigação de Riscos (CD)

Alinhado ao fluxo do GitHub Flow, o deploy do ApoiaRede é disparado após o merge aprovado na branch main:

* **Build da Imagem Docker:** A esteira gera automaticamente uma nova imagem Docker da aplicação tagged com a versão/hash do commit.

* **Publicação de Artefato:** Envio do artefato verificado para o registrador de contêineres (GitHub Packages / Docker Hub).

* **Implantação Segura:** Para o contexto da aplicação Web/Mobile, adota-se o uso de Feature Flags ou variáveis de ambiente para ativação de novas funcionalidades sem causar parada no serviço (zero downtime), permitindo rollback imediato para a versão anterior em caso de incidentes em ambiente de testes/homologação.

#### 6.3. Template de Workflow YML:

```
name: ApoiaRede CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do Código
        uses: actions/checkout@v4

      - name: Configurar Java JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: maven

      - name: Compilar e Executar Testes
        run: mvn clean test

      - name: Validar Build da Imagem Docker
        run: docker build -t apoiarede-backend:latest .
```

