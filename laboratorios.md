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
