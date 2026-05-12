# Operações de Machine Learning (MLOps) com a Vertex AI: Avaliação de Modelo

---

## Introdução à Avaliação de Modelos

### O que é a Avaliação de Modelos?
A avaliação de modelos é o processo de testar e analisar o desempenho de um modelo de Machine Learning. Funciona como um teste de qualidade para responder a perguntas essenciais: 
O modelo é preciso? É confiável? Funciona bem com dados novos? Ele ajuda a alcançar as metas de negócios traçadas?

### Por que é importante?
A avaliação é crucial por cinco motivos principais:
- **Desempenho:** Permite medir com clareza o quão bem o modelo está operando por meio de diversas métricas.
- **Generalização:** Garante que o modelo não funcione apenas com os dados usados no treinamento, mas que seja capaz de lidar com dados novos e variáveis do mundo real.
- **Escolha do Modelo:** Ajuda a comparar diferentes modelos para identificar o mais efetivo, otimizando o uso de recursos computacionais.
- **Melhoria Contínua:** Permite monitorar a degradação do modelo ao longo do tempo (mudanças nos padrões de dados) e determinar quando é necessário retreiná-lo.
- **Tomada de Decisões:** Fornece dados concretos para que as partes interessadas confiem no sistema e tomem decisões embasadas sobre implantações e atualizações.

### Quando ocorre a avaliação?
Embora permeie todo o fluxo de trabalho de ML, ela se concentra em duas fases críticas:
- **Após o treinamento inicial:** As métricas são analisadas para decidir se o modelo está pronto para entrar em produção (implantação).
- **Após a implantação (Avaliação Contínua):** O modelo é monitorado constantemente com novos dados reais. Se o desempenho cair, um retreinamento pode ser acionado.

### Como é feita? (Técnicas vs. Métricas)
Para avaliar um modelo, é preciso primeiro entender seu tipo (classificação, regressão, processamento de linguagem natural, etc.). A partir daí, utilizam-se técnicas e métricas, que possuem papéis diferentes:

1. Técnicas de Avaliação (O Processo)
  - São os procedimentos usados para testar o modelo, geralmente dividindo o conjunto de dados em partes separadas para treinamento e teste.
  - **Exemplos:** Validação Hold-out, Validação Cruzada K-Fold e Leave-One-Out.
  - **A Analogia do Bolo:** As técnicas representam o processo de preparar e assar o bolo (como os ingredientes são misturados, tempo de forno, temperatura, etc.).

2. Métricas de Avaliação (A Pontuação)
  - São os sistemas numéricos que quantificam o desempenho do modelo em uma tarefa específica.
  - **Classificação:** Acurácia, precisão, recall (revocação) e pontuação F1.
  - **Regressão:** Erro quadrático médio (MSE) e R².
  - **PLN (Processamento de Linguagem Natural):** BLEU e ROUGE.
  - **A Analogia do Bolo:** As métricas representam a avaliação final de quem come o bolo (a textura está boa? o sabor é o esperado?).

### Fatores a considerar na escolha de Técnicas e Métricas
Não existe uma abordagem única para todos os cenários. A escolha deve levar em conta:
  - **Tipo de Modelo e Meta do Projeto:** O que é mais importante para o sucesso do seu negócio específico?
  - **Tamanho do Conjunto de Dados e Custo Computacional:** Dados pequenos ou grandes exigem técnicas diferentes. Deve-se buscar um equilíbrio entre a precisão da avaliação e o custo em infraestrutura para realizá-la.
  - **Compensação Viés-Variância:** Uso de técnicas como bootstrapping para entender problemas de overfitting (sobreajuste) e underfitting (subajuste).
  - **Custo dos Erros e Desequilíbrio de Dados:** Qual a gravidade de um erro na vida real (ex: um diagnóstico médico falso negativo)? Além disso, conjuntos de dados desequilibrados exigem métricas que vão além da simples acurácia.

### Quem se beneficia da avaliação de modelos?
Os resultados da avaliação são essenciais para diversos públicos:
  - **Cientistas de Dados / Engenheiros de ML:** Para ajustar, aprimorar e escolher os melhores algoritmos.
  - **Líderes Empresariais:** Para entender o impacto financeiro (receita/despesas) e a satisfação do cliente.
  - **Desenvolvedores de Software:** Para garantir uma integração confiável do modelo aos sistemas existentes.
  - **Usuários Finais:** Que dependem da precisão e segurança da ferramenta no dia a dia.
  - **Órgãos Reguladores:** Para auditar se a IA cumpre normas éticas e legais.
  - **Pesquisadores:** Para desenvolver novas metodologias e evoluir o campo da Inteligência Artificial.

---

## Avaliação de modelos em MLOps

