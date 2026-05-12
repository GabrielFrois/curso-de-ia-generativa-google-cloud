# Anotações dos Laboratórios

## Laboratório 1: IA generativa com a Vertex AI: design de comandos

### Sobre o Gemini e seus Modelos
O Gemini é a família de modelos avançados e multimodais do Google DeepMind, capaz de compreender texto, código, imagem, áudio e vídeo. Ele pode ser acessado em aplicativos por meio da API na Vertex AI. O material destaca duas versões:
- **Gemini Pro:** Projetado para tarefas de raciocínio complexo, análise de grandes volumes de informações e solução de problemas avançados (inclusive em programação).
- **Gemini Flash:** Otimizado para velocidade e eficiência. Oferece respostas em menos de um segundo, custos reduzidos, compreensão espacial aprimorada e uso de ferramentas nativas, como a Pesquisa Google.

### Práticas Recomendadas para Criar Comandos
O núcleo do aprendizado foca em técnicas para reduzir a variabilidade das respostas, evitar "alucinações" (informações inventadas) e melhorar a qualidade da saída gerada pelo LLM (Large Language Model):
- **Use textos concisos:** Reduza o ruído e informações desnecessárias para não confundir o modelo.
- **Seja específico e bem definido:** Deixe claro exatamente o formato e a resposta que você espera.
- **Peça uma ação por vez:** Evite agrupar várias solicitações complexas em um único comando.
- **Forneça instruções do sistema:** Defina o papel e as regras que a IA deve seguir (por exemplo, atuar como um "chatbot de viagens") para evitar respostas irrelevantes.
- **Prefira classificação à geração aberta:** Tarefas de geração livre trazem muita variabilidade. Transformar um comando em uma tarefa de classificação (pedir para a IA escolher entre categorias específicas) aumenta a precisão e a segurança da resposta.
- **Inclua exemplos (Few-shot prompting):** Inserir de um a cinco exemplos práticos de perguntas e respostas no comando ajuda o modelo a aprender o padrão esperado. Cuidado com o excesso de exemplos para não causar overfitting (limitar a criatividade do modelo viciando-o nos dados de entrada).

---

## Laboratório 2: Começar a usar o Vertex AI Studio

### 1. Criando e Implantando Aplicativos

A interface principal de chat do Vertex AI Studio é dividida em três partes essenciais:
- **Instruções do sistema:** Regras gerais que definem o papel e o comportamento da IA (ex: agir como um analista de seguros objetivo).
- **Configurações do modelo:** Onde você escolhe o modelo, ajusta parâmetros e define ferramentas adicionais.
- **Comando (Prompt):** A área principal para enviar as instruções e os dados.
- **Implantação Rápida:** O laboratório demonstra que, com apenas alguns cliques, é possível pegar um comando salvo e implantá-lo como um aplicativo da Web funcional (sem servidor) usando o Cloud Run.

### 2. Engenharia de Comandos e Parâmetros

Como refinar comandos para obter respostas mais precisas, com duas técnicas principais:
- **Zero-shot:** Enviar um comando direto sem exemplos prévios.
- **Poucos disparos (Few-shot):** Fornecer exemplos (uma entrada e a saída esperada) no comando para ensinar à IA o formato exato e o padrão de resposta desejado (muito útil para extração estruturada de dados).  
- **Configurações do Modelo (Ajustes Finos):**
  - **Temperatura:** Controla a criatividade. Valores baixos (0.0 a 0.2) geram respostas focadas e factuais. Valores altos (1.5 a 2.0) geram respostas mais criativas e imprevisíveis.
  - **Limite de token de saída:** Define o tamanho máximo da resposta gerada.
  - **Top-P:** Também controla a aleatoriedade, limitando as opções da IA aos tokens mais prováveis.
  - **Orçamento de pensamento:** Define o nível de raciocínio lógico que o modelo deve aplicar antes de responder (útil para tarefas complexas).
  - **Embasamento (Grounding):** Permite conectar a IA à Pesquisa Google ou a bases de dados próprias para evitar alucinações.

### 3. Comparação de Comandos

O Vertex AI Studio possui uma ferramenta chamada Comparar, que permite colocar duas configurações lado a lado para testes A/B. Isso é útil para:
- Avaliar o impacto de pequenas mudanças nas Instruções do Sistema.
- Ver como a variação de Temperatura afeta a mesma entrada.
- Comparar a capacidade de raciocínio de diferentes modelos (ex: modelos padrão vs. modelos Pro) diante de diretrizes complexas.

### 4. Capacidades Multimodais (Gemini)

O laboratório destaca que os modelos Gemini conseguem processar mais do que apenas texto:
- É possível fazer o upload de imagens (como uma tabela de horários de voos) e pedir para a IA descrevê-la, extrair seus textos de forma estruturada ou até mesmo realizar cálculos matemáticos com base nos dados visuais.
- Recomenda-se manter a Temperatura baixa para extração de dados de imagens, garantindo precisão.

### 5. Geração de Mídia (Imagem e Voz)

Além de texto, o Vertex AI Studio conta com ferramentas para criação de outros tipos de mídia:
- **Imagen:** Ferramenta para gerar imagens realistas a partir de descrições em texto. Conta com recursos de edição avançada, como Inpaint (alterar partes específicas) e Outpaint (expandir as bordas da imagem).
- **SynthID:** Tecnologia do Google DeepMind que insere uma marca-d'água digital invisível nas imagens geradas por IA, garantindo a rastreabilidade e transparência, mesmo que a imagem sofra edições.
- **Chirp (Text-to-Speech):** Ferramenta para gerar vozes realistas (IA de voz) a partir de textos, permitindo selecionar diferentes modelos, idiomas e locutores.

---

## Laboratório 3: Introdução à IA generativa do Google usando o SDK da IA generativa

