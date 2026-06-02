# Implementação do Cloud Load Balancing no Compute Engine

## Laboratório 1: Configurar Balanceadores de Carga de Rede

Visão Geral do Laboratório
O foco deste laboratório é a implementação prática de um Balanceador de Carga de Rede (Network Load Balancer - NLB) de camada 4 (L4) utilizando a interface de linha de comando (gcloud). Diferente de um balanceador L7 (HTTP/HTTPS) que inspeciona o conteúdo da requisição, o NLB L4 opera na camada de transporte, roteando o tráfego exclusivamente com base em dados de rede (endereços IP de origem/destino e portas), oferecendo altíssima performance para distribuição de tráfego TCP/UDP.

Etapas Principais

1. Preparação da Infraestrutura e Ambiente

Contexto Padrão: Definição da região e zona padrão de operação usando gcloud config set, garantindo que todos os recursos criados a seguir residam no mesmo local físico sem a necessidade de declarar esses parâmetros em cada comando subsequente.

2. Provisionamento dos Servidores Web (Back-ends)

Criação em Lote: Criação de três instâncias de máquina virtual (www1, www2, www3) no Compute Engine.

Automação (Startup Script): Utilização do parâmetro --metadata=startup-script para injetar um script bash que atualiza o sistema, instala o servidor web Apache e cria uma página index.html exclusiva para cada VM. Isso garante que a infraestrutura nasça pronta e configurada.

Segurança (Firewall): Criação de uma regra de firewall baseada em tags (network-lb-tag) para permitir a entrada de tráfego externo via TCP na porta 80.

3. Configuração dos Componentes do Balanceador de Carga

IP Estático: Reserva de um endereço IP externo estático (network-lb-ip-1) para ser a "fachada" única do balanceador, garantindo que os clientes acessem sempre o mesmo IP, independentemente de quantas VMs existam no back-end.

Verificação de Integridade (Health Check): Criação de um http-health-check (basic-check). Este é o mecanismo de segurança que monitora constantemente se os servidores Apache estão respondendo; caso um falhe, o balanceador para de enviar tráfego para ele.

4. Construção do Roteamento (Target Pool e Forwarding Rule)

Pool de Destino (Target Pool): Criação de um agrupamento lógico (www-pool) que une a verificação de integridade criada anteriormente às três instâncias de VM. Todas as instâncias neste pool precisam estar na mesma região.

Regra de Encaminhamento (Forwarding Rule): A "cola" final da arquitetura. Uma regra (www-rule) é criada para instruir o Google Cloud a pegar todo o tráfego que chega na porta 80 do endereço IP estático e encaminhá-lo para o Pool de Destino.

5. Validação de Distribuição de Tráfego

Teste de Estresse Simples: Utilização de um loop infinito via shell script (while true; do curl...) batendo no IP do balanceador.

Comprovação: A resposta do terminal alterna aleatoriamente entre as marcações do Apache ("Web Server: www1", "www2", "www3"), comprovando que o tráfego está sendo distribuído de forma equilibrada entre os nós do cluster.

Conceitos Chave Aprendidos

Balanceamento L4 (Camada de Transporte): Roteamento cego ao conteúdo, focado apenas em IP e Porta, ideal para tráfego não-HTTP ou onde a latência mínima absoluta é o requisito principal.

Startup Scripts: A prática fundamental de Infraestrutura como Código (IaC) em nível de sistema operacional, permitindo que VMs se auto-configurem durante o boot.

Target Pools vs. Backend Services: O laboratório utiliza Target Pools, que é o método tradicional para balanceadores de rede de passagem externa no Google Cloud para agrupar instâncias que receberão o tráfego.

Health Checks: A inteligência central que garante a alta disponibilidade, evitando que requisições de usuários sejam enviadas para servidores inativos ou com falha.

---

## Laboratório 2: Configurar Balanceadores de Carga de Aplicativo

Visão Geral do Laboratório
Este laboratório foca na implementação de um Balanceador de Carga de Aplicativo (Application Load Balancer) operando na Camada 7 (L7) do modelo OSI. Diferente do NLB (Camada 4) que roteia tráfego cegamente via IP e porta, o L7 entende o tráfego HTTP/HTTPS. Isso permite roteamento inteligente baseado em conteúdo (URLs, cabeçalhos, rotas de diretório). A infraestrutura L7 no Google Cloud é global, rodando nos Google Front Ends (GFEs), que direcionam o usuário para o grupo de instâncias mais próximo com capacidade disponível.

