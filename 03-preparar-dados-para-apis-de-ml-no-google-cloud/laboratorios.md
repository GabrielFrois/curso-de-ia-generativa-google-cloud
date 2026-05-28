# Preparar dados para APIs de ML no Google Cloud

---

## Laboratório 1 - Dataprep: Qwik Start

Visão Geral
O laboratório ensina a utilizar o Dataprep, uma ferramenta de preparação de dados sem servidor (serverless), para importar, limpar, transformar e mesclar conjuntos de dados sem a necessidade de escrever código complexo. O cenário prático utiliza dados reais da Comissão Eleitoral Federal (FEC) dos EUA de 2016.

Fluxo de Trabalho Passo a Passo
1. Preparação do Ambiente
Criação de Bucket: Criação de um bucket no Cloud Storage para servir de base de dados.

Inicialização: Ativação da identidade de serviço do Dataprep e autenticação no painel da Alteryx Designer Cloud.

2. Criação do Projeto e Importação
Flow (Fluxo): Criação de um espaço de trabalho chamado "FEC-2016" para gerenciar o processo.

Importação: Os arquivos brutos (cn-2016.txt e itcont-2016-orig.txt) são importados a partir do Cloud Storage e renomeados para "Candidate Master 2016" e "Campaign Contributions 2016", respectivamente.

3. Transformação de Dados (Candidate Master)
Filtros de Tempo: Seleção e filtragem de registros específicos da column5 (anos de 2015 a 2019).

Tratamento de Incompatibilidades: Ajuste da tipagem da column6 de State para String para resolver erros de dados não correspondentes.

Filtro de Candidatos: Seleção apenas dos candidatos presidenciais (valor "P" na column7).

4. Limpeza e Mesclagem (Join)
Limpeza (Wrangle): Utilização da linguagem Wrangle para remover delimitadores indesejados no arquivo de contribuições.

Junção (Join): Mesclagem dos conjuntos de dados de "Candidatos" e "Contribuições" usando chaves comuns inferidas pelo Dataprep (ID do candidato).

5. Agregação e Resumo
Pivot/Agregação: Criação de uma tabela de resumo contendo:

Soma, média e contagem de contribuições (column16).

Agrupamento por ID do candidato, Nome e Afiliação Partidária.

6. Refinamento Final
Renomeação: Mapeamento de colunas genéricas (column2, column24, etc.) para nomes intuitivos (ex: Candidate_Name, Party_Affiliation).

Formatação: Arredondamento dos valores calculados na coluna Average_Contribution_Sum para uma melhor leitura.

Conceitos Chave Aprendidos
Wrangle: A linguagem de transformação de dados utilizada pelo Dataprep para manipular colunas e linhas.

Transformer View: A interface visual onde o usuário interage com os dados e cria o "Recipe" (Roteiro) de transformação.

Joins: Capacidade de conectar tabelas distintas baseadas em chaves comuns.

Visualização de Perfis: O Dataprep utiliza histogramas e sinalizações de erro para identificar rapidamente a qualidade dos dados antes da execução final.

---

## Laboratório 2 - Dataflow - Qwik Start: Modelos

Visão Geral do Lab
O foco é demonstrar como o Dataflow permite criar pipelines de dados complexos utilizando modelos pré-construídos, evitando a necessidade de escrever código de processamento do zero. O cenário utiliza dados de corridas de táxi em tempo real.

Etapas Principais
1. Preparação do Ambiente
Ativação de API: O laboratório exige a desativação e reativação da API dataflow.googleapis.com para garantir a permissão adequada no ambiente temporário.

Estrutura de Dados (BigQuery):

Criação de um dataset chamado taxirides.

Criação de uma tabela chamada realtime, definindo um esquema específico (ex: ride_id, latitude, longitude, timestamp, etc.) para receber os dados JSON.

Armazenamento (Cloud Storage): Criação de um bucket para armazenar os arquivos de "staging" (arquivos temporários usados pelo Dataflow durante a execução do job).

2. Execução do Pipeline (O Coração do Lab)
O pipeline é executado utilizando o comando gcloud dataflow jobs run, que invoca um template pronto do Google.

Template Utilizado: PubSub_to_BigQuery.

Parâmetros:

Input: Um tópico público do Pub/Sub (projects/pubsub-public-data/topics/taxirides-realtime).

