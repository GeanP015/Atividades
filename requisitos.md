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

### **Primeiro Produto: Requisitos e suas Fontes**

#### **Tema do Trabalho:** 
Sistema de Gestão de Voluntariado e Resposta a Desastres Naturais e Emergências Locais

#### **Problema:** 
Em emergências e desastres locais, há um descompasso entre a oferta de voluntários e a real demanda nos pontos de apoio, gerando gargalos como excesso de um tipo de doação (ex: roupas) e falta de outros itens essenciais (ex: água ou remédios).

#### **Solução:** 
Uma plataforma Web/Mobile que mapeia necessidades em tempo real por geolocalização, permitindo que abrigos cadastrem suas demandas exatas e voluntários se inscrevam para tarefas específicas ou doações pontuais.

### Requisitos Funcionais

* RF01: O sistema deve permitir o cadastro e autenticação de usuários.

* RF02: A instituição deve poder cadastrar um Ponto de Apoio com nome, endereço, geolocalização e capacidade máxima.

* RF03: O moderador deve aprovar novos Pontos de Apoio. Abrigos governamentais ou pré-validados recebem selo de "Verificado" automaticamente para agilizar.

* RF04: A instituição deve poder publicar e atualizar demandas em tempo real, ditando o que o abrigo precisa hoje.

* RF05: As demandas devem ser categorizadas como: Mantimentos, Vestuário, Higiene, Saúde e Voluntariado.

* RF06: Cada demanda deve possuir um Nível de Urgência (Normal, Urgente, Crítica) para guiar a logística do doador.

* RF07: O sistema deve exibir visualmente o progresso da demanda, encerrando-a quando a meta atingir 100% para evitar excessos.

* RF08: O Voluntário deve poder registrar um "Compromisso de Doação/Ajuda" no sistema, indicando quando irá entregar o item.

* RF09: A instituição deve poder confirmar o recebimento do item, efetivando a baixa no estoque.

* RF10: O sistema deve exibir um mapa público interativo (sem necessidade de login) contendo os Pontos de Apoio.

### Requisitos Não-Funcionais

* RNF01: O sistema deve ser escalável para suportar picos repentinos, como 10.000 acessos simultâneos.

* RNF02: As interfaces, especialmente o carregamento do mapa, devem ser otimizadas para redes instáveis, carregando textos antes de imagens/mapas pesados.

* RNF03: O design deve priorizar a tela do celular, principal meio de acesso de quem está em serviço voluntário e em doação.

* RNF04: A visualização do mapa e demandas deve ser pública. O login só será exigido na hora de confirmar uma doação.

* RNF05: Dados sensíveis (telefone, documento) de doadores e coordenadores não serão expostos publicamente.

### Fontes de Requisitos

1. Comportamento do Doador e Necessidade de Transparência (Fonte: FIFE/Idis, 2026):
Pesquisas recentes indicam que, embora metade da população brasileira realize doações em emergências, o perfil do doador tornou-se mais criterioso, e a falta de transparência é a principal barreira para o engajamento.

   <https://filantropia.ong/informacao/fife-2026-metade-da-populacao-brasileira-realiza-doacoes-em-emergencias-aponta-idis/>  


2. Desafios Logísticos na Ajuda Humanitária (Fonte: Oxfam Brasil):
A literatura sobre ajuda humanitária aponta que a escassez de recursos frente à alta demanda exige extrema eficiência operacional, evitando desperdícios logísticos e garantindo acesso rápido às áreas mais afetadas.

   <https://www.oxfam.org.br/ajuda-humanitaria-conheca-os-principais-desafios-da-solidariedade-2/>  


3. Agilidade da Mobilização Comunitária (Fonte: Voluntariado.org.br, 2026):
A análise da atuação voluntária demonstra que as redes locais agem com maior rapidez do que estruturas institucionais tradicionais, pois os moradores e líderes comunitários conhecem de perto as reais necessidades emergenciais de sua região.

   <https://www.voluntariado.org.br/2026/05/o-papel-do-voluntariado-em-tempos-de.html>  


4. Fragmentação de Informações em Desastres (Estudo de Caso: Enchentes RS 2024 / FundMed):
Durante calamidades de grande escala, como as enchentes no Rio Grande do Sul, as informações sobre pontos de coleta, tipos de doação (roupas vs. sangue vs. dinheiro) e formulários de voluntariado ficam dispersas em longos textos, sites e redes sociais.

   <https://fundmed.org.br/como-ajudar-vitimas-enchentes-rs-voluntariado-doacoes/>  