### O Panorama Geral do MLOps
MLOps (Machine Learning Operations) é uma prática que une o melhor do desenvolvimento de software tradicional (DevOps) com o Machine Learning. 
Seu principal objetivo é conectar o desenvolvimento de modelos à sua operacionalização, ou seja, integrar os modelos criados em ambientes de produção reais para que possam agir e fazer previsões com base em dados do mundo real.

### Os Três Pilares do MLOps
O MLOps atua para criar modelos que sejam precisos, robustos e alinhados aos objetivos de negócios. Para isso, ele se baseia em três fundamentos:
  - **Colaboração:** Integração constante entre cientistas de dados, engenheiros de ML e as partes interessadas do negócio (stakeholders).
  - **Iteração:** Melhoria contínua dos modelos através de avaliações e atualizações frequentes.
  - **Sistematização:** Criação de um framework (estrutura) de controle e avaliação que garante a confiabilidade e a reprodutibilidade dos modelos a longo prazo.

### A Vertex AI no Ciclo de MLOps
A Vertex AI é apresentada como a plataforma completa do Google Cloud que simplifica todo esse processo. Ela unifica serviços avançados de IA, otimizando desde a criação até a implantação e o escalonamento dos modelos.

### Governança e Avaliação de Modelos
Um ambiente de MLOps maduro e com boa governança exige uma avaliação rigorosa. A avaliação não deve ser uma etapa isolada, mas sim integrada a todo o ciclo de vida do modelo (criação, treinamento e implantação).
- **Mitigação de Riscos:** A avaliação integrada permite que as equipes identifiquem precocemente riscos, defeitos, vieses (parcialidade) e outros problemas que possam impactar negativamente a experiência do usuário.
- **Comparação e Visualização:** Com os serviços da Vertex AI, é possível realizar avaliações iterativas em larga escala. A plataforma oferece recursos visuais avançados para comparar diferentes modelos, analisar recortes específicos de dados (anotações) e escolher o melhor candidato para produção.

### Maturidade em MLOps
Atingir a maturidade em MLOps significa criar um roteiro claro onde as fases de treinamento, validação e implantação são automatizadas e integradas.

Ao utilizar a Vertex AI, as equipes conseguem:
- Estabelecer ciclos de feedback para melhoria contínua.
- Garantir alta escalabilidade.
- Realizar comparações inteligentes e checagens automáticas de parcialidade (vieses).

---

## Desafios da avaliação de modelos e soluções oferecidas pela Vertex AI

### Principais Desafios na Avaliação de Modelos de ML
Mesmo os melhores modelos de Machine Learning enfrentam obstáculos que podem comprometer sua confiabilidade. Os principais desafios incluem:
- Problemas com Dados:
  - **Overfitting (Sobreajuste):** O modelo decora os dados de treinamento, mas tem péssimo desempenho ao lidar com dados novos e inéditos.
  - **Shift de Dados (Desvio de Conceito):** Ocorre quando a realidade muda com o tempo e os dados atuais já não correspondem àqueles usados no treinamento, prejudicando as previsões.
  - **Falta de Representatividade:** Se os dados de treino não cobrirem a variedade de cenários do mundo real, o modelo será impreciso.
- **Escolha Inadequada de Métricas:** Avaliar o modelo olhando apenas para uma métrica (como acurácia) pode ser enganoso, mascarando falhas em classes minoritárias. A métrica deve sempre estar alinhada ao objetivo do negócio.
- **Interpretabilidade ("Caixa-Preta"):** Modelos complexos (como redes neurais profundas) são difíceis de explicar. Não saber por que o modelo tomou uma decisão é um risco enorme em setores regulamentados.
- **Viés e Parcialidade:** Se os dados históricos contiverem preconceitos, o modelo não só aprenderá esses vieses, como poderá amplificá-los, gerando resultados injustos.
- **Deterioração e Integração:** O modelo perde eficiência ao longo do tempo conforme o cenário real muda. Além disso, integrá-lo ao sistema de produção gera atritos logísticos e de comunicação entre equipes.

### Estratégias para Solucionar os Desafios
Para mitigar esses problemas:
- **Avaliação Multidimensional:** Usar várias métricas em conjunto (Acurácia, Precisão, Recall, F1, AUC-ROC).
- **Validação Meticulosa:** Utilizar técnicas de divisão de dados, como amostra estratificada e validação cruzada.
- Combate ao Overfitting:
  - **Regularização:** Força o modelo a focar nos padrões reais e ignorar os "ruídos".
  - **Dropout:** Obriga a rede a aprender de forma redundante, tornando-a mais robusta.
  - **Parada Antecipada (Early Stopping):** Interrompe o treinamento assim que o desempenho do modelo começa a cair.
