# Operações de Machine Learning (MLOps) para IA Generativa

---

## Revisão

- **ML:** Machine Learning - Aprendizado de Máquina
- **LLM:** Grandes Modelos de Linguagem

### Como uma Máquina Aprende?
Geramos uma série de inputs e analisamos os outputs. Em seguida selecionamos as entradas que fazem mais sentido ou que estão mais relacionadas às saídas. E por fim as entradas recebem pesos, que são proporcionais à sua importância para determinada saída.

---

## A Evolução das Operações de ML

### Introdução ao MLOps (Machine Learning Operations)
Treinar e implantar modelos de Machine Learning (ML) tradicionalmente é um processo longo e iterativo. O MLOps surge como a solução para esse problema, fornecendo processos padronizados e infraestrutura tecnológica. 
Ele permite que as organizações construam, implantem e operem sistemas de ML de forma muito mais rápida, confiável e escalável.

### IA Preditiva vs. IA Generativa
Para entender o avanço do MLOps, há uma distinção clara entre dois tipos de Inteligência Artificial:
- **IA Preditiva (Não Generativa):** É focada em resolver problemas específicos e executar tarefas direcionadas (como regressão, classificação e detecção de objetos). Ela não cria novos conteúdos, mas utiliza dados e algoritmos preexistentes para tomar decisões, classificar ou fazer previsões.
- **IA Generativa:** Refere-se a modelos mais sofisticados focados em criar conteúdos novos e originais (como textos, imagens e músicas) de alta qualidade, semelhantes ao que um humano faria. Ela funciona aprendendo os padrões ocultos nos dados fornecidos.

### O Desafio Atual do MLOps
Embora ambos os tipos de IA compartilhem princípios fundamentais, a IA generativa traz um conjunto único de desafios. O objetivo atual das equipes de engenharia é adaptar, 
estender e refinar a infraestrutura e os processos já estabelecidos do MLOps para suportar o crescimento acelerado e o potencial da IA generativa de forma eficaz.

### O Fluxo de Trabalho Tradicional de ML
O ciclo tradicional do Machine Learning pode ser simplificado e dividido em duas etapas principais (Treinamento e Disponibilização/Serviço), que se desdobram em quatro fases distintas:
- **Experimentação:** Uso de dados rotulados e algoritmos de ML.
- **Treinamento:** Operacionalização do modelo.
- **Implantação (Deployment):** Alocação do modelo em um endpoint.
- **Predição (Inferência):** Uso de novos dados e solicitações de previsão através de um pipeline de inferência.

### Aprimoramentos Modernos no MLOps
Devido à natureza volátil dos dados no mundo real, o fluxo de trabalho clássico precisou evoluir. Foram adicionadas novas camadas essenciais ao processo:
- **Avaliação e Monitoramento:** Implementados em todas as fases (tanto no treinamento quanto na implantação) para garantir o bom desempenho contínuo do modelo.
- **Registro de Artefatos:** Melhoria nas práticas da indústria para registrar e organizar componentes, incluindo registros de modelos, repositórios de atributos (features) e mapeamento de pipelines em galerias.
- **Governança:** Manutenção de uma governança consistente de dados e artefatos por todo o ciclo de vida do modelo.

---

## Framework de MLOps para IA Generativa

### Introdução ao MLOps para IA Generativa
O MLOps para IA Generativa é definido como a aplicação dos princípios tradicionais do MLOps para operacionalizar aplicativos geradores de conteúdo. 
Embora a base tradicional de operações de Machine Learning continue essencial, a IA generativa possui características únicas que exigem o refinamento e a adição de novas camadas ao fluxo de trabalho padrão.

### Mudanças no Fluxo de Trabalho Clássico
A transição para a IA generativa altera a forma como lidamos com a criação e a alimentação dos modelos:
- **Experimentação e Descoberta:** A engenharia deixa de focar na construção de modelos do zero e passa a priorizar a descoberta e a utilização de modelos pré-treinados.
- **Atalho de Predição Direta:** Cria-se um caminho mais rápido onde, logo após a fase de descoberta, é possível realizar predições e gerar resultados imediatos usando apenas comandos em linguagem natural (prompts).
- **Personalização e Ajuste (Tuning):** A fase de treinamento é substituída ou complementada pelo ajuste de modelos pré-treinados para adaptá-los a tarefas ou necessidades específicas da organização.
- **Foco em Dados Selecionados:** Em vez de depender de quantidades imensas de dados rotulados, a IA generativa exige conjuntos de dados altamente selecionados (curadoria). Isso força as empresas a reavaliarem a forma como armazenam e estruturam seus dados (data lakes e data warehouses).

### Novas Exigências de Operação e Controle
Para gerenciar esses novos sistemas com segurança e eficiência, o MLOps precisou expandir suas práticas de controle:
- **Governança de Novos Artefatos:** O processo passa a lidar com novos componentes tecnológicos que precisam ser registrados, governados e versionados, como trabalhos de ajuste, camadas adaptativas e incorporações de dados (embeddings).
- **Novas Métricas de Avaliação e Monitoramento:** Métricas clássicas (como acurácia e precisão matemática) não conseguem medir a qualidade de um texto ou imagem gerada. O monitoramento agora exige a avaliação de aspectos subjetivos e críticos, como a fluência do conteúdo, a veracidade das informações geradas e o impacto na reputação da marca.