Output: A tabela realtime criada no BigQuery.

Infraestrutura: O job é configurado com a máquina e2-medium.

3. Validação dos Dados
Monitoramento: Após iniciar o job, o status pode ser verificado no console do Dataflow, na seção de "Jobs".

Consulta SQL: Uma vez que o fluxo está ativo, utiliza-se o editor do BigQuery para realizar uma consulta simples (SELECT * FROM...) e confirmar que os dados das corridas de táxi estão sendo gravados corretamente na tabela de destino.

Conceitos Importantes
Pipeline de Streaming: Ao contrário do processamento em lote (batch), o pipeline de streaming processa eventos continuamente, conforme eles chegam ao tópico do Pub/Sub.

Modelos (Templates) do Dataflow: São ferramentas que automatizam a criação de pipelines comuns. O Google oferece uma biblioteca de templates que podem ser parametrizados, economizando tempo de desenvolvimento.

BigQuery Time Partitioning: No laboratório, a tabela é particionada por timestamp, o que é uma prática recomendada para tabelas de grande volume em streaming, melhorando a performance e reduzindo custos em consultas futuras.

Respostas para o Teste de Conhecimento
Google Cloud Dataflow supports batch processing.

Resposta: Verdadeiro (O Dataflow é uma plataforma unificada que suporta tanto processamento em lote quanto em streaming).

Which Dataflow Template used in the lab to run the pipeline?

Resposta: Pub/Sub to BigQuery (Este foi o modelo específico configurado para ler do tópico de táxis e gravar na tabela).

---

Laboratório 3 - Dataflow: Qwik Start - Python

Visão Geral do Lab
O objetivo é realizar o "Hello World" do processamento de dados: o WordCount (contagem de palavras). O laboratório diferencia dois modos de execução: local (DirectRunner) e distribuída (DataflowRunner).

Etapas Principais
1. Preparação do Ambiente
Bucket de Armazenamento: Criação de um bucket multirregional no Cloud Storage. Este é um requisito obrigatório, pois o Dataflow utiliza o Storage como área de preparação (staging) e local temporário (temp) para arquivos de trabalho durante o processamento em escala.

Configuração do SDK: Utilização de um ambiente isolado (container Docker) para instalar o apache-beam[gcp]. Isso garante que as dependências do SDK do Apache Beam e os conectores do Google Cloud estejam configurados corretamente.

2. Execução Local (DirectRunner)
O laboratório demonstra como executar o pipeline diretamente no ambiente local (no Cloud Shell/Container).

Conceito: O DirectRunner é ideal para testes e depuração, pois processa os dados na máquina local, permitindo validar a lógica do código sem custos de infraestrutura de nuvem.

3. Execução Remota (DataflowRunner)
Esta é a parte central do laboratório, onde o pipeline é submetido ao serviço Dataflow.

Diferenciais: Ao definir o --runner DataflowRunner, o Google Cloud provisiona automaticamente os workers (máquinas virtuais, neste caso, instâncias e2-standard-2) necessários para processar o volume de dados, escalando a operação conforme a necessidade.

Parâmetros de Execução: É essencial informar os caminhos de staging e temp no Cloud Storage, além da região e o ID do projeto.

4. Verificação e Monitoramento
Console do Dataflow: Utilização da interface gráfica para acompanhar o ciclo de vida do job (do estado "Em execução" ao "Concluído").

Validação de Saída: Inspeção dos arquivos gerados no bucket do Cloud Storage, confirmando que o pipeline processou o texto de entrada e consolidou as contagens de palavras nos arquivos de resultados.

Conceitos Chave Aprendidos
Apache Beam SDK: O framework de código aberto que permite escrever pipelines de dados agnósticos à plataforma de execução.

Runner: O componente que especifica onde o pipeline será executado. (DirectRunner para local, DataflowRunner para a nuvem).

Gerenciamento de Recursos: O Dataflow automatiza a alocação de instâncias, o gerenciamento de paralelismo e a tolerância a falhas.

Resposta para o Teste de Conhecimento
Dataflow temp_location must be a valid Cloud Storage URL.

Resposta: Verdadeiro. * Explicação: Como o Dataflow é um serviço distribuído, ele precisa que os arquivos temporários estejam em um local compartilhado e acessível por todos os workers em execução. O Google Cloud Storage é o local padrão e necessário para essa orquestração.

