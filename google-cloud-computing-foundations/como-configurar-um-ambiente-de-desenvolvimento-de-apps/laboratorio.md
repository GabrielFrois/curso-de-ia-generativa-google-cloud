# Como configurar um ambiente de desenvolvimento de apps no Google Cloud

Visão Geral do Laboratório
Assim como os outros laboratórios com desafio (Challenge Labs), o GSP315 não oferece um tutorial passo a passo, mas sim um cenário de negócios onde você deve aplicar seus conhecimentos de forma autônoma. O cenário foca na criação de uma arquitetura Serverless (Sem Servidor) e Orientada a Eventos (Event-Driven) para um aplicativo de armazenamento de fotos. O objetivo central é orquestrar recursos de armazenamento, mensageria e processamento que reajam automaticamente quando um usuário faz o upload de uma imagem, além de aplicar práticas básicas de segurança e governança.

Etapas Principais e Arquitetura do Desafio

1. A Origem do Evento (Cloud Storage)

Tarefa 1: Criação de um Bucket no Cloud Storage (qwiklabs-gcp-04-85b05d07aa1f-bucket). Este bucket atuará como o ponto de entrada do sistema. É fundamental que ele seja criado na região especificada (us-east1) para evitar latência e garantir a pontuação automática.

2. O Canal de Mensageria (Pub/Sub)

Tarefa 2: Criação de um Tópico do Pub/Sub (topic-memories-235). O Pub/Sub atua como um barramento de mensagens assíncrono. Neste fluxo, ele servirá para receber notificações de sucesso geradas pela função de processamento, permitindo que futuros serviços (não cobertos neste lab) "escutem" esse tópico e tomem outras ações sem sobrecarregar o sistema principal.

3. O Processamento Central (Cloud Run Functions)

Tarefa 3: Este é o coração do laboratório. Você deve criar uma Função do Cloud Run (2ª geração) chamada memories-thumbnail-maker rodando em Node.js.

Gatilho (Trigger): A função não é ativada manualmente, mas sim configurada para "escutar" o Cloud Storage. Sempre que um novo arquivo é criado no bucket da Tarefa 1, o Eventarc (motor de eventos do Google) dispara a função.

Código (index.js e package.json): O código fornecido utiliza a biblioteca sharp para capturar a imagem original, redimensioná-la para 64x64 pixels (uma miniatura), salvá-la novamente no bucket com um novo sufixo no nome, e então disparar uma mensagem de sucesso para o tópico do Pub/Sub da Tarefa 2.

Validação: O teste prático exige que você faça o upload de uma imagem qualquer (como map.jpg) e verifique se a arquitetura reage criando a versão miniatura automaticamente.

4. Governança e Segurança (IAM)

Tarefa 4: Uma simulação real de operações de TI (SecOps). Você deve acessar a aba de IAM (Identity and Access Management) e remover o acesso de um usuário específico (o "engenheiro de nuvem anterior") que detinha o papel de Leitor no projeto. Isso reforça o Princípio do Menor Privilégio e a importância do offboarding seguro.

Conceitos Chave Consolidados (Avaliação)

Arquitetura Orientada a Eventos: A compreensão de que sistemas modernos na nuvem muitas vezes não rodam continuamente. Eles "dormem" até que um evento (como o upload de um arquivo) os acorde, processe a demanda e volte a dormir, gerando extrema economia (billing por milissegundo de uso).

Cloud Run Functions (2ª Geração): A evolução do antigo Cloud Functions. A 2ª geração utiliza a infraestrutura do Cloud Run e do Eventarc por trás dos panos, permitindo maior tempo de execução, instâncias maiores e melhor controle de concorrência.

Gerenciamento de Dependências (Node.js): O uso do arquivo package.json para instruir o servidor do Google sobre quais bibliotecas externas (como o @google-cloud/storage e o sharp) precisam ser baixadas e instaladas antes que o seu código index.js possa ser executado.

IAM e Revogação de Acesso: A capacidade de auditar rapidamente quem tem acesso a um projeto e revogar permissões de usuários que não fazem mais parte da equipe.

Estratégia para Obter 100% de Pontuação (Prevenção de Erros)

Atenção aos Nomes Variáveis: O nome do bucket (qwiklabs-gcp-04-85b05d07aa1f-bucket) é único para a sua sessão específica. Nunca copie o nome do bucket do colega ao lado ou de tutoriais na internet, senão o sistema de validação falhará.

Gatilhos e Permissões: Na 2ª geração de funções, os gatilhos do Storage utilizam o Eventarc. É comum que, ao criar a função, o Console do Google Cloud exiba um prompt pedindo para conceder papéis de conta de serviço (como Eventarc Event Receiver). Você deve aceitar/conceder essas permissões, ou a função nascerá "surda" e não saberá quando um arquivo for inserido no bucket.

Ponto de Entrada (Entry Point): É um erro comum esquecer de alterar o Ponto de Entrada na configuração da função. O código Node.js exporta a função como memories-thumbnail-maker. Se você deixar o padrão (helloWorld ou helloHttp), a implantação falhará porque o contêiner não encontrará a função correta para executar.

Delay de IAM: Se receber erros de "Permissão Recusada" (Permission Denied) logo ao tentar criar a função, aguarde cerca de 1 a 2 minutos. Às vezes, a propagação de novas permissões de Contas de Serviço pelo sistema global do IAM leva alguns segundos a mais.