Etapas Principais

1. Preparação e Contraste Inicial

O laboratório inicia definindo a região/zona padrão e criando três instâncias de VM independentes (como no lab anterior). Essa etapa serve principalmente como base comparativa para demonstrar como o gerenciamento muda drasticamente ao usar a abordagem recomendada para L7 (via MIGs).

2. Infraestrutura Base (Escalabilidade)
Diferente do pool de destino estático do lab anterior, o L7 exige uma fundação escalável:

Modelo de Instância (Instance Template): Criação de um "molde" (lb-backend-template) que define como as VMs devem nascer (máquina e2-medium, Debian, script de inicialização do Apache com SSL habilitado).

Grupo Gerenciado de Instâncias (MIG): Criação do lb-backend-group a partir do modelo, configurado com tamanho fixo de 2 VMs. O MIG é o motor que permite autoescalonamento, auto-recuperação (autohealing) e atualizações em lote.

3. Segurança (Firewall Específico do GCP)

Regra fw-allow-health-check: Liberação de tráfego de entrada na porta 80 exclusivamente para os blocos de IP 130.211.0.0/22 e 35.191.0.0/16. Estes são os IPs oficiais dos sistemas de verificação de integridade do Google Cloud. Se essa regra não existir, o balanceador achará que todos os back-ends estão inativos.

4. A Cadeia de Arquitetura do Balanceador L7 (Front-end ao Back-end)
A criação do L7 exige a montagem de uma cadeia de recursos interligados de trás para frente:

IP Global: Reserva de um endereço IPv4 estático e global (lb-ipv4-1), evidenciando que este balanceador pode atender tráfego mundial, diferentemente do NLB que era regional.

Health Check: Criação do monitoramento básico HTTP.

Serviço de Back-end (Backend Service): O "cérebro" do back-end (web-backend-service). Ele agrupa o Health Check e o MIG, definindo que a comunicação será via HTTP.

Mapa de URL (URL Map): O coração do roteamento L7 (web-map-http). É aqui que as regras de caminho (ex: /video, /imagens) seriam definidas. Neste lab básico, todo o tráfego é roteado para o serviço de back-end padrão.

Proxy de Destino (Target HTTP Proxy): O recurso (http-lb-proxy) que recebe o tráfego do usuário e consulta o Mapa de URL para saber o que fazer.

Regra de Encaminhamento (Forwarding Rule): A "porta de entrada" global (http-content-rule) que amarra o IP público estático, a porta 80 e o Proxy de Destino.

5. Validação

Acessando o IP global pelo navegador, a página retorna "Page served from: lb-backend-group-xxxx", provando que a requisição passou por toda a cadeia (Regra de Encaminhamento > Proxy > Mapa de URL > Serviço de Back-end) até chegar a uma VM específica gerada dinamicamente pelo MIG.

Conceitos Chave Aprendidos

Camada 7 vs. Camada 4: A transição do roteamento baseado apenas em rede (L4) para um roteamento profundo com capacidade de inspecionar pacotes HTTP (L7).

Grupos Gerenciados de Instâncias (MIGs): O padrão ouro para cargas de trabalho de produção no Compute Engine, substituindo a criação manual de VMs por instâncias descartáveis e idênticas nascidas de um Template.

A Anatomia do Load Balancer L7: O Google Cloud divide o balanceador de aplicativo em módulos altamente personalizáveis (Regra de encaminhamento $\rightarrow$ Proxy $\rightarrow$ Mapa de URL $\rightarrow$ Serviço de Back-end), o que permite arquiteturas extremamente complexas (como enviar parte do tráfego para VMs e parte para um bucket no Cloud Storage).

IPs de Health Check do Google: A compreensão obrigatória de que os "probes" de verificação de saúde do GCP vêm de IPs fixos externos e precisam ser liberados no firewall.

---

## Laboratório 3: Usar um Balanceador de Carga de Aplicativo Interno

Visão Geral do Laboratório
Este laboratório foca na criação de um Balanceador de Carga de Aplicativo Interno (ILB). Diferente dos laboratórios de balanceadores externos (onde o tráfego vinha da internet pública), o ILB distribui o tráfego dentro da sua Nuvem Privada Virtual (VPC).
O cenário prático constrói uma arquitetura clássica de duas camadas (Two-Tier Architecture):

Camada Front-end (Pública): Um servidor web que os usuários acessam pela internet.

