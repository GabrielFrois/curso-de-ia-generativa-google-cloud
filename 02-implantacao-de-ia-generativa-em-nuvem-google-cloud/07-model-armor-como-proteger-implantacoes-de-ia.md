# Model Armor: Como Proteger Implantações de IA

---

## Sobre o Model Armor

### Model Armor
O Model Armor não é apenas uma ferramenta isolada, mas sim um sistema abrangente composto por diversos componentes integrados. 
O objetivo central é garantir a segurança da Inteligência Artificial, mantendo o controle total sobre as operações e comportamentos do modelo.

O sistema atua fundamentalmente como um filtro bidirecional configurável, inspecionando o fluxo de dados em duas frentes: os comandos recebidos (entradas) e as respostas geradas pelo modelo (saídas).

### Mecanismos de Proteção e Filtragem
A principal função da ferramenta é verificar o tráfego de dados e sinalizar ou bloquear atividades suspeitas de acordo com as configurações estabelecidas. As principais ameaças detectadas incluem:
- Violações das diretrizes de IA Responsável.
- Injeções de comandos (prompt injections).
- Tentativas de contornar restrições (jailbreaks).
- Presença de URLs maliciosas.

### Exemplos Práticos de Atuação
A transcrição ilustra o funcionamento do sistema através de dois cenários de proteção:

#### 1. Proteção na Entrada (Identificação de URLs Maliciosas)
Quando um usuário insere um link suspeito em um comando (por exemplo, um site de phishing), o Model Armor intercepta a mensagem antes que ela alcance o modelo de IA. O sistema verifica a URL utilizando grandes bancos de dados de sites maliciosos e fontes de inteligência contra ameaças. Ao confirmar o risco, a entrada é imediatamente bloqueada.

#### 2. Proteção na Saída (Prevenção de Vazamento de Dados)
A verificação das respostas geradas pelo modelo é crucial, pois a IA pode cometer erros ou expor dados sensíveis sem intenção maliciosa.
- **Cenário:** Ao solicitar o resumo de um pedido, o modelo pode incluir indevidamente o número completo de um cartão de crédito, acreditando ser uma informação útil.
- **Ação do Sistema:** O Model Armor detecta a presença da informação sensível (PII). Com base nas configurações previamente estabelecidas, é possível instruir o sistema a mascarar o dado automaticamente (por exemplo, substituindo a maior parte dos números por "X" e exibindo apenas os quatro últimos dígitos) antes de apresentar a resposta final.

---

## Riscos de segurança de LLMs

### As Principais Vulnerabilidades de LLMs
A segurança de Grandes Modelos de Linguagem (LLMs) tornou-se uma prioridade no desenvolvimento de software.
Para mapear e combater os riscos mais críticos dessa tecnologia, a indústria baseia-se em classificações padronizadas, sendo a mais notória delas a lista das 10 principais vulnerabilidades de LLM.

Esse mapeamento oficial é desenvolvido pela fundação OWASP (Open Worldwide Application Security Project), uma organização composta por especialistas globais dedicada à melhoria contínua da segurança de softwares.

Neste contexto, o texto apresenta a ferramenta Model Armor, uma solução tecnológica focada em eliminar diretamente quatro das principais ameaças listadas pela OWASP.

### As 4 Ameaças Mitigadas pelo Model Armor
Abaixo, detalha-se cada um dos quatro riscos abordados e como a ferramenta atua para neutralizá-los na arquitetura do sistema:

#### 1. Arquivos Maliciosos e URLs Não Seguros
- **O Risco:** Agentes mal-intencionados podem tentar sequestrar o LLM inserindo links perigosos diretamente nos comandos (prompts), já que os modelos tendem a seguir essas URLs sem questionar a intenção. Além de links diretos, documentos (como PDFs) podem ser manipulados para atuar como "cavalos de Troia", ocultando códigos maliciosos.
- **A Solução (Model Armor):** O sistema aplica uma detecção automatizada de URLs perigosas e realiza a filtragem rigorosa de arquivos PDF. Isso garante a identificação e o bloqueio automático dessas ameaças camufladas antes que o modelo as processe.