- **Ferramentas de Explicabilidade:** Uso de métodos como LIME e SHAP para entender a importância de cada atributo na decisão do modelo.
- **Monitoramento Contínuo:** Acompanhar o modelo em produção para detectar desvios de dados a tempo.

### Avaliação de Modelos com a Vertex AI
Implementar todas essas estratégias manualmente é complexo. A Vertex AI automatiza e fornece ferramentas avançadas para avaliação, comparação e testes em larga escala, permitindo segmentar os dados e gerar visualizações detalhadas.

**Requisitos para avaliar na Vertex AI:**
Para iniciar uma avaliação na plataforma, são necessários três elementos:
1. Um Modelo Treinado (criado via AutoML ou código personalizado).
2. Saída de Predição em Lote (resultados gerados pelo modelo em um job de predição).
3. **Dados Empíricos (Ground Truth):** O "gabarito", ou seja, os dados corretamente rotulados por humanos para servir de base de comparação.

### O Fluxo de Trabalho (Passo a Passo)
O processo típico de avaliação na plataforma segue estas 6 etapas:
1. **Treinamento:** Treinar o modelo.
2. **Predição:** Executar predições em lote com os dados de teste.
3. **Preparação:** Organizar os dados empíricos (informações corretas).
4. **Avaliação:** Iniciar o job de avaliação, onde a plataforma compara automaticamente as predições com o gabarito.
5. **Análise:** Verificar as métricas geradas para entender o desempenho.
6. **Iteração:** Usar os insights para melhorar o modelo e comparar diferentes versões até chegar ao cenário ideal.

### Como a avaliação se encaixa no ciclo de vida?
- **Antes da Implantação**: Permite comparar diferentes versões de modelos recém-treinados para escolher qual vai para produção.
- **Após a Implantação (Avaliação Contínua):** Analisa o desempenho com dados novos do dia a dia. Se as métricas caírem, a plataforma sinaliza a necessidade de retreinamento.

---

## Desafios da Avaliação de Tarefas de IA Generativa: Introdução

### A Transição para a IA Generativa
Enquanto o Machine Learning tradicional foca na análise e previsão, o mundo da IA Generativa lida com a criação de conteúdos totalmente novos (como imagens realistas, músicas e histórias) a partir da aprendizagem de padrões em vastos conjuntos de dados. 
Essa capacidade de inovar e gerar saídas criativas e diversificadas traz novos e complexos desafios para a avaliação de modelos, que continua sendo vital para garantir a qualidade e a confiabilidade dos resultados.

### IA Preditiva vs. IA Generativa vs. LLMs
Para alinhar os conceitos, a transcrição esclarece as diferenças entre três termos frequentemente confundidos:
- **IA Preditiva (Não Generativa):** Focada em analisar dados para fazer previsões, classificações ou tomar decisões (ex: prever vendas ou classificar e-mails como spam).
- **IA Generativa:** Um termo amplo que engloba qualquer modelo capaz de criar conteúdo novo e diversificado, seja texto, imagem, áudio ou código.
- **LLMs (Large Language Models):** São um subconjunto da IA Generativa especializado exclusivamente em tarefas de linguagem, como geração de textos, traduções e resumos.

### O Ecossistema e os Componentes de um LLM
A jornada da IA Generativa começa com a escolha de um modelo pré-treinado. No entanto, em produção, um LLM não atua sozinho. Ele está no centro de um ecossistema complexo e interage com diversos componentes essenciais. 
Para avaliar o sistema adequadamente, é preciso entender esse "bloco de LLM", composto por:
- **O Motor Principal (LLMs):** É o mecanismo central de raciocínio, geralmente acessado via APIs de plataformas (como Google Cloud) ou modelos de código aberto (como Mistral).
- **Fontes de Dados:** Fornecem contexto vital para as respostas usando bancos de dados relacionais, vetoriais ou de gráficos. São a base estrutural para técnicas como a Geração Aumentada de Recuperação (RAG).
- **Templates de Comando (Prompts):** Instruções padronizadas e compartilhadas nas solicitações feitas ao modelo. Costumam ser tratadas e gerenciadas como código (versionamento).
- **Memória:** Atua como uma fonte de dados dinâmica. Ela armazena e recupera o histórico de interações com o usuário para manter o contexto vivo durante uma conversa.
- **Ferramentas (Tools):** Expandem as capacidades do LLM permitindo que ele interaja com sistemas externos, como fazer chamadas de API, executar blocos de código ou buscar informações na web.
- **Fluxo de Controle de Agente:** Permite que o modelo trabalhe de forma autônoma e iterativa, fazendo várias tentativas e refinamentos em uma tarefa até atingir um critério de parada predefinido.
- **Proteções (Guardrails):** São os mecanismos de segurança que filtram a saída do modelo antes que ela chegue ao usuário final. Podem ser lógicas simples (bloqueio de palavras-chave nocivas) ou o uso de modelos secundários de verificação, podendo até acionar uma revisão humana (fallback) se necessário.