### 1. Interação Básica com o Modelo
A interação com a API do Gemini permite o envio de diferentes tipos de informações para gerar respostas dinâmicas:
- **Comandos de Texto:** Uso do método generate_content para receber respostas em formato de texto.
- **Comandos Multimodais:** O SDK aceita prompts combinados contendo textos, PDFs, imagens, áudios e vídeos (inclusive arquivos passados diretamente via URL/URI).
- **Instruções do Sistema:** Definição prévia do comportamento e da "personalidade" do modelo para que as respostas sigam regras ou formatos estritos.

### 2. Configuração e Controle
O SDK oferece ferramentas para garantir que as saídas da IA sejam seguras, úteis e formatadas corretamente:
- **Parâmetros do Modelo:** Ajustes finos (como temperatura) para controlar a criatividade e o foco da resposta.
- **Filtros de Segurança:** Ajuste das categorias de segurança da API para bloquear a geração de conteúdos indesejados ou nocivos.
- **Saída Controlada:** Permite forçar o modelo a gerar respostas em formatos de dados rigorosos, como JSON ou esquemas baseados em Pydantic/dicionários Python. Útil para extração estruturada de dados de texto.
- **Conversa Multiturno:** Capacidade de criar interações contínuas (chat), onde o modelo lembra do contexto das mensagens anteriores.

### 3. Gerenciamento de Interações e Desempenho
Para aplicações em produção, o laboratório destaca métodos de otimização de tempo e recursos:
- **Streaming de Conteúdo:** Uso de generate_content_stream para exibir a resposta em tempo real, pedaço por pedaço, em vez de aguardar o processamento completo.
- **Solicitações Assíncronas:** Execução de chamadas à API sem bloquear o restante do código da aplicação, usando o módulo client.aio.
- **Contagem de Tokens:** Ferramentas para calcular o tamanho da entrada antes do envio, ajudando no controle de custos e limites técnicos.

### 4. Recursos Avançados
A última etapa foca em técnicas de arquitetura para uso em larga escala da IA:
- **Chamadas de Função (Function Calling):** Permite descrever ferramentas e funções do seu próprio código para o modelo. A IA decide quando "chamar" essas funções e com quais argumentos, automatizando ações.
- **Armazenamento em Cache de Contexto:** Salva em cache grandes blocos de contexto (tokens) que são usados repetidamente, reduzindo custos e acelerando as respostas.
- **Predições em Lote (Batch Prediction):** Envio de milhares de solicitações de uma só vez através de arquivos (JSONL) via Cloud Storage ou BigQuery. É um processamento assíncrono muito mais barato e eficiente do que fazer chamadas individuais em tempo real.
- **Embeddings de Texto:** Capacidade de converter textos em representações vetoriais/numéricas (geralmente com 768 dimensões) para uso em sistemas de busca e comparação de similaridade.

---

## Laboratório 4: Criação de comandos na Vertex AI: laboratório com desafio

### O Cenário Prático
O usuário assume o papel de um profissional em uma startup parceira da Cymbal Direct, uma varejista de equipamentos para atividades ao ar livre. O objetivo é usar o Vertex AI Studio e os modelos Gemini para automatizar a criação de materiais para uma campanha de marketing voltada para a natureza, dividida em duas frentes:
- Descrições de produtos baseadas em imagens.
- Slogans chamativos e personalizados.

### Tarefa 1: Ferramenta de Análise de Imagens (Multimodal)
O objetivo desta etapa é usar a capacidade multimodal do Gemini para analisar imagens de produtos e gerar textos de marketing.
- **Ação:** Criar um comando no Vertex AI Studio fornecendo uma imagem armazenada no Cloud Storage.
- **Testes:** O comando deve ser testado para gerar diferentes saídas, como descrições curtas, frases para anúncios ou textos poéticos focados na natureza.
- **Conclusão:** O comando deve ser salvo com o nome específico "Análise de produtos da Cymbal".

### Tarefa 2: Gerador de Slogans (Few-Shot Prompting)
Esta tarefa foca em criar um gerador de textos padronizado e controlável usando exemplos.
- **Instruções do Sistema:** É necessário definir o papel da IA, informando sobre a parceria com a Cymbal Direct e o foco em incentivar jovens a explorar a natureza.
- **Exemplos (Few-Shot):** O usuário deve inserir pelo menos dois exemplos (Entrada vs. Saída) para guiar o estilo do modelo (ex: Entrada detalhando uma mochila durável -> Saída: "Um elemento essencial para sua aventura").
- **Parâmetros:** O comando deve ser estruturado para aceitar variáveis dinâmicas, como características do produto, público-alvo e resposta emocional.
- **Conclusão:** Salvar o comando como "Modelo de gerador de slogans da Cymbal".

### Tarefas 3 e 4: Integração, Teste e Modificação de Código (Python)
A etapa final tira os comandos da interface visual do Vertex AI Studio e os leva para um ambiente de desenvolvimento real usando Jupyter Notebooks no Vertex AI Workbench.

- O usuário deve exportar o código Python de ambos os comandos criados (Imagens e Slogans), colá-los nos notebooks correspondentes (image-analysis.ipynb e tagline-generator.ipynb), ajustar a autenticação para usar o ID do Projeto e resolver dois desafios de modificação de código:
- **Modificação no Código de Imagem (Tarefa 3):**
  - Alterar o texto do prompt no código para exigir que a resposta tenha menos de 10 palavras.
  - Alterar um parâmetro no código (a Temperatura) para forçar o modelo a ser o mais criativo e inesperado possível.
- **Modificação no Código de Slogans (Tarefa 4):**
  - Alterar a string de entrada final no código Python para ordenar explicitamente que o modelo inclua a palavra-chave "nature" no slogan gerado.