---

Laboratório 4 - Serviço Gerenciado para Apache Spark: Qwik Start - Console

Visão Geral do Laboratório
O laboratório foca na automação de tarefas que, tradicionalmente, exigiriam infraestrutura complexa. Através do console do Google Cloud, você realiza o ciclo completo de vida de um cluster de Big Data: criação, submissão de job, verificação de resultados e redimensionamento dinâmico.

Etapas Principais
1. Preparação do Ambiente
Ativação da API: Habilitação da API Cloud Managed Service for Spark.

Permissões IAM: Concessão do papel de Administrador de armazenamento para a conta de serviço do Compute Engine, garantindo que o cluster tenha permissão para ler/gravar dados necessários durante a execução.

2. Criação do Cluster
Configuração: Definição do example-cluster utilizando o tipo Padrão (1 mestre e N workers).

Infraestrutura: Especificação de máquinas série e2-standard-2 com discos persistentes padrão, garantindo um ambiente de teste equilibrado.

Provisionamento: O estado inicial é "Provisionamento" até que o ambiente esteja totalmente configurado como "Em execução".

3. Envio e Monitoramento de Job
Job de Exemplo: Submissão do clássico SparkPi (uma classe Java inclusa nos exemplos do Spark).

Método Monte Carlo: O job calcula o valor de $\pi$ através de um processo estocástico, utilizando a computação paralela dos workers do cluster para aumentar a precisão dos resultados.

Verificação: Acompanhamento do log de saída no console do job, onde é possível visualizar o valor calculado de $\pi$ após a conclusão.

4. Redimensionamento Dinâmico (Scalability)
Atualização: O cluster é editado em tempo real para alterar o número de nós de trabalho (de 2 para 4).

Importância: Isso demonstra a flexibilidade do serviço gerenciado, permitindo aumentar a capacidade computacional sob demanda sem recriar o ambiente.

Conceitos Chave Aprendidos
Serviço Gerenciado: A eliminação da necessidade de gerenciar o overhead operacional de clusters, permitindo foco exclusivo no código e na análise de dados.

Elasticidade: A capacidade de adicionar ou remover workers para otimizar custos e performance conforme o volume da carga de trabalho varia.

Processamento Paralelo: Como o Spark divide uma tarefa pesada (cálculo de $\pi$ com milhares de tarefas) entre diversos workers simultâneos.

Respostas para o Teste de Conhecimento
Which type of Managed Apache Spark job is submitted in the lab?

Resposta: Spark (O laboratório utiliza a classe org.apache.spark.examples.SparkPi).

Managed Apache Spark helps users process, transform and understand vast quantities of data.

Resposta: Verdadeiro (Essa é a definição fundamental de um cluster Spark gerenciado).

---

# Laboratório 5 - Serviço Gerenciado para Apache Spark: Qwik Start - linha de comando

Visão Geral do Laboratório
O GSP104 é a versão focada em automação via CLI (Interface de Linha de Comando) do laboratório anterior. Enquanto a versão via console foca na interface visual, este laboratório ensina como operar o Cloud Dataproc — o serviço gerenciado do Google Cloud para Apache Spark e Hadoop — utilizando apenas comandos gcloud no Cloud Shell. O objetivo central é demonstrar como o uso da linha de comando acelera o provisionamento e o gerenciamento de infraestruturas de Big Data, permitindo que pipelines complexos sejam criados, executados e escalados de forma programática.

Etapas Principais
1. Preparação e Autorização (Configuração de Segurança)
Diferente da versão via console, esta etapa exige uma configuração manual detalhada via terminal:

APIs: Reativação da API dataproc.googleapis.com para assegurar que o ambiente do projeto esteja pronto.

IAM (Permissões): Concessão de papéis críticos (roles/storage.admin e roles/dataproc.worker) para a conta de serviço padrão. Isso é indispensável para que os workers do cluster tenham permissão para interagir com o Cloud Storage (leitura/escrita de dados) e executar tarefas do Dataproc.

Rede: Ativação do "Acesso privado do Google" na sub-rede. Isso garante que os nós do cluster consigam se comunicar com os serviços do Google (como o Storage) sem precisar de endereços IP públicos, seguindo as melhores práticas de segurança.

2. Criação do Cluster
O cluster example-cluster é provisionado usando o comando gcloud dataproc clusters create.

