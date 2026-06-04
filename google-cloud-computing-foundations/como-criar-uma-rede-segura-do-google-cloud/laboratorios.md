# Como criar uma rede segura do Google Cloud

## Laboratório 1: Como proteger máquinas virtuais usando o Chrome Enterprise Premium

Visão Geral do Laboratório
O objetivo deste laboratório é demonstrar como acessar com segurança servidores Linux (via SSH) e Windows (via RDP) que não possuem endereços IP públicos, eliminando a necessidade de expor suas máquinas à internet ou de configurar VPNs complexas. Isso é feito através do Identity-Aware Proxy (IAP) para encaminhamento TCP.

Em vez de abrir portas na rede pública, o tráfego de administração é encapsulado dentro de requisições HTTPS, e o Google Cloud verifica a identidade do usuário (IAM) antes de permitir que os pacotes de rede cheguem à máquina virtual.
Etapas Principais

1. Preparação da Infraestrutura Isolada

Ativação de API: Habilitação da API Cloud Identity-Aware Proxy.

Criação das VMs Privadas: Provisionamento de duas máquinas (linux-iap e windows-iap). O detalhe crucial aqui é a configuração de rede: o Endereço IPv4 externo é definido como "Nenhum". Elas nascem totalmente isoladas da internet pública.

Criação da VM Cliente: Provisionamento de uma terceira máquina (windows-connectivity). Diferente das outras, esta possui IP público. Ela simula o computador físico de um administrador tentando acessar o ambiente isolado.

2. O Bloqueio Nativo (Prova de Falha)

O laboratório instrui você a tentar conectar nas máquinas isoladas usando os botões nativos de SSH/RDP. Como esperado, a conexão falha, provando que o isolamento de rede está funcionando.

3. A Liberação Segura de Rede (Firewall)

Regra allow-ingress-from-iap: Criação de uma regra de firewall permitindo entrada nas portas 22 (SSH) e 3389 (RDP).

O "Pulo do Gato" (Filtro de Origem): Em vez de permitir qualquer IP (0.0.0.0/0), a regra permite tráfego exclusivamente do bloco 35.235.240.0/20. Este é o range de IPs oficial e fixo da infraestrutura interna do IAP do Google. Todo o tráfego de túnel virá desses IPs.

4. O Controle de Acesso Baseado em Identidade (IAM)

Acesso liberado na rede não significa acesso concedido. No painel de Segurança do IAP, você deve selecionar as VMs privadas e atribuir o papel Usuário de túnel protegido por IAP (iap.tunnelResourceAccessor) para a conta de serviço da máquina cliente e para a sua própria conta de estudante. Isso vincula a rede à identidade.

5. Acesso Prático via Interface Gráfica e CLI

IAP Desktop: Acessando a máquina cliente (windows-connectivity), você utiliza um aplicativo Windows (IAP Desktop) autenticado com sua conta Google para enxergar e conectar diretamente na VM windows-iap com um clique, abstraindo toda a complexidade do túnel.

CLI (gcloud): Ainda na máquina cliente, você utiliza o terminal para acessar a máquina Linux. O comando gcloud compute ssh linux-iap é inteligente o suficiente para detectar a ausência de IP externo e construir o túnel IAP automaticamente.

Encaminhamento de Porta Local: Para provar o conceito de encapsulamento, você usa o comando gcloud compute start-iap-tunnel para mapear a porta 3389 da VM privada para uma porta local (localhost) da máquina cliente, permitindo usar o cliente RDP nativo do Windows apontando para a própria máquina local.

Conceitos Chave Aprendidos

Zero Trust (BeyondCorp): A mudança de paradigma de segurança. Não confiamos em ninguém apenas por estar "dentro da rede". Confiamos no contexto e na identidade criptografada do usuário.

Bloco de IPs do IAP (35.235.240.0/20): Conhecimento obrigatório para engenheiros e arquitetos de rede no GCP. É impossível usar IAP sem abrir o firewall para este intervalo específico.

IAP Tunneling: A capacidade de encapsular protocolos baseados em TCP (como SSH e RDP) dentro do tráfego web seguro (HTTPS/WebSockets).

Substituição de Bastion Hosts: O IAP elimina a necessidade de manter e pagar por máquinas de salto (Jump Boxes / Bastion Hosts) apenas para administrar servidores privados.

Estratégia para Obter 100% de Pontuação (Prevenção de Erros)

Aba Correta no IAP: Ao conceder as permissões no painel do IAP, certifique-se de estar na aba Recursos SSH e TCP. O painel costuma abrir na aba de "Aplicações" (HTTPS), o que causará erro na avaliação se a permissão for dada no lugar errado.

Cuidado com as Contas (IAM): A Tarefa 5 exige que você adicione duas identidades: a conta de serviço da VM e o e-mail do estudante. Pular uma delas fará com que o validador do laboratório bloqueie sua pontuação, pois ele testa o acesso usando ambas.

Porta Local RDP (Tarefa 7): Ao rodar o comando de túnel (--local-host-port=localhost:0), o terminal escolherá uma porta aleatória vazia e a exibirá na tela (ex: Listening on port [38472]). Você deve copiar exatamente essa porta e colá-la no cliente RDP (localhost:38472), caso contrário, a conexão remota falhará.