### Uma Mudança de Paradigma na Avaliação
Devido à inclusão de todos esses componentes, o design de aplicações com LLMs é muito mais amplo e diversificado.

---

## A Arte e a Ciência de Avaliar Modelos de Linguagem Grandes

### A Complexidade da Avaliação de LLMs
A avaliação de Grandes Modelos de Linguagem não segue a mesma linearidade dos modelos preditivos (onde se define um objetivo, coleta-se dados e analisa-se a saída). 
Devido à sua escala massiva, alta complexidade e capacidade de executar múltiplas tarefas, os LLMs introduzem desafios únicos que exigem novas abordagens de validação.
  
Esses desafios podem ser divididos em seis categorias principais:

1. Problemas Relacionados aos Dados
  - O maior contraste com o machine learning tradicional está na forma como os dados são tratados e avaliados:
    - **Falta de Dados Iniciais:** Enquanto modelos preditivos exigem bons conjuntos de dados logo na primeira etapa, os LLMs muitas vezes começam com pouco ou nenhum dado específico. Isso dificulta a definição de um referencial claro (o que é considerado uma "boa saída").
    - **Contaminação de Dados:** Como os modelos de fundação são treinados com vastas fontes de dados (muitas vezes não reveladas publicamente), existe o risco de que os "dados de teste" já tenham sido incluídos no treinamento. Isso arruína a confiabilidade das análises comparativas.
    - **Dados de Referência Limitados:** Métricas clássicas (como BLEU e ROUGE) precisam de um "gabarito" para comparar a resposta do modelo. Em LLMs, onde existem dezenas de respostas criativas aceitáveis, é muito difícil construir bases de referência de alta qualidade que englobem todas as saídas válidas.
    - **Critérios de Qualidade em Aberto:** Diferente de tarefas exatas, definir o que constitui um conjunto de dados "ideal" para testar LLMs ainda é um problema sem solução definitiva na indústria.

2. Complexidade e Tomada de Decisões
  - O espaço de decisão na criação de LLMs é imenso. Envolve escolhas críticas sobre treinamento, seleção de arquitetura, personalização (tuning) e aprendizado contextual. O funcionamento interno desses modelos é tão vasto e complexo que escolher a configuração ideal e interpretar o porquê o modelo gerou certa saída exige muitos recursos e considerações cuidadosas.

3. Viés e Parcialidade
  - Os LLMs podem absorver preconceitos dos seus dados de treinamento. Isso é um problema grave, pois o modelo pode gerar saídas injustas, preconceituosas e acabar amplificando desigualdades sociais. Detectar, avaliar e mitigar esses vieses é essencial para garantir o uso ético da tecnologia.

4. Generalização no Mundo Real
  - Testes padronizados e comparativos (benchmarks) são úteis para criar rankings de desempenho em laboratório. No entanto, o mundo real é caótico e imprevisível. O desempenho perfeito de um LLM em um teste controlado não garante que ele conseguirá generalizar e lidar com as ambiguidades da implantação real.

5. Segurança e Vulnerabilidades
  - Os LLMs são suscetíveis a manipulações intencionais.
    - **Ataques Adversários:** Usuários mal-intencionados podem inserir comandos criados especificamente para "enganar" o modelo e forçá-lo a gerar saídas nocivas, incorretas ou até mesmo envenenar seus dados de treinamento. Isso expõe grandes falhas nos métodos de avaliação atuais e exige pesquisas contínuas de segurança.

6. Subjetividade e Novos Métodos de Avaliação
  - Avaliar textos e conteúdos criativos é algo intrinsecamente subjetivo, pois raramente existe "apenas uma resposta certa". Entender as nuances dessas saídas geradas requer metodologias robustas e muita análise interpretativa. Além disso, novos métodos de avaliação surgem rapidamente no mercado, colocando em xeque as práticas que já estavam consolidadas e exigindo que os profissionais mantenham a mente aberta para inovações.

---

## Além da Acurácia: Como Dominar as Métricas de Avaliação da IA Generativa