Especificações: Definição precisa do tipo de máquina (e2-standard-4) e do tamanho do disco (500 GB).

Automação: Este comando encapsula toda a complexidade de rede, discos e nós em uma única instrução, exemplificando o conceito de Infrastructure as Code (Infraestrutura como Código).

3. Envio de Jobs
Execução: Utilização do comando gcloud dataproc jobs submit spark.

Sintaxe Crucial: O uso dos dois traços (--) após o comando é o ponto principal aqui: tudo o que vem antes define a configuração do Dataproc (nome do cluster, classe principal, arquivo JAR), e tudo o que vem depois são os argumentos que o seu código Spark (neste caso, o SparkPi para cálculo de $\pi$) deve processar.

4. Atualização Dinâmica (Escalabilidade)
O comando gcloud dataproc clusters update demonstra como escalar o cluster (aumentar ou diminuir o número de workers) em tempo real, sem necessidade de recriar o ambiente ou interromper a disponibilidade dos dados, provando a eficiência da nuvem.

Conceitos Chave Aprendidos
Automação via CLI: A ferramenta gcloud permite que pipelines de dados sejam criados e destruídos programaticamente, essencial para fluxos de trabalho de Big Data em produção.

Segurança e Identidade: A importância de garantir permissões (IAM bindings) adequadas para contas de serviço, evitando falhas de execução no processamento distribuído.

Elasticidade: A capacidade de ajustar o poder computacional (número de nós) conforme a demanda, otimizando tanto o desempenho quanto o custo financeiro.

Teste de Conhecimento
Pergunta: Clusters can be created and scaled quickly with a variety of virtual machine types, disk sizes, and number of nodes.

Resposta: Verdadeiro. (O Dataproc oferece flexibilidade total para ajustar a infraestrutura conforme o tamanho do conjunto de dados e as necessidades específicas do projeto).

---

## Laboratório 6 - API Cloud Natural Language: Qwik Start

Visão Geral
O Processamento de Linguagem Natural (PLN) é a área da ciência da computação que permite que computadores entendam, interpretem e manipulem a linguagem humana. A API Cloud Natural Language disponibiliza modelos de ML pré-treinados que facilitam tarefas complexas de análise textual, como identificar nomes de pessoas, locais, eventos e até mesmo o sentimento por trás de uma frase, tudo via chamadas de API.

Etapas Principais
1. Preparação e Autenticação (Configuração de Segurança)
Para interagir com a API de forma segura, o laboratório guia o usuário pela criação de credenciais de serviço:

Service Account: Criação de uma conta de serviço específica (my-natlang-sa) para atuar como identidade para a API.

Chaves de Acesso: Geração de um arquivo de chave em formato JSON (key.json), que armazena os dados de autenticação.

Variáveis de Ambiente: Definição da variável GOOGLE_APPLICATION_CREDENTIALS, que orienta o SDK do Google Cloud a utilizar essas credenciais para autorizar as solicitações.

2. Análise de Entidades (Entity Analysis)
O coração do laboratório é a execução de uma requisição de análise de entidades:

Entrada: Um snippet de texto contendo nomes, nacionalidades e obras de arte ("Michelangelo Caravaggio...").

Processamento: O comando gcloud ml language analyze-entities envia o texto para os modelos de ML do Google.

Resultado: O serviço retorna um arquivo JSON rico em metadados, contendo:

Entidades: Identificação automática de tipos (PERSON, LOCATION, EVENT).

Metadados: Links da Wikipédia para enriquecer a compreensão do objeto identificado.

Salience: Um índice de "saliência" (0 a 1) que mede o quanto aquela entidade é central para o significado do texto.

Mentions: Onde e como a entidade foi mencionada no texto original.

Conceitos Chave Aprendidos
Identificação de Entidades: A capacidade da API de reconhecer substantivos próprios e classificá-los sem necessidade de treinamento de modelo pelo usuário.

Enriquecimento de Dados: A API não apenas identifica a palavra, mas conecta-a a bases de conhecimento externas (como URLs da Wikipédia), transformando texto bruto em dados estruturados.

Arquitetura de API: O uso de autenticação via conta de serviço e a manipulação de saídas em formato JSON, padrão utilizado em serviços de IA na nuvem.