#### 2. Injeção de Comandos (Prompt Injection) e Jailbreaks
- **O Risco:** Trata-se da utilização de métodos criativos de engenharia de prompt projetados especificamente para enganar o modelo, burlar suas proteções nativas e manipular o seu comportamento para fins ilícitos.
- **A Solução (Model Armor):** A ferramenta possui mecanismos de detecção criados exclusivamente para reconhecer e bloquear essas táticas manipulativas, impedindo que os invasores contornem as barreiras de segurança do sistema.

#### 3. Vazamento de Dados Sensíveis
- **O Risco:** Assim como fraudes com cartões de crédito causam grandes transtornos no mundo físico, a exposição de Informações de Identificação Pessoal (PII) e dados confidenciais por um LLM representa uma quebra crítica de segurança e privacidade.
- **A Solução (Model Armor):** Para evitar vazamentos, o sistema integra a técnica de Prevenção contra Perda de Dados (DLP) focada em Proteção de Dados Sensíveis. A ferramenta utiliza "tipos de informações" predefinidos (infoTypes) criados para rastrear, localizar e transformar dados sigilosos automaticamente, garantindo que informações privadas permaneçam inacessíveis a terceiros.

#### 4. Geração de Material Ofensivo
- **O Risco:** A geração e exibição de conteúdo inadequado, tóxico ou abusivo pode causar danos irreparáveis à reputação de uma organização. Um modelo corporativo não pode ser vulnerável a sequestros que o forcem a gerar respostas desagradáveis.
- **A Solução (Model Armor):** Através da implementação de filtros de segurança robustos baseados nas diretrizes de IA Responsável, o sistema estabelece limites estritos. Essa configuração garante um controle total sobre o fluxo de informações, impedindo a entrada de comandos inadequados e a saída de qualquer material considerado nocivo.

---

## Sobre a Personalização

### A Necessidade de Segurança Sob Medida
No contexto de segurança para Grandes Modelos de Linguagem (LLMs), a abordagem genérica de "tamanho único" é considerada ineficaz e ilusória. 
Organizações possuem requisitos de proteção altamente específicos, complexos e peculiares, o que torna as soluções prontas de mercado inadequadas para operações críticas de alto nível.

Para resolver esse problema, o Model Armor foi projetado com uma arquitetura totalmente flexível. O sistema permite o ajuste e a customização completa do serviço para atender às demandas exclusivas de cada empresa, atuando como uma barreira de segurança feita estritamente sob medida para a Inteligência Artificial.

### Os Dois Pilares da Personalização
O alto nível de controle e proteção do serviço é viabilizado por meio de dois recursos arquiteturais principais:

### 1. Configurações Mínimas (A Base da Segurança)
- **O Conceito:** Representa a fundação inegociável do sistema de proteção.
- **A Função:** Estabelece os requisitos de segurança básicos (o "piso" de proteção). Qualquer configuração customizada criada na plataforma é obrigada a atender a esses parâmetros mínimos. Isso garante que a flexibilidade oferecida ao usuário jamais comprometa as diretrizes vitais de segurança da infraestrutura.

### 2. Modelo (O Painel de Controle)
- **O Conceito:** Atua como a central de comando operacional da ferramenta.
- **A Função:** Permite a realização do ajuste fino e exato dos parâmetros de inspeção. É através do recurso de "Modelo" que os administradores definem as regras rigorosas sobre como o Model Armor deve monitorar, examinar e filtrar os comandos recebidos (entradas) e as respostas geradas (saídas) pelo LLM.

---

## Configurações Mínimas

### A Fundação da Segurança
No processo de personalização do Model Armor, o primeiro e mais importante passo é o estabelecimento das Configurações Mínimas. Elas representam os requisitos de segurança básicos e inegociáveis que todos os modelos (templates) do sistema devem obrigatoriamente seguir.

O objetivo estrutural dessa etapa é garantir uma proteção consistente em todas as aplicações de Inteligência Artificial, criando um ponto de partida absoluto e unificado para as equipes de segurança cibernética.