Camada Back-end (Privada): Um cluster de máquinas que faz o processamento pesado (neste caso, calcular números primos) e não possui acesso direto à internet, garantindo alta segurança.

Etapas Principais

1. Preparação do Back-end Privado (Serviço de Cálculo)

Script de Inicialização (Python): Criação de um servidor web simples em Python (serveprimes.py) que recebe um número e responde True (se for primo) ou False.

Segurança por Design (--no-address): O modelo de instância (primecalc) é criado com a flag --no-address. Isso significa que as VMs de back-end não recebem um endereço IP público. Elas são invisíveis para a internet.

MIG de Back-end: Criação de um Grupo Gerenciado de Instâncias com 3 VMs usando o modelo criado.

Firewall Interno: Abertura da porta 80 apenas para permitir que o balanceador de carga e o health check se comuniquem com essas instâncias.

2. Construção do Balanceador de Carga Interno
Assim como no balanceador externo L7, o ILB é composto por várias partes, mas configuradas para operar internamente:

Health Check: Configurado para testar o caminho de URL /2 (garantindo que o script Python consiga calcular que 2 é primo e retorne o status 200 OK).

Serviço de Back-end: Criado com a flag --load-balancing-scheme internal, o que diz ao Google Cloud que este roteamento não deve ser exposto publicamente.

Regra de Encaminhamento (Forwarding Rule): Associa o serviço a um endereço IP VIP privado (IP estático interno da sua VPC).

3. Teste de Validação em Rede Fechada

Como o ILB não tem IP público, você não pode testá-lo do seu próprio navegador ou do Cloud Shell (que rodam fora da VPC do projeto).

Solução: Criação de uma VM temporária (testinstance) na mesma rede. Via SSH nessa máquina, executa-se comandos curl apontando para o IP interno do balanceador para provar que a distribuição de tráfego entre os back-ends está funcionando corretamente.

4. Construção da Camada Front-end Pública

Script de Front-end: Criação de um segundo script Python (getprimes.py) que gera uma tabela HTML colorida (verde para primos, vermelho para não primos). Este script atua como um cliente interno, fazendo requisições para o IP privado do seu balanceador de carga para obter as respostas.

VM Pública e Firewall Público: Criação da instância de front-end, desta vez com IP público, e uma regra de firewall permitindo o tráfego da internet (0.0.0.0/0) na porta 80.

Resultado Visual: Ao acessar o IP do front-end no navegador, ele exibe a matriz de números, comprovando que a camada pública conseguiu se comunicar com sucesso com a camada privada isolada.

Conceitos Chave Aprendidos

Arquitetura Multi-Tier (N-Tier): A separação de responsabilidades. O Front-end lida com a interface do usuário, e o Back-end (protegido por um ILB) lida com a lógica de negócios e dados. Se a máquina do Front-end for invadida, o atacante não terá acesso direto irrestrito aos servidores de Back-end.

Balanceamento de Carga Interno (ILB): Essencial para microsserviços. Permite que serviços internos conversem entre si usando um IP fixo, sem precisar rastrear quais VMs de back-end estão ligadas, desligadas ou escaladas no momento.

Segurança de Rede (Sem IP Público): O uso prático de instâncias do Compute Engine sem IPs externos, forçando todo o tráfego a fluir por caminhos controlados (VPC e balanceadores de carga).

Uso de IA no Desenvolvimento: O laboratório introduziu o Gemini Code Assist (antigo Duet AI/Cloud Code) no Cloud Shell Editor, demonstrando como a IA generativa pode ser usada para explicar blocos de código desconhecidos durante o provisionamento da infraestrutura.

---

## Laboratório 4: Implementar o Balanceamento de Carga no Compute Engine - Laboratório com Desafio

Visão Geral do Laboratório
Diferente dos laboratórios tutoriais, este é um Laboratório com Desafio (Challenge Lab). Ele atua como uma avaliação final (capstone) projetada para testar a consolidação do conhecimento adquirido nos laboratórios GSP007 (Balanceador L4) e GSP155 (Balanceador L7). Não há instruções passo a passo ou comandos gcloud prontos; o aluno recebe apenas os requisitos de arquitetura e deve construir a infraestrutura de forma autônoma, lidando com a resolução de problemas (troubleshooting) durante o processo.

O cenário simula o papel de um Engenheiro de Nuvem Júnior que precisa provisionar tanto um balanceamento regional rápido (L4) quanto um balanceamento global inteligente (L7) na rede VPC padrão do Google Cloud.