### Tipos de Avaliação de Modelos
A avaliação de um LLM começa pela escolha do formato de julgamento mais adequado. Eles variam em complexidade e profundidade:
- **Avaliação Binária:** É o formato mais simples (ex: Sim/Não, Aprovado/Reprovado). É fácil de implementar e útil para detectar spam ou moderação básica, mas não detalha a qualidade do erro.
- **Avaliação Categórica:** Oferece múltiplas opções (ex: Positivo/Neutro/Negativo, ou notas de 1 a 5 estrelas). Traz mais nuances, mas exige critérios claros para não gerar confusão na interpretação.
- **Avaliação de Classificação (Ranking):** Compara a saída de vários modelos baseando-se na preferência do usuário (ex: "Qual destes três resumos é o melhor?"). É muito útil para identificar o melhor desempenho relativo, mas consome muitos recursos.
- **Avaliação Numérica:** Atribui uma pontuação matemática (como porcentagem de acurácia, F1, ROUGE ou BLEU). Gera resultados objetivos e comparáveis, mas falha em capturar as nuances complexas de um texto criativo.
- **Avaliação de Texto (Feedback Humano):** Especialistas fornecem críticas, comentários e explicações detalhadas sobre os erros e acertos. Traz insights qualitativos profundos, mas é um processo demorado, subjetivo e difícil de escalar.
- **Avaliação Multitarefa:** A abordagem mais completa. Combina métricas numéricas (quantitativas) e feedback humano (qualitativo) para garantir uma análise global do modelo em diversas tarefas simultâneas (ex: tradução + resumo).

### Categorias de Métricas para LLMs (A Analogia da Redação)
Avaliar um LLM é como um professor corrigindo a redação de um aluno. As métricas se dividem nas seguintes áreas:
- **Similaridade Lexical (O vocabulário está correto?):** Avalia se a IA usou palavras semelhantes a um texto de referência criado por humanos, focando na correspondência de palavras e ignorando a gramática. Exemplos: BLEU, ROUGE e METEOR.
- **Qualidade Linguística (O texto é claro e bem estruturado?):** Foca na fluência, coerência e gramática.
  - Uma métrica comum aqui é a Perplexidade, que mede a capacidade do modelo de prever a próxima palavra. Uma menor perplexidade indica um texto mais fluido, mas não garante que ele seja verdadeiro ou seguro. Outro exemplo: BLEURT.
- **Métricas Específicas para Tarefas (O aluno fez o que foi pedido?):** Mede o sucesso do modelo na tarefa exata proposta (ex: correspondência exata para responder a uma pergunta direta).
- **Segurança e Imparcialidade (A redação ofende alguém?):** Verifica se o conteúdo gerado é nocivo, tóxico, preconceituoso ou carrega discursos de ódio.
- **Embasamento / Factualidade (O aluno "inventou" fatos?):** Garante que o LLM entende o mundo real e não está sofrendo de "alucinações", utilizando ferramentas de checagem de fatos.
- **Métricas Focadas no Usuário (A redação foi agradável de ler?):** Mede o engajamento, a utilidade e o nível de satisfação das pessoas que estão interagindo com a IA na ponta final.

### A Importância das Métricas de Diversidade
Além de gerar respostas corretas, um LLM precisa ser criativo e evitar respostas robóticas, engessadas ou repetitivas. Para medir a variedade e riqueza do texto, utilizam-se as Métricas de Diversidade:
- **Distinct-n:** Conta o número de sequências de palavras exclusivas (n-gramas) no texto gerado.
- **Entropia:** Mede a imprevisibilidade da IA. Quanto maior a entropia, mais aleatório e original é o texto. Textos com baixa entropia tendem a ser repetitivos.
- **Self-BLEU:** Compara o texto do modelo com outros textos que ele mesmo gerou. Uma pontuação baixa indica que o modelo não se repete e consegue gerar respostas variadas para o mesmo tema.
- **MAUVE:** Compara a variedade das palavras usadas pelo modelo com o vocabulário rico usado por humanos reais.
- **Cobertura:** Verifica se a IA conseguiu abordar todos os conceitos e palavras-chave presentes nos dados de referência.

**O grande desafio:** Alta diversidade nem sempre significa alta qualidade. Um texto muito aleatório pode perder o sentido e a coerência. 
Por isso, a avaliação ideal deve sempre equilibrar métricas automatizadas (para escala) com o julgamento humano (para compreensão de contexto e subjetividade).

---

## Práticas recomendadas para a avaliação de LLMs

### As Duas Fases Principais da Avaliação
A avaliação de modelos não ocorre em um único momento; ela deve ser dividida em duas etapas cruciais dentro do fluxo de trabalho de Machine Learning:
- **Pré-produção:** Ocorre antes do modelo ir para o mundo real. Envolve a criação de templates de comandos (prompts), a escolha criteriosa do modelo base e a otimização de parâmetros de ajuste (tuning).
- **Em produção:** Após a implantação, o desempenho do modelo deve ser monitorado continuamente para garantir que ele mantenha a qualidade diante de novos dados diários.
  
Devido à alta complexidade das respostas geradas pela IA Generativa, essa avaliação contínua funciona como um ciclo de feedback ininterrupto. 
Ela garante que a ferramenta se mantenha útil, segura, alinhada às necessidades operacionais dos usuários e aos objetivos de negócios e culturais da empresa.