Por que isso é importante?
Esta tecnologia é a base para ferramentas modernas como:

Chatbots: Que precisam entender quem ou o que o usuário mencionou.

Sistemas de Busca: Que utilizam extração de entidades para indexar conteúdos de forma mais inteligente.

Análise de Mídia: Para monitorar citações de marcas ou personalidades em notícias e redes sociais.

---

## Laboratório 7 - API Speech-to-Text: Qwik Start

Visão Geral do Laboratório
O GSP119 é um laboratório prático introdutório que demonstra como integrar os modelos avançados de inteligência artificial e aprendizado de máquina do Google para o reconhecimento de voz em aplicações de terceiros. A API Cloud Speech-to-Text permite que desenvolvedores enviem arquivos de áudio ou fluxos de voz em tempo real e recebam de volta uma transcrição de texto precisa em mais de 125 idiomas.

O objetivo central deste exercício é aprender a realizar a autenticação segura do serviço usando uma chave de API restrita e efetuar uma chamada de transcrição síncrona baseada em um arquivo de áudio hospedado no Cloud Storage, consumindo o serviço por meio de requisições HTTP REST clássicas (via curl).

Etapas Principais
1. Preparação do Ambiente e Segurança (Chave de API)
Diferente de outros laboratórios que utilizam contas de serviço estruturadas do IAM, este foca no uso de chaves de API para requisições diretas via cliente HTTP:

Geração da Chave: Criação de uma credencial do tipo Chave de API (API Key) no painel de APIs e Serviços.

Princípio do Menor Privilégio: Aplicação de restrições na chave para que ela funcione exclusivamente com a API Cloud Speech-to-Text, impedindo o uso indevido em outros serviços.

Variável de Ambiente: Acesso à máquina virtual Linux provisionada (linux-instance) via SSH para exportar a chave em uma variável local (export API_KEY=...), mascarando o segredo durante as chamadas.

2. Estruturação da Requisição JSON
Montagem do payload (corpo da mensagem) que dita as regras de negócio para os servidores de IA do Google:

Objeto config: Declaração de parâmetros essenciais de processamento. Informa o tipo de codificação do arquivo ("encoding": "FLAC") e a variante de idioma nativa do áudio ("languageCode": "en-US").