Detalhamento das Tarefas do Desafio

Tarefa 1: Infraestrutura Base (VMs Independentes e Firewall)

Objetivo: Criar a fundação para o balanceador de rede (L4).

Execução: Provisionamento manual de três instâncias separadas (web1, web2, web3) do tipo e2-small rodando Debian 12.

Automação: É exigida a injeção do script de inicialização bash (fornecido no lab) via metadados para instalar o Apache. O aluno deve lembrar de alterar a variável de nome no script para cada máquina correspondente.

Segurança: Criação da regra de firewall www-firewall-network-lb vinculada à tag network-lb-tag para permitir a entrada de tráfego TCP na porta 80.

Tarefa 2: Configuração do Balanceador de Carga de Rede (Camada 4)

Objetivo: Orquestrar o tráfego das três VMs criadas na Tarefa 1 usando roteamento baseado em IP e Porta.

Requisitos:

Reservar um IP externo estático (network-lb-ip-1).

Criar um Pool de Destino (www-pool) e adicionar as instâncias web1, web2 e web3 a ele.

(Conhecimento Implícito): O aluno precisa lembrar de criar a regra de encaminhamento (Forwarding Rule) na porta 80 apontando o IP estático para o Pool de Destino, passo vital que não é explicitamente listado nos requisitos da tabela.

Tarefa 3: Construção do Balanceador de Carga HTTP (Camada 7)

Objetivo: Construir uma infraestrutura escalável, baseada em grupos gerenciados e com roteamento inteligente.

Infraestrutura Escalável:

Criação de um Modelo de Instância (lb-backend-template) do tipo e2-medium com a tag de rede allow-health-check.

Criação de um Grupo Gerenciado de Instâncias (MIG) chamado lb-backend-group baseado no modelo criado.

Firewall Crítico: Criação da regra fw-allow-health-check. O aluno deve aplicar a regra de permitir os blocos de IP 130.211.0.0/22 e 35.191.0.0/16, que representam os servidores de sondagem (probes) do Google Cloud.

A Cadeia de Balanceamento (Arquitetura L7): O aluno precisa construir a "escadaria" de componentes de trás para frente (ou de frente para trás), interligando:

O MIG (criado anteriormente).

A Verificação de Integridade (http-basic-check).

(Conhecimento Implícito): Serviço de Back-end (associando o MIG e o Health Check).

Mapa de URL (web-map-http).

Proxy HTTP de Destino (http-lb-proxy).

IP Externo Global (lb-ipv4-1).

(Conhecimento Implícito): Regra de Encaminhamento Global vinculando o IP, a porta 80 e o Proxy.

Conceitos Chave Consolidados (Avaliação)

L4 vs. L7 na Arquitetura do GCP: A capacidade de distinguir claramente que o balanceador L4 utiliza Target Pools (agrupamento estático de instâncias) enquanto o balanceador L7 utiliza Managed Instance Groups - MIGs (agrupamento dinâmico e escalável via Templates).

Gerenciamento de Regras de Firewall: A compreensão prática de que balanceadores externos simples precisam apenas de regras abertas para a internet, mas balanceadores de aplicativo (e ILBs) exigem regras estritas permitindo a comunicação interna dos IPs de Health Check do próprio Google.

Dependência de Recursos: A validação de que o aluno entende a ordem de criação dos recursos em nuvem (ex: não é possível criar um MIG sem antes criar o Template; não é possível criar o Proxy HTTP sem antes criar o Mapa de URL).

Estratégia para Obter 100% de Pontuação (Prevenção de Erros)

Nomenclatura Exata: Sistemas de pontuação automatizados são sensíveis a erros de digitação (typos). Copie e cole os nomes exatos exigidos (ex: www-firewall-network-lb, lb-backend-template).

Tags de Rede: Na Tarefa 3, esquecer de adicionar a tag allow-health-check no Template de Instância fará com que o MIG nasça sem a permissão de firewall, resultando em instâncias marcadas como não-íntegras (Unhealthy) pelo balanceador.

Paciência no L7: O Google Front End (GFE) pode levar de 3 a 5 minutos para propagar totalmente a configuração global do balanceador HTTP. Testar o IP prematuramente resultará em erros 404 ou 502 temporários. Aguarde o status verde no painel de "Serviços de rede" antes de clicar na validação da tarefa.