### Estudo de Caso: O Desafio da Escala em Projetos Reais
Para ilustrar os desafios da avaliação, temos um cenário hipotético: você lidera um projeto de "Identificação de Tendências" em uma grande empresa de mídia.
  
- **O Problema:** O processo atual de identificar tendências nas notícias é manual, lento e propenso a erros.
- **A Solução com LLMs:** Criar uma ferramenta capaz de analisar volumes massivos de notícias, redes sociais e comentários em tempo real. O modelo precisa identificar conceitos, agrupar artigos, analisar sentimentos e extrair palavras-chave, exibindo tudo em um painel dinâmico para a equipe editorial.
  
**Os Desafios Práticos:**
Se você precisa testar pelo menos dois modelos diferentes, avaliando mais de 1.000 artigos diários utilizando duas ou mais métricas, os seguintes problemas surgem:
- A dificuldade de criar um framework (estrutura) de avaliação que seja escalonável e suporte tamanhos variados de saída.
- A necessidade de validar resultados e calcular métricas com precisão em um volume gigantesco de dados.
- A exigência de criar uma estrutura adaptável e reutilizável, que demande o mínimo de esforço de configuração futura.

### Estratégias e Práticas Recomendadas
Para lidar com esses desafios e aumentar a eficácia da avaliação de LLMs, a transcrição recomenda quatro estratégias principais:

1. Use Múltiplas Métricas de Avaliação:
  - Nunca dependa de apenas uma métrica (como acurácia). Combine várias pontuações para medir de forma completa todos os ângulos do modelo, incluindo fluência, coerência, relevância e a capacidade de concluir a tarefa solicitada.

2. Incorpore o Julgamento Humano de Forma Inteligente:
  - O feedback humano é essencial, mas subjetivo. Para resolver isso, use vários avaliadores humanos simultaneamente e verifique a confiabilidade e concordância entre eles. O crowdsourcing pode ser usado para trazer perspectivas diferentes e ganhar escala no processo.

3. Utilize Dados Específicos do Domínio:
  - Para testar o modelo para o mundo real, abandone conjuntos de dados genéricos. Use bases de dados totalmente voltadas para o setor da sua empresa (ex: jargões médicos, textos jurídicos, notícias jornalísticas).

4. Adote o MLOps e Automatize o Processo:
  - Não avalie o modelo manualmente após cada pequena rodada de ajuste (tuning). Em vez disso, crie um processo automatizado onde a avaliação seja a última etapa obrigatória do fluxo de trabalho. Sempre que o modelo for ajustado, o sistema deve avaliá-lo instantaneamente. Isso aumenta a eficiência do desenvolvimento.

---

## Como Superar os Desafios na Avaliação

### O Papel da Vertex AI na Avaliação
A Vertex AI é apresentada como uma plataforma unificada do Google Cloud que permite prototipar, desenvolver, implantar e, principalmente, avaliar modelos preditivos e generativos. 
Ela oferece ferramentas integradas para que as equipes implementem as práticas recomendadas de MLOps.  
  
Através da plataforma, é possível:
- Comparar modelos pré-treinados para escolher o melhor.
- Testar parâmetros (como a "temperatura" do modelo) e ver como eles afetam a qualidade da saída.
- Otimizar a engenharia de comandos (prompts).
- Garantir a segurança, eliminando vieses e saídas indesejadas.

### Métodos de Avaliação na Vertex AI
A Vertex AI divide a avaliação em duas grandes abordagens (também chamadas de "serviços de pipeline de avaliação"):
1. Avaliação Baseada em Computação (Tradicional)
  - É a abordagem matemática clássica, rápida e econômica, muito usada no mercado e na academia. Ela compara as respostas do modelo com um "gabarito" (dados empíricos / informações de referência) pré-definido pelo usuário.
  - **Desvantagem:** Fórmulas não conseguem captar a nuance criativa e os diferentes estilos de um texto gerado.
  - **Categorias de métricas usadas:**
    - **Baseadas no Léxico:** Mede a similaridade das strings (palavras) com a resposta esperada. Ex: Correspondência exata e ROUGE.
    - **Baseadas em Contagem:** Quantifica compatibilidade/incompatibilidade. Ex: Acurácia e F1.
    - **Baseadas em Embedding:** Compara o significado (semântica) entre a saída e o gabarito convertendo os textos em representações numéricas vetoriais.