Objeto audio: Apontamento direto do recurso de mídia utilizando a URI nativa de um bucket do Cloud Storage (gs://cloud-samples-tests/speech/brooklyn.flac).

3. Execução da Chamada REST e Análise de Resultados
Submissão do pipeline de IA através de uma requisição POST com a ferramenta curl:

Transmissão: Envio do arquivo request.json com os dados binários para o endpoint do método síncrono da API (v1/speech:recognize).

Análise do Retorno (Response): A API processa o áudio e devolve um JSON com duas métricas cruciais de Machine Learning:

transcript: O texto bruto convertido e interpretado pela IA ("how old is the Brooklyn Bridge").

confidence: Um valor estatístico decimal (ex: 0.93) que representa o grau de certeza matemática do modelo em relação à exatidão da transcrição.

Conceitos Chave Aprendidos
Reconhecimento Síncrono vs. Assíncrono: O laboratório introduz o método síncrono (recognize), ideal para arquivos de áudio curtos (menos de 1 minuto) e respostas imediatas.

Consumo de Modelos Pré-treinados: Como usufruir de inteligência artificial de ponta sem a necessidade de coletar dados de voz, treinar redes neurais ou gerenciar servidores de GPU.

Formatação e Codificação: A importância de fornecer metadados técnicos corretos (como o codec FLAC) para que os algoritmos de PLN processem as frequências sonoras perfeitamente.

Casos de Uso na Indústria
O ecossistema explorado neste laboratório serve de fundação para o desenvolvimento de:

Sistemas de legenda automatizada para vídeos em tempo real.

Transcrição e auditoria de chamadas em centrais de atendimento (Call Centers).

Comandos de voz para assistentes virtuais e automação residencial.

---

## Laboratório 8 - Video Intelligence: Qwik Start

Visão Geral do Laboratório
O GSP154 é um laboratório prático de nível introdutório focado no uso da API Cloud Video Intelligence. Essa API permite que desenvolvedores extraiam metadados avançados de arquivos de vídeo de forma assíncrona usando modelos de machine learning pré-treinados do Google, sem a necessidade de criar ou treinar redes neurais do zero.

O objetivo central deste exercício é aprender a configurar a autenticação por meio de uma conta de serviço dedicada e submeter um vídeo público hospedado no Cloud Storage (gs://...) para o recurso de Detecção de Rótulos (Label Detection). Ao final, o aluno compreende como interpretar a resposta JSON da API para identificar quais objetos ou entidades (substantivos) aparecem no vídeo e o tempo exato de suas aparições.

Etapas Principais
1. Configuração e Autorização (IAM)
Antes de fazer chamadas à API, o laboratório estabelece o contexto de segurança no Cloud Shell:

Criação da Service Account: É gerada uma conta de serviço personalizada chamada quickstart.

Geração da Chave JSON: É exportada uma chave de autenticação privada (key.json) atrelada a essa conta.

Ativação e Token: A conta de serviço é ativada no ambiente do terminal (gcloud auth activate-service-account), e é gerado um token de acesso temporário (gcloud auth print-access-token) que será injetado no cabeçalho das requisições HTTP (Authorization: Bearer).

2. Criação da Solicitação de Anotação (Payload JSON)
Montagem do arquivo de configuração request.json que define o escopo do processamento:

inputUri: Aponta para o arquivo de mídia bruta no Cloud Storage (gs://spls/gsp154/video/train.mp4, um vídeo curto de um trem).

features: Define quais inteligências serão aplicadas ao vídeo. Neste caso, utiliza-se a LABEL_DETECTION (detecção de rótulos/objetos).

3. Execução Assíncrona e Monitoramento da Operação
Como o processamento de vídeos exige alto poder computacional e tempo, a API Video Intelligence trabalha com operações assíncronas:

Primeiro Envio: O comando curl faz um POST para o endpoint videos:annotate. A API não devolve o resultado imediatamente; ela responde com um ID de Operação (ex: projects/.../operations/...).

Checagem de Status (Polling): O usuário executa um segundo comando curl apontando para o endpoint da operação específica para checar o progresso. Inicialmente, o JSON de resposta mostra o percentual de progresso.

Resultado Final: Quando o processamento atinge 100%, a flag "done": true é retornada, revelando o bloco annotationResults.

Conceitos Chave Aprendidos
Operações Assíncronas: Padrão arquitetural essencial para serviços de IA que lidam com arquivos pesados (vídeos/áudios longos), onde a requisição retorna um "recibo" (ID da operação) para que o cliente consulte o status depois.

Detecção de Rótulos (Label Detection): Capacidade da IA de assistir ao vídeo quadro a quadro, reconhecer objetos (como um trem ou trilhos), associar um ID de entidade global (entityId) e calcular a precisão matemática (confidence) daquela detecção.

Offsets de Tempo (startTimeOffset / endTimeOffset): Segmentação temporal que diz exatamente em qual segundo o objeto entra e sai da cena.

Casos de Uso na Indústria
O ecossistema explorado neste laboratório serve de fundação para soluções reais como:

Sistemas de Busca de Mídia: Motores de busca internos para plataformas de streaming (ex: encontrar todas as cenas de um catálogo onde aparece um "carro").

Moderação de Conteúdo: Varredura automática de vídeos enviados por usuários para detectar conteúdos explícitos ou logotipos protegidos por direitos autorais.

Geração de Tags para SEO: Criação automática de palavras-chave baseadas no conteúdo visual do vídeo para melhorar a indexação na web.

---

## Laboratório 9 - Preparação de dados para APIs de ML no Google Cloud

Visão Geral do Laboratório
Os Laboratórios com Desafio (Challenge Labs) são avaliações práticas projetadas para consolidar e validar as habilidades adquiridas ao longo de uma trilha de aprendizado — neste caso, o selo de engenharia de dados e machine learning. Diferente dos laboratórios tradicionais, o GSP323 não fornece instruções passo a passo ou comandos para copiar e colar. Em vez disso, ele apresenta um cenário de negócios real na empresa fictícia Jooli Inc., onde você deve configurar de forma autônoma pipelines de dados (em lote e distribuídos) e consumir APIs de Inteligência Artificial, provando sua capacidade de arquitetar soluções integradas no Google Cloud.

Detalhamento das Tarefas do Desafio
Tarefa 1: Ingestão de Dados em Lote com Dataflow
O objetivo é criar um pipeline ETL (Extração, Transformação e Carregamento) sem servidor para mover dados brutos do Cloud Storage para o BigQuery.

Preparação Obrigatória: Antes de rodar o pipeline, você deve criar manualmente a estrutura de destino: um Dataset no BigQuery e um Bucket no Cloud Storage.

O Pipeline: Utiliza-se o modelo nativo do Dataflow (Cloud Storage Text Files to BigQuery).

Transformação (UDF): O job aplica uma função JavaScript definida pelo usuário (UDF) hospedada em gs://spls/gsp323/lab.js para transformar os dados antes de salvá-los.

Infraestrutura: É necessário desmarcar o padrão e fixar as instâncias como e2-standard-2 para controlar o custo e escopo do processamento.

Tarefa 2: Processamento Distribuído com Managed Service for Spark (Dataproc)
Validação de habilidades na orquestração de algoritmos complexos de Big Data em clusters gerenciados.

Preparação no HDFS: Antes do envio do job, você deve se conectar via SSH a um nó do cluster e usar comandos de terminal para copiar o arquivo do Cloud Storage diretamente para o sistema de arquivos nativo do Hadoop (hdfs dfs -cp gs://... /data.txt).

Configuração do Cluster: O cluster deve ser instanciado usando a série de máquinas E2 (e2-standard-2) com discos permanentes equilibrados de 100 GB e a rede configurada para permitir IPs externos (desmarcar apenas IP interno).

O Job: Submissão de um job do tipo Spark executando o algoritmo SparkPageRank, passando o arquivo do HDFS como argumento.

Tarefa 3: Análise de Áudio com a API Cloud Speech-to-Text
Conversão de voz em texto utilizando os modelos de Deep Learning do Google.

Execução: Processar de forma síncrona ou assíncrona o arquivo de áudio brooklyn.flac (ou o especificado task3.flac).

Entrega do Artefato: O JSON resultante da transcrição deve ser salvo e enviado para o bucket especificado no campo Cloud Speech Location.

Regra de Validação: O cabeçalho de metadados (Content-Type) do arquivo no Cloud Storage deve ser explicitamente definido como application/json, caso contrário, o validador automático falhará.

Tarefa 4: Extração de Conhecimento com a API Cloud Natural Language
Uso de Processamento de Linguagem Natural (PLN) para analisar textos não estruturados.

Execução: Submeter o trecho de texto fornecido sobre a mitologia de Odin para o endpoint de análise de entidades (analyze-entities).

Entrega do Artefato: Salvar a resposta JSON (contendo a classificação de pessoas, locais e objetos, bem como o índice de relevância/salience) e fazer o upload do arquivo para o caminho indicado em Cloud Natural Language Location, também aplicando o metadado application/json.

Conceitos Fundamentais Consolidados
Arquitetura de Dados Unificada: Como conectar a camada de armazenamento de arquivos brutos (Cloud Storage), processamento distribuído (Spark/Dataproc), computação sem servidor baseada em eventos (Dataflow) e armazenamento analítico (BigQuery).

Segurança e IAM: A verificação inicial reforça o conceito de que contas de serviço padrão (como a do Compute Engine) precisam receber explicitamente papéis como roles/storage.admin para permitir a automação de pipelines.

Consumo de IA Pronta (Pre-trained ML): Demonstração prática de que análises complexas de áudio e texto não exigem que o engenheiro de dados treine modelos, mas sim que saiba estruturar payloads JSON e tratar respostas REST de maneira eficiente.

Estratégia para Obter 100% de Pontuação
Zere a Tarefa 1 por primeiro: Garanta que o esquema da tabela do BigQuery corresponda exatamente ao arquivo .schema fornecido. Aguarde o job do Dataflow mudar para o status "Succeeded" antes de clicar no botão de progresso.

Cuidado com a Sintaxe no Spark: No Dataproc, o argumento /data.txt aponta para a raiz do HDFS. Se esquecer de rodar o comando de cópia via SSH antes, o job falhará imediatamente por falta de arquivo.

Metadados do Cloud Storage: Ao fazer upload dos arquivos result.json das tarefas de IA (Speech e Natural Language), use o console ou o utilitário gcloud/gsutil para garantir que o tipo do arquivo seja application/json, um detalhe técnico sutil que bloqueia muitos estudantes neste desafio.
