## INF0056B_ES-SI_2026/2 - Engenharia de Software

<div align="center"><b><h1>Atividade Supervisionada U2-A4</b></div>

Matrícula: 202504988   
Nome: Daniel Mendonça Garcia

Matrícula: 202501707  
Nome: Gean Pablo Pereira Camargo  

Matrícula: 202501291  
Nome: Paulo César Ribeiro Soares  

Matrícula: 202501009  
Nome: Pedro Carlos da Conceição Arantes  

---

### **Quinto Produto: Critérios de Aceitação**

#### **Tema do Trabalho:** 
Sistema de Gestão de Voluntariado e Resposta a Desastres Naturais e Emergências Locais - ApoiaRede

#### **Problema:** 
Em emergências e desastres locais, há um descompasso entre a oferta de voluntários e a real demanda nos pontos de apoio, gerando gargalos como excesso de um tipo de doação (ex: roupas) e falta de outros itens essenciais (ex: água ou remédios).

#### **Solução:** 
Uma plataforma Web/Mobile que mapeia necessidades em tempo real por geolocalização, permitindo que abrigos cadastrem suas demandas exatas e voluntários se inscrevam para tarefas específicas ou doações pontuais.

--- 

### **Histórias de Usuário e Critérios de Aceitação**

As histórias de usuário abaixo estruturam os requisitos funcionais prioritários do **ApoiaRede**, seguindo a anatomia ágil focada em papéis específicos, objetivos claros e valor de negócio mensurável. Agora atualizado com os Critérios de Aceitação estruturados na sintaxe BDD / Gherkin (DADO QUE, QUANDO, ENTÃO), eliminando ambiguidades e cobrindo os cenários positivos e de borda conforme os requisitos.

---

#### **HU01: Cadastro e Autenticação de Perfil**
* ***COMO*** Usuário da plataforma,
* ***EU QUERO*** criar uma conta indicando meu perfil (Voluntário ou Coordenador),
* ***PARA QUE*** eu possa assumir compromissos de doação ou gerenciar demandas de forma personalizada e segura.

#### Critérios de Aceitação:
1. **Cenário 1: cadastro válido com seleção de perfil.**

    * ***DADO QUE*** o usuário não autenticado acessa a tela de cadastro e preenche nome, e-mail válido, senha e os dados obrigatórios do perfil escolhido (CPF/telefone para Voluntário; CPF/cargo para Coordenador),
    * ***QUANDO*** ele submete o formulário de criação de conta,
    * ***ENTÃO*** o sistema cria o registro com a senha criptografada, oculta dados pessoais sensíveis da visualização pública e autentica o usuário na sessão. 

2. **Cenário 2: tentativa de cadastro com email existente.**

    * ***DADO QUE*** já existe uma conta ativa associada ao e-mail informado,
    * ***QUANDO*** o usuário tenta concluir o cadastro com esse mesmo e-mail,
    * ***ENTÃO*** o sistema impede a criação duplicada e exibe uma mensagem informando que o e-mail já está em uso.

---

#### **HU02: Cadastro de Pontos de Apoio**
* ***COMO*** Coordenador de Ponto de Apoio,
* ***EU QUERO*** cadastrar pontos de coleta informando endereço, geolocalização exata e capacidade máxima,
* ***PARA QUE*** a comunidade identifique a localização do abrigo e a logística de recebimento seja facilitada.

#### Critérios de Aceitação
1. **Cenário 1: Cadastro de novo ponto de apoio por coordenador autenticado**

    * ***DADO QUE*** o usuário está autenticado com o perfil de Coordenador,
    * ***QUANDO*** ele preenche o formulário informando nome da entidade, CNPJ, endereço completo, coordenadas geográficas (latitude/longitude) e capacidade máxima de atendimento válida,
    * ***ENTÃO*** o sistema registra o Ponto de Apoio com status inicial "Pendente de Moderação" e o vincula ao Coordenador responsável.

2. **Cenário 2: Bloqueio por dados obrigatórios incompletos**

    * ***DADO QUE*** o Coordenador está preenchendo o cadastro de um Ponto de Apoio,
    * ***QUANDO*** ele tenta salvar sem informar as coordenadas de geolocalização ou com capacidade máxima menor ou igual a zero,
    * ***ENTÃO*** o sistema bloqueia a submissão e destaca os campos obrigatórios inválidos.

---

#### **HU03: Validação de Entidades e Abrigos**
* ***COMO*** Moderador do Sistema,
* ***EU QUERO*** analisar e aprovar cadastros de novos Pontos de Apoio,
* ***PARA QUE*** apenas entidades legítimas publiquem demandas e o público fique protegido contra fraudes.