2. Avaliação Baseada em Modelo (A Nova Abordagem)
  - Desenvolvida pelo Google Research, esta técnica inovadora usa um LLM especializado e calibrado para atuar como um "julgador", simulando a avaliação que um humano faria, porém com a velocidade de uma máquina.
  - **Vantagens:**
    - Escalonável, econômica e muito mais rápida que contratar avaliadores humanos.
    - É baseada em dados objetivos, reduzindo os vieses típicos da preferência humana.
    - Atualmente, suporta quatro tarefas principais: Resumo, Respostas a Perguntas, Uso de Ferramentas e Geração de Texto em Geral.

### Paradigmas de Avaliação: Por Pontos vs. Por Pares
Na Vertex AI, os testes de avaliação podem ser configurados de duas formas distintas, dependendo do objetivo:
- **Avaliação por Pontos (Absoluta):** Avalia um único modelo de forma isolada, gerando uma pontuação numérica absoluta para ele. Serve para entender como ele se comporta no mundo real, identificar seus pontos fracos e estabelecer uma nota de referência (baseline) para futuras melhorias.
- **Avaliação por Pares (Relativa):** Coloca dois modelos "lado a lado" e pede ao avaliador (seja humano ou o LLM julgador automático do Google) para escolher qual teve o melhor desempenho na tarefa. É essencial para tomada de decisões, como escolher qual modelo comprar ou decidir qual configuração de prompt funciona melhor.

### O Diferencial: Transparência e Confiança
A grande inovação da Avaliação Baseada em Modelo (onde um LLM julga o outro) na Vertex AI é que ela não entrega apenas um número final. Ela aumenta a transparência do processo fornecendo:
- **Explicações em String (Fluxo de Consciência):** O LLM julgador escreve um texto explicando passo a passo o raciocínio que o levou a dar aquela nota ou a escolher determinado modelo.
- **Pontuação de Confiança (0 a 1):** Um valor numérico que mostra o quão "certeiro" o julgador está de sua própria avaliação. Essa pontuação é gerada testando o modelo múltiplas vezes (decodificação de autoconsistência); se o julgador chegar à mesma conclusão várias vezes, sua pontuação de confiança será alta.

### Orquestração e Pipelines
Todo esse processo (chamar o modelo, gerar a resposta, enviá-la ao julgador e calcular as métricas) pode ser automatizado e orquestrado usando o Vertex AI Pipelines.  
  
Devido ao tempo de inicialização (latência) da infraestrutura, o uso de pipelines não é ideal para checagens instantâneas unitárias, mas é extremamente benéfico para avaliações em larga escala (em background) e para automatizar testes dentro do ciclo contínuo de MLOps (onde o resultado não precisa ser imediato).

---

## Como Simplificar a Avaliação de Modelos com Métricas Baseadas em Computação

### O que são Métricas Baseadas em Computação?
As métricas baseadas em computação (ou métricas tradicionais/matemáticas) oferecem uma forma rápida e efetiva de avaliar modelos de Inteligência Artificial. 
Esse método analisa o desempenho do modelo baseando-se estritamente em pares de entrada e saída, comparando o que o modelo gerou com um "gabarito" (informação empírica). 
Essa metodologia é amplamente utilizada em pesquisas acadêmicas e parâmetros de mercado (benchmarks).

### Suporte e Métricas por Tarefa
Na Vertex AI, essas métricas estão disponíveis para as versões base e ajustadas (tuned) dos modelos de texto da família PaLM. As métricas são personalizadas de acordo com a tarefa executada:
- **Tarefas de Classificação:** Utilizam métricas como Micro-F1, Macro-F1 e F1 por classe.
- **Tarefas de Resumo:** Utilizam o ROUGE-L, que mede a capacidade do modelo de capturar a essência de um artigo identificando a maior sequência de palavras em comum com o texto de referência.

A documentação oficial da Vertex AI detalha a lista completa de métricas adequadas para cada necessidade específica.

### O Fluxo de Trabalho (Passo a Passo da Avaliação)
A execução de uma avaliação baseada em computação pode ser feita via API REST, SDK da Vertex AI ou pelo Console do Google Cloud. O processo envolve três etapas fundamentais:

1. Preparação do Conjunto de Dados
  - Você deve criar uma base contendo pares de Comandos (Prompts) e Informações Empíricas (Gabarito).
  - O comando deve conter a instrução clara e o contexto.
  - A informação empírica é a resposta correta esperada, que será cruzada com a resposta gerada pela IA para calcular a nota.
  - **Prática recomendada:** Incluir pelo menos 10 exemplos que representem fielmente os cenários de aplicação do mundo real.

2. Upload para a Nuvem
 - O conjunto de dados preparado deve ser carregado em um bucket (repositório) do Google Cloud Storage.

3. Execução do Job de Avaliação
  - Utilizando a biblioteca Python e os templates do Vertex AI Pipelines, você inicia a avaliação em larga escala.
  - Nesta etapa, é necessário especificar parâmetros-chave: a localização do conjunto de dados, o tipo de tarefa, onde a saída será salva e qual modelo será avaliado.