### Integração de Dados Empresariais
Os modelos de fundação (modelos pré-treinados básicos) são estáticos, pois seu conhecimento é limitado àquilo que aprenderam durante seu treinamento original. 
Para extrair o verdadeiro potencial dessas ferramentas e executar tarefas sofisticadas, é necessário conectá-los a dados externos e atualizados (dados privados da empresa). 
Contudo, adicionar esses dados externos aumenta significativamente a complexidade de avaliação e monitoramento da infraestrutura.

---

## Navegando pela IA Generativa: Entender as Nuances e Ajustar MLOps

### O Desafio da IA Generativa no MLOps
Embora as equipes possam aproveitar a infraestrutura existente de MLOps, a integração eficiente de modelos de IA Generativa (como geração de texto, código e resumos) exige adaptações. 
A tecnologia traz considerações únicas que exigem soluções personalizadas para que todo o seu potencial seja extraído com sucesso.

Esses desafios são divididos em cinco áreas principais e apresenta as soluções do Google Cloud (Vertex AI) para mitigá-los:
- **Desafio 1:** Necessidade de Infraestrutura Robusta
  - Modelos de linguagem grande (LLMs) possuem arquiteturas complexas que exigem recursos computacionais massivos (GPUs e TPUs) para pré-treinamento, experimentação e implantação.
  - **Solução (Model Garden):** O Vertex AI oferece o Model Garden, um catálogo que facilita a descoberta de modelos pré-treinados (do Google, código aberto e de terceiros). Ele permite testar modelos com comandos de texto simples, sem precisar construir pipelines complexos do zero.
  - **Solução (Generative Studio e Vertex Training):** Um ambiente totalmente gerenciado onde o Google cuida da infraestrutura pesada. Permite testar comandos, ajustar modelos de fundação com dados próprios e escalar o treinamento com alta disponibilidade de forma eficiente.
- **Desafio 2:** Personalização e Ajuste de Modelos (Tuning)
  - Modelos genéricos precisam ser refinados para realizar tarefas específicas e domínios de negócios.
  - **Soluções do Vertex AI:**
    - **Ajuste Supervisionado:** Para tarefas que possuem saídas bem definidas e previsíveis.
    - **RLHF (Aprendizado por Reforço com Feedback Humano):** Ideal para tarefas subjetivas, como aplicativos de chat e resumos (disponível para modelos PALM e Llama 2).
    - **Curadoria de Dados:** Ampliação do pré-treinamento genérico com dados específicos do domínio do cliente.
- **Desafio 3:** Gerenciamento de Novos Artefatos
  - A IA generativa introduz novos elementos técnicos que precisam ser orquestrados e governados.
  - **Comandos (Prompts):** O uso de ferramentas como Langchain e Weights & Biases ajuda a depurar e gerenciar a "Engenharia de Comandos".
  - **Embeddings:** Vetores que transformam dados não estruturados (textos, imagens) em representações matemáticas. O Vertex AI Feature Store simplifica o armazenamento e fornecimento desses dados.
  - **Camadas Adaptativas (Adapters):** Pequenos grupos de pesos (megabytes) atualizados sem alterar todo o modelo base. Gerenciados através do Vertex Model Registry.
  - **Trabalhos de Ajuste:** O Vertex AI Pipelines garante a rastreabilidade (linhagem do dado até o modelo) e reprodutibilidade usando frameworks como TensorFlow, PyTorch ou XGBoost.
- **Desafio 4:** Avaliação e Monitoramento de Saídas Não Estruturadas
  - Ao contrário de modelos preditivos, a IA generativa produz textos longos e imagens, tornando métricas tradicionais ineficazes.
  - **Avaliação:** Usa-se pares de "comandos + informações empíricas" (a resposta ideal esperada) para medir fluência, veracidade e reputação da marca. O Vertex AI Evaluation Services automatiza essa verificação.
  - **Monitoramento (Segurança e Plágio):**
    - **Pontuações de Segurança:** O modelo PALM gera automaticamente payloads que avaliam o conteúdo em mais de 10 categorias de segurança, permitindo o bloqueio de conteúdos nocivos.
    - **Verificação de Recitação:** O sistema cruza a saída gerada com artigos da web e repositórios de código para detectar correspondências (plágio), garantindo a originalidade ou citando a fonte.
- **Desafio 5:** Integração com Dados Empresariais
  - Para que os modelos não fiquem limitados ao conhecimento do seu treinamento original e evitem "alucinações" (respostas inventadas), eles precisam acessar os dados privados e atualizados da empresa.
  - **Soluções do Vertex AI:**
    - **Vector Search e Embeddings:** APIs para processar textos e imagens no mesmo espaço vetorial, combinadas a um banco de dados vetorial gerenciado para consultas rápidas.
    - **Embasamento (Grounding):** Capacidade de forçar o modelo (como o Vertex Palm) a gerar respostas baseadas estritamente nos dados reais da empresa.
    - **Vertex Extensions:** Ferramentas que conectam a IA a dados em tempo real e permitem a execução de ações no mundo real.
   