#### Critérios de Aceitação
1. **Cenário 1: Aprovação de Ponto de Apoio legítimo**

    * ***DADO QUE*** o Moderador acessa a fila de Pontos de Apoio com status "Pendente de Moderação"
    * ***QUANDO*** ele valida os dados cadastrais da instituição e seleciona a opção "Aprovar",
    * ***ENTÃO*** o status do Ponto de Apoio muda para "Ativo", o local passa a ser exibido no mapa público e o Coordenador recebe permissão para publicar demandas.

2. **Cenário 2: Rejeição de cadastro suspeito ou inválido**

    * ***DADO QUE*** o Moderador identifica inconsistências ou fraude nos dados de um Ponto de Apoio pendente,
    * ***QUANDO*** ele seleciona "Rejeitar" e registra a justificativa,
    * ***ENTÃO*** o Ponto de Apoio permanece oculto do mapa público e bloqueado para publicação de demandas.

---

#### **HU04: Atribuição de Selo de Verificado**
* ***COMO*** Moderador do Sistema,
* ***EU QUERO*** conceder validação automática a órgãos oficiais e Defesa Civil,
* ***PARA QUE*** abrigos governamentais consigam publicar necessidades sem gargalos burocráticos durante crises agudas.

#### Critérios de Aceitação
1. **Cenário 1: Concessão do Selo de Verificado**

    * ***DADO QUE*** o Moderador está analisando um Ponto de Apoio vinculado a um órgão governamental ou Defesa Civil devidamente comprovado,
    * ***QUANDO*** ele ativa a flag de "Selo de Verificado" durante a validação,
    * ***ENTÃO*** o Ponto de Apoio é aprovado imediatamente com destaque visual de "Órgão Verificado" no mapa público e liberação instantânea para criação de demandas.

---

#### **HU05: Publicação de Demandas em Tempo Real**
* ***COMO*** Coordenador de Ponto de Apoio,
* ***EU QUERO*** publicar e atualizar necessidades de mantimentos categorizadas com nível de urgência,
* ***PARA QUE*** a comunidade saiba exatamente quais são os itens prioritários do dia e evite doações desnecessárias.

#### Critérios de Aceitação
1. **Cenário 1: Publicação de demanda de insumos com sucesso**

    * ***DADO QUE*** o Coordenador gerencia um Ponto de Apoio com status "Ativo",
    * ***QUANDO*** ele cadastra uma nova demanda informando descrição, categoria (Mantimentos, Vestuário, Higiene ou Saúde), unidade de medida, quantidade meta (> 0) e nível de urgência (Normal, Urgente ou Crítica),
    * ***ENTÃO*** o sistema publica a demanda em tempo real no mural do abrigo com progresso inicial em 0% (0 / meta).

2. **Cenário 2: Tentativa de publicação por abrigo não aprovado**

    * ***DADO QUE*** o Ponto de Apoio ainda está com status "Pendente de Moderação",
    * ***QUANDO*** o Coordenador tenta acessar a criação de demandas,
    * ***ENTÃO*** o sistema bloqueia a operação e informa que o abrigo aguarda validação da moderação.

---

#### **HU06: Convocação de Voluntariado Presencial**
* ***COMO*** Coordenador de Ponto de Apoio,
* ***EU QUERO*** abrir chamados para trabalho voluntário presencial especificando funções e horários,
* ***PARA QUE*** o abrigo obtenha mão de obra operacional sem gerar aglomerações desordenadas no local.

#### Critérios de Aceitação
1. **Cenário 1: Criação de chamado para turno presencial**

    * ***DADO QUE*** o Coordenador gerencia um Ponto de Apoio "Ativo",
    * ***QUANDO*** ele cria uma demanda da categoria "Voluntariado" informando a função necessária, data do turno, horário de início, horário de término, número de vagas (meta) e nível de urgência,
    * ***ENTÃO*** o sistema disponibiliza o chamado na listagem pública do abrigo exibindo o total de vagas disponíveis e ocupadas.

---

#### **HU07: Registro de Compromisso de Doação**
* ***COMO*** Voluntário / Doador,
* ***EU QUERO*** registrar um compromisso de doação informando o item e a quantidade que irei entregar,
* ***PARA QUE*** o sistema reserve a cota daquela necessidade e dê transparência ao progresso da arrecadação.