### Limitações deste Método e o Fator Humano
Avaliar vários modelos simultaneamente é um processo técnico simples: basta executar o pipeline para cada um e comparar as métricas agregadas (os números finais).  

No entanto, a transcrição alerta para um grande desafio na interpretação dos resultados:
- Métricas matemáticas agregadas indicam qual modelo é "tecnicamente" superior, mas são difíceis de traduzir para a realidade.
- Elas não revelam qual modelo produz textos e resumos mais alinhados às preferências humanas (qualidade subjetiva).
- Avaliar manualmente par por par para atribuir uma "nota de preferência humana" é um processo demasiadamente lento e inviável em larga escala.

---

## Como Comparar Desempenhos com uma Avaliação Baseada em Modelo

### Introdução ao AutoSxS
O AutoSxS (Avaliação Lado a Lado Automática) é uma ferramenta avançada projetada para facilitar o teste A/B sob demanda de Grandes Modelos de Linguagem (LLMs) em tarefas específicas, como resumos e respostas a perguntas.  
A base do AutoSxS é o "avaliador automático": um LLM treinado especificamente para atuar como um "modelo julgador". Ele analisa a qualidade das respostas geradas por outros modelos e determina qual teve o melhor desempenho, fornecendo uma métrica chamada taxa de ganho (win rate).  

### O Diferencial: Transparência e Explicação
Ao contrário de métricas tradicionais que fornecem apenas um número, o AutoSxS oferece alta transparência. Para cada avaliação, o modelo julgador fornece:
- **Uma pontuação de confiança:** Quantificando o nível de certeza do julgador sobre a sua própria escolha.
- **Explicações em nível de entrada:** O modelo escreve um texto explicando detalhadamente por que preferiu o Modelo B em vez do Modelo A (ex: "O Modelo B foi favorecido devido a uma maior coerência e melhor cobertura do assunto").

Isso ajuda os usuários a entenderem profundamente os pontos fortes e fracos de cada modelo, alinhando a decisão da IA ao julgamento que um humano faria.

### O Passo a Passo da Avaliação na Vertex AI
Para usar o AutoSxS comparando, por exemplo, o Gemini Pro com outro modelo (considerando que as respostas prévias já foram geradas), o fluxo de trabalho exige três etapas fundamentais:

1. Preparação do Conjunto de Dados
  - O conjunto de dados deve estar preferencialmente no formato JSON/JSONL.
  - Cada linha (exemplo único) deve conter: ID, o comando original (prompt), o contexto e as respostas geradas pelos diferentes modelos.
  - **Recomendação de Escala:** Embora funcione com apenas 1 exemplo, é altamente recomendado usar de 400 a 600 exemplos (baseados em cenários de uso reais) para que as métricas agregadas sejam precisas e confiáveis.

2. Armazenamento
  - O conjunto de dados JSON deve ser armazenado em um bucket do Google Cloud Storage ou em uma tabela do BigQuery.

3. Execução do Pipeline de Avaliação
  - A avaliação é orquestrada através do Vertex AI Pipelines, onde você define parâmetros essenciais antes de executar o job via SDK Python:
    - **evaluation_dataset:** Localização dos dados (Cloud Storage ou BigQuery).
    - **id_columns:** Campos usados para distinguir cada exemplo de avaliação.
    - **task:** O tipo da tarefa que será avaliada (ex: "resumo").
    - **Configurações do Avaliador:** Instruções de inferência e contextos para guiar o LLM julgador, além de indicar as colunas exatas onde estão as respostas geradas a serem comparadas.

### Resultados da Avaliação
Após a conclusão do job, a Vertex AI entrega os resultados em dois formatos principais:
- **Tabela de Julgamento:** Mostra o resultado detalhado de cada par avaliado, indicando o modelo vencedor, a pontuação de confiança e a explicação textual do motivo da escolha.
- **Métricas Agregadas (Taxas de Ganho):** Apresenta o panorama geral, mostrando a porcentagem total de vezes que o avaliador automático escolheu o Modelo A em relação ao Modelo B.

### Integração com Preferências Humanas
O AutoSxS é flexível e permite a incorporação de validação humana para garantir que a IA julgadora está realmente alinhada ao que as pessoas preferem:
- Basta adicionar uma coluna no conjunto de dados (ex: human preference) indicando qual resposta um avaliador humano considerou melhor.
- O parâmetro é atualizado no pipeline antes da execução.
- O resultado final gerará matrizes de alinhamento, indicando o nível de concordância entre as escolhas do avaliador automático e as escolhas do avaliador humano (uma métrica extra de acurácia).