### A Regra de Implementação (A Ordem de Configuração)
A regra de ouro na arquitetura do Model Armor estabelece que as configurações mínimas devem ser criadas antes da definição de qualquer modelo. 
Elas funcionam como o alicerce de uma construção: ao estabelecer essa fundação primeiro, assegura-se que os modelos implementados posteriormente herdarão automaticamente e respeitarão as diretrizes básicas do ambiente.

### Os Três Níveis de Hierarquia
A plataforma oferece a flexibilidade de definir essas configurações em três níveis distintos da hierarquia de recursos do Google Cloud, podendo ser aplicadas via Console ou via API:
1. **Nível da Organização:**
  - Aplica os requisitos básicos a todos os modelos associados a qualquer pasta ou projeto dentro de toda a empresa. É o nível de alcance mais amplo.
2. **Nível da Pasta:**
  - Aplica a exigência mínima de segurança a todos os modelos vinculados aos projetos contidos exclusivamente dentro de uma pasta específica.
3. **Nível do Projeto:**
  - Restringe a regra básica apenas aos modelos associados àquele projeto individual.

### Considerações Estratégicas para o Planejamento
Antes de aplicar as configurações mínimas, a arquitetura de segurança exige a análise de três fatores cruciais:
1. **O Escopo Ideal (Escolha do Nível):**
  - A decisão do nível de aplicação depende da abrangência desejada. O nível da organização é ideal para aplicar regras universais a toda a empresa. Já os níveis de pasta e projeto são indicados para o desenvolvimento de configurações mais restritas e específicas para setores isolados.
2. **A Natureza dos Requisitos:**
  - A definição dos parâmetros exige estratégia. Como as configurações mínimas são a base estrutural e os modelos atuarão como camadas de proteção adicionais sobrepostas a elas, deve-se selecionar com clareza quais regras são verdadeiramente universais.
3. **Exceções e Flexibilidade (Quebra de Herança):**
  - Para projetos ou pastas especiais que demandam maior liberdade operacional, o sistema permite exceções. Um administrador que possua as permissões adequadas pode interromper a herança estrutural do nível superior, o que possibilita a criação de um modelo personalizado ou a desativação completa da obrigatoriedade da configuração mínima para aquele recurso específico.

---

## Proteções e Níveis de Confiança

### Execução de Políticas
As configurações mínimas operam como uma barreira de proteção arquitetural no Model Armor. 
O objetivo primário é impedir a redução dos padrões de segurança do sistema para limites abaixo dos parâmetros aceitáveis, bloqueando alterações feitas de forma acidental ou intencional por desenvolvedores ou engenheiros.

### Bloqueio e Rastreabilidade de Violações
A aplicação dessas regras mínimas ocorre de maneira estrita e automatizada para garantir a integridade da infraestrutura:
- **Bloqueio Ativo:** Caso haja uma tentativa de criar ou atualizar um modelo utilizando um nível de confiança menos rigoroso do que o estabelecido pela regra base, o sistema intervém de forma imediata. A plataforma exibe uma mensagem de erro clara e recusa a consolidação da operação.
- **Auditoria Contínua:** Além do bloqueio preventivo, todas as tentativas de contornar as regras de configuração mínima são capturadas e documentadas na ferramenta de Análise de Registros. Essa rastreabilidade facilita a rápida identificação e correção de anomalias de conformidade pelas equipes de segurança.

### Calibragem de Sensibilidade: Níveis de Confiança
O Model Armor permite o ajuste da sensibilidade analítica do sistema, determinando o grau de certeza necessário antes que uma violação seja sinalizada. A calibragem funciona como um balanceamento técnico para capturar ameaças reais (verdadeiros positivos) sem prejudicar a usabilidade do modelo ao bloquear conteúdos inofensivos (falsos positivos).

O sistema classifica as opções de sensibilidade em três categorias de rigor:
- **Baixo e acima (Alta Sensibilidade):** Representa a proteção mais restritiva. O sistema bloqueia ou sinaliza conteúdos ao menor indício de alinhamento com os critérios de detecção estabelecidos, abrangendo praticamente qualquer tipo de anomalia.
- **Médio e acima (Equilíbrio Padrão):** Apresenta uma filtragem mais equilibrada e criteriosa, sendo a configuração inicial recomendada. A sinalização ocorre apenas quando os itens analisados demonstram uma correspondência moderada com os critérios da ameaça.
- **Alto e acima (Alta Precisão):** Exige o grau máximo de certeza do sistema. Os alertas são disparados exclusivamente quando há uma confiança extrema de que as informações processadas correspondem de forma forte e inegável aos critérios de detecção estipulados.

---

## Modelos

### O Papel dos Modelos
No ecossistema do Model Armor, os Modelos (ou Templates) atuam como a camada de proteção especializada e dedicada aos Grandes Modelos de Linguagem (LLMs). 
Enquanto as configurações mínimas estabelecem as regras de base globais, os modelos gerenciam os detalhes críticos da segurança, informando à API exatamente quais anomalias devem ser rastreadas, bloqueadas e registradas como violações.

A criação e a gestão desses modelos podem ser realizadas através da API do Model Armor ou diretamente pela interface do Security Command Center. Estruturalmente, um modelo é dividido em três componentes principais: Informações gerais, Detecções e IA responsável.

### 1. Informações Gerais
Esta é a etapa de identificação e organização do recurso. Para configurar a base do modelo, é necessário preencher os parâmetros fundamentais de infraestrutura:
  - **Template ID e Região:** Definição de um identificador único para o modelo e a seleção da região (data center) onde ele será executado.
  - **Rótulos (Labels):** Permite a adição de marcadores personalizados para facilitar a categorização, o agrupamento e a administração dos modelos em ambientes com múltiplos recursos.

### 2. Detecções
A seção de detecções é onde se configuram as defesas ativas contra ameaças cibernéticas e táticas de manipulação de dados. Ela é subdividida em três categorias de proteção:

#### A. Detecção de URLs Maliciosas
Ao habilitar esta opção, o sistema passa a rastrear e bloquear comandos que contenham links direcionando para sites de phishing, armadilhas de malware ou qualquer outro vetor conhecido de ataque cibernético.

#### B. Injeções de Comando (Prompt Injections) e Jailbreak
Focada em impedir que invasores subvertam as regras originais do LLM. A ativação dessa defesa bloqueia tentativas de inserir comandos maliciosos ou contornar as travas lógicas da inteligência artificial. Ao selecionar esta opção, um campo oculto é revelado para que se defina o "nível de confiança", calibrando a sensibilidade (ou a "intuição") matemática do sistema para flagrar esse tipo de ataque.

#### C. Proteção de Dados Sensíveis (DLP)
Destinada a evitar o vazamento de informações sigilosas inseridas nos comandos ou geradas nas respostas. Apresenta duas modalidades operacionais:
- **Básica:** Utiliza um conjunto predefinido de tipos de informação (infoTypes) capazes de detectar automaticamente números de cartões de crédito, contas financeiras, credenciais de contas de serviço do Google Cloud, chaves de API e senhas expostas em texto simples. Em regiões dos EUA, o filtro também cobre números de Previdência Social e Identificações Fiscais.
- **Avançada:** Oferece configurações de inspeção mais profundas e parametrizáveis, sujeitas a custos operacionais adicionais.

### 3. IA Responsável (RAI)
Esta última seção concentra-se na moderação de conteúdo e na adequação ética do modelo.

O sistema aplica filtros de conteúdo projetados para identificar materiais ofensivos, discursos de ódio, linguagem explícita e assédio. 
Para o funcionamento correto desta camada, é necessário definir um nível de confiança para cada categoria de filtro, estabelecendo o grau de certeza matemática que o sistema deve ter antes de sinalizar o conteúdo como uma violação.

Regra de Hierarquia: É fundamental destacar que o nível de confiança configurado na seção de IA Responsável utiliza as "configurações mínimas" globais como ponto de partida. 
É plenamente possível adotar uma proteção mais rigorosa do que a regra básica, porém, o sistema bloqueará qualquer tentativa de relaxar os filtros para um nível inferior ao mínimo já estabelecido pela arquitetura de segurança da organização.

---

## Sobre a configuração