#### Critérios de Aceitação
1. **Cenário 1: Registro válido de compromisso de doação ou turno**

    * ***DADO QUE*** o usuário está autenticado como Voluntário e visualiza uma demanda aberta com cota disponível (progresso < 100%),
    * ***QUANDO*** ele informa uma quantidade válida (menor ou igual ao saldo restante da meta) e a data prevista de entrega/comparecimento,
    * ***ENTÃO*** o sistema registra o compromisso com status "Pendente de Entrega", incrementa a barra de progresso da demanda e exibe o comprovante da reserva ao voluntário.

2. **Cenário 2: Exigência de autenticação no ato do compromisso**

    * ***DADO QUE*** um visitante não autenticado navega pelo mapa público e seleciona uma demanda,
    * ***QUANDO*** ele clica em "Assumir Compromisso" ou "Voluntariar-se",
    * ***ENTÃO*** o sistema redireciona para a tela de login/cadastro antes de efetivar a transação.

---

#### **HU08: Confirmação de Recebimento Físico**
* ***COMO*** Coordenador de Ponto de Apoio,
* ***EU QUERO*** confirmar no sistema o recebimento do item ou a presença do voluntário,
* ***PARA QUE*** o progresso da meta seja atualizado no mapa e o ciclo da doação seja concluído.

#### Critérios de Aceitação
1. **Cenário 1: Baixa manual de entrega ou presença**

    * ***DADO QUE*** o Coordenador visualiza a lista de compromissos com status "Pendente de Entrega" vinculados ao seu Ponto de Apoio,
    * ***QUANDO*** o voluntário comparece ao local e o Coordenador aciona a opção "Confirmar Recebimento / Presença",
    * ***ENTÃO*** o sistema altera o status do compromisso para "Concluído/Entregue" e consolida definitivamente o quantitativo na meta do Ponto de Apoio.

---

#### **HU09: Bloqueio Automático de Metas Atingidas**
* ***COMO*** Doador criterioso,
* ***EU QUERO*** que o sistema impeça novos compromissos em demandas que atingiram 100% da meta,
* ***PARA QUE*** eu não gaste recursos doando itens que o abrigo já possui em excesso.

#### Critérios de Aceitação
1. **Cenário 1: Bloqueio imediato ao atingir 100% da cota**

    * ***DADO QUE*** a soma dos compromissos registrados em uma demanda atinge exatamente 100% da quantidade meta definida,
    * ***QUANDO*** o sistema processa o último compromisso que completou a cota,
    * ***ENTÃO*** o status da demanda muda automaticamente para "Meta Atingida / Bloqueada" e o botão de novos compromissos é desabilitado na interface.

2. **Cenário 2: Tentativa de envio concorrente para demanda já cheia**

    * ***DADO QUE*** uma demanda já atingiu 100% da meta,
    * ***QUANDO*** um segundo voluntário tenta submeter um novo compromisso para essa mesma demanda,
    * ***ENTÃO*** o backend rejeita a requisição e exibe a mensagem "Esta demanda já atingiu 100% da meta de arrecadação".

---

#### **HU10: Filtragem Georreferenciada no Mapa**
* ***COMO*** Voluntário em busca de onde ajudar,
* ***EU QUERO*** filtrar o mapa público por nível de urgência e proximidade geográfica,
* ***PARA QUE*** eu possa direcionar minha ajuda ao local que se encontra em situação mais crítica.

#### Critérios de Aceitação
1. **Cenário 1: Acesso público e filtragem combinada no mapa**

    * ***DADO QUE*** qualquer cidadão (sem necessidade de login) acessa a página inicial do ApoiaRede,
    * ***QUANDO*** ele aplica filtros por raio de proximidade geográfica e/ou nível de urgência (ex: "Crítica"),
    * ***ENTÃO*** o mapa atualiza os marcadores em menos de 3 segundos, exibindo apenas os Pontos de Apoio ativos que atendem aos critérios selecionados e ocultando quaisquer dados pessoais dos coordenadores.

---

### Definition of Done (DoD) global do projeto:

Complementando os Critérios de Aceitação específicos de cada história acima, toda História de Usuário do ApoiaRede só será considerada concluída na Sprint quando atender aos seguintes critérios globais de engenharia:

1. Código-fonte versionado no repositório Git seguindo o workflow GitHub Flow e padrão Conventional Commits.

2. Pull Request revisado e aprovado por pelo menos 1 membro da equipe.

3. Pipeline de CI no GitHub Actions executado com sucesso (build sem erros e testes automatizados passando).

4. Interface responsiva validada em viewport mobile.