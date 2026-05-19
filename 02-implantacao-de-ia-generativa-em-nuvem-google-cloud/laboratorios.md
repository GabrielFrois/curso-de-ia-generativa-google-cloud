# Anotações dos Laboratórios

## Laboratório 1: Reduzir o Viés com o MinDiff no TensorFlow

### Visão Geral e Propósito do Laboratório

Este laboratório prático de nível intermediário foca na transição entre a identificação do viés e a correção ativa dele. 
O objetivo central é ensinar como utilizar a técnica MinDiff — aplicada através da biblioteca Model Remediation do TensorFlow — para mitigar preconceitos em modelos de Inteligência Artificial, especificamente em tarefas de Processamento de Linguagem Natural (PLN).

### Objetivos de Aprendizagem (O Que Será Feito)

Durante o laboratório, é feito todo o fluxo de trabalho de uma auditoria e correção de viés, estruturado nas seguintes metas:
- **Compreensão de Dados:** Analisar um conjunto de dados focado em "textos de toxicidade" (comentários ofensivos ou abusivos).
- **Treinamento de Referência (Baseline):** Criar e treinar um modelo inicial de classificação de toxicidade padrão, sem nenhuma intervenção ética.
- **Diagnóstico Visual:** Plotar e analisar os resultados das previsões desse modelo inicial para comprovar matematicamente a existência de viés em suas decisões.
- **Remediação de Modelo:** Aplicar a técnica MinDiff utilizando a biblioteca oficial do TensorFlow. A técnica MinDiff funciona penalizando o modelo durante o treinamento se ele tratar grupos de dados de forma estatisticamente diferente, forçando-o a ser mais equitativo.
- **Avaliação Comparativa:** Colocar o modelo de referência (enviesado) lado a lado com o novo modelo (corrigido pelo MinDiff) para comparar e validar a redução do viés.

### Fluxo de Trabalho e Execução Prática

O laboratório é dividido em três fases operacionais dentro do ecossistema do Google Cloud:  

**Fase 1: Preparação da Infraestrutura (Configuração e APIs)**
Como a IA exige processamento em nuvem, o laboratório inicia com a preparação do ambiente isolado:
- **Acesso Seguro:** O login no Console do Google Cloud deve ser feito via janela anônima usando credenciais temporárias exclusivas do laboratório para evitar cobranças indevidas.
- **Ativação de Serviços Básicos:** É obrigatório ativar duas APIs fundamentais para o funcionamento do ambiente de desenvolvimento: a API Notebooks e a API Vertex AI.

**Fase 2: Criação do Ambiente de Desenvolvimento (Vertex AI Workbench)**
O código não roda na máquina local do usuário, mas sim em uma máquina virtual (VM) no Google Cloud.
- Instanciamento: O aluno deve criar uma nova instância no Workbench da Vertex AI, mantendo as configurações de região e zona padrão fornecidas.
- Acesso à Interface: Após a inicialização (que leva alguns minutos), o aluno acessa o ambiente de programação abrindo o JupyterLab em uma nova aba.

**Fase 3: Execução do Código e Aplicação do MinDiff**
Com o ambiente em nuvem pronto, a fase de programação em si se inicia através do terminal do JupyterLab.
- **Clonagem do Repositório:** O aluno utiliza comandos de terminal (via git clone) para baixar o repositório oficial do curso (asl-ml-immersion), que contém todos os arquivos e materiais necessários, e executa o comando make install para instalar as dependências.
- **Navegação e Limpeza:** O usuário deve localizar o notebook específico da solução (min_diff_keras.ipynb dentro da pasta responsible_ai/fairness/solutions). Uma prática recomendada antes de iniciar é limpar todas as saídas de código pré-existentes na interface para garantir uma execução limpa.
- **Execução Célula a Célula:** Por fim, o aluno executa o notebook interativo (utilizando SHIFT+ENTER), lendo as instruções de cada bloco de código para compreender passo a passo como o TensorFlow Model Remediation treina e ajusta os pesos do modelo para atingir a imparcialidade desejada.

---

## Laboratório 2: Implantação de Modelo de Classificação de Imagens com Vertex Explainable AI

### Visão Geral e Propósito do Laboratório

Este laboratório prático de nível intermediário foca na aplicação real de técnicas de Inteligência Artificial Explicável (XAI) no ecossistema do Google Cloud.

O objetivo central vai além de simplesmente criar uma IA que reconhece imagens: o laboratório ensina como disponibilizar esse modelo em produção e fazer com que ele justifique visualmente suas decisões para os usuários, utilizando a ferramenta Vertex Explainable AI.

### Objetivos de Aprendizagem (O Que Será Feito)

Durante o exercício, o aluno passará por todo o ciclo de vida de um modelo de visão computacional (treinamento, implantação e auditoria), com as seguintes metas práticas:
- **Construção e Treinamento:** Criar e treinar um modelo personalizado de classificação de imagens usando o Vertex AI.
- **Implantação (Deploy):** Colocar esse modelo treinado em produção (em um Endpoint ativo), permitindo que ele receba novos dados e faça previsões no mundo real.
- **Geração de Previsões Explicáveis:** Configurar o endpoint não apenas para dizer "o que" está na imagem, mas para retornar os metadados de explicação da decisão.
- **Visualização de Atribuição de Atributos:** Usar a técnica de Gradientes Integrados (IG)  para renderizar um "mapa de calor" visual sobre a foto, destacando exatamente quais pixels o modelo considerou mais importantes para chegar à sua conclusão.

### Fluxo de Trabalho e Execução Prática

O laboratório é estruturado em três fases principais de execução na nuvem:

### Fase 1: Preparação da Infraestrutura e APIs
Como o treinamento e a implantação de modelos de imagem exigem processamento em nuvem, a primeira etapa é preparar o ambiente isolado:
- **Acesso Seguro:** O login no Console do Google Cloud é feito via janela anônima com credenciais temporárias do laboratório (para evitar problemas com contas pessoais).
- **Ativação de Serviços:** O aluno deve habilitar a API Vertex AI (o coração de todo o processo de Machine Learning do Google Cloud) e a API Notebooks para permitir a criação do ambiente de programação.

### Fase 2: Criação do Ambiente de Desenvolvimento (Vertex AI Workbench)
O código será executado em uma máquina virtual (VM) dedicada ao cientista de dados.
- **Instanciamento:** O aluno cria uma nova instância de Notebook no Vertex AI Workbench, mantendo as configurações de região padrão fornecidas pelo laboratório.
- **Acesso à Interface:** Após a inicialização da VM (que leva alguns minutos), o desenvolvedor acessa o ambiente abrindo uma aba do JupyterLab.

### Fase 3: Execução do Código e Geração de Explicações
Com o JupyterLab aberto, a fase de engenharia e modelagem entra em ação pelo terminal e pelo notebook:
- **Clonagem do Repositório:** O usuário utiliza comandos de terminal (como git clone e make install) para baixar os arquivos oficiais do curso (asl-ml-immersion) e instalar as dependências necessárias do Python.
- **Configuração do Notebook:** O aluno navega até o arquivo específico da solução (xai_image_vertex.ipynb na pasta de IA Explicável). É necessário garantir que o Kernel selecionado seja o Python 3 e limpar todas as saídas de código pré-existentes (Editar > Limpar todas as saídas) para que o teste seja feito do zero.
- **Treinamento e Implantação:** O aluno executa o notebook célula a célula (usando SHIFT+ENTER). O código guiará o usuário pelo processo de treinar o classificador de imagens no TensorFlow, fazer o deploy no Vertex AI, e, finalmente, chamar a API de explicação para renderizar os Gradientes Integrados diretamente sobre as imagens de teste.

---

## Laboratório 3: Privacidade Diferencial em Machine Learning com a TensorFlow Privacy

### Visão Geral do Laboratório
Este laboratório de nível intermediário traduz a teoria da IA Responsável para a prática. Ele demonstra, passo a passo, como aplicar os conceitos de 
Privacidade Diferencial no treinamento de modelos de Machine Learning utilizando a biblioteca oficial TensorFlow Privacy dentro do ecossistema do Google Cloud.

#### Objetivos Essenciais de Aprendizagem:
Ao concluir este experimento de arquitetura, o desenvolvedor estará capacitado a:
1. Substituir Otimizadores Padrão: Aprender a "agrupar" (encapsular) otimizadores tradicionais de Machine Learning (como o SGD) e substituí-los por suas contrapartes seguras e com privacidade diferencial (como o DP-SGD).
2. Calibrar Hiperparâmetros de Privacidade: Praticar a verificação e o ajuste fino dos novos hiperparâmetros introduzidos pela técnica (como o nível de ruído e o limite de truncamento de gradiente), buscando o equilíbrio entre segurança e desempenho.
3. Auditar e Medir Garantias: Utilizar as ferramentas de análise nativas da TensorFlow Privacy para medir matematicamente qual é a garantia real de privacidade (o valor de Epsilon) que o modelo treinado oferece.

### Passo a Passo da Execução
O laboratório é dividido em quatro fases técnicas, desde o provisionamento da infraestrutura na nuvem até a execução do código em Python.

### Fase 1: Configuração e Requisitos (Tarefa 0)
Antes de escrever qualquer código, é necessário preparar o ambiente e garantir as permissões de arquitetura.
- **Acesso Seguro:** O laboratório deve ser executado em uma janela anônima para evitar conflitos de credenciais, utilizando o projeto temporário fornecido pela plataforma.
- **Ativação de APIs Críticas:** O desenvolvedor deve acessar o Console do Google Cloud e ativar duas APIs fundamentais para a execução de modelos de IA em nuvem:
  - API Notebooks (Biblioteca de APIs)
  - API Vertex AI (Ativando todas as APIs recomendadas no painel da Vertex AI).

### Fase 2: Provisionamento do Ambiente de Desenvolvimento (Tarefa 1)
O código não rodará na máquina local, mas sim em uma infraestrutura gerenciada e otimizada para Machine Learning.
- **Criação da Instância:** No menu do Google Cloud, acessa-se Vertex AI > Workbench.
- **Máquina Virtual (VM):** Cria-se uma nova instância de Notebook baseada no JupyterLab, mantendo a região e zona padrão fornecidas pelo laboratório. Após o tempo de inicialização (2 a 3 minutos), o ambiente JupyterLab é aberto em uma nova guia.

### Fase 3: Importação do Repositório de Código (Tarefa 2)
Com a máquina virtual rodando, o próximo passo é baixar os materiais e arquivos do curso diretamente para a instância.
- Via Terminal: Abre-se o terminal integrado do JupyterLab e executa-se a clonagem do repositório oficial de imersão em ML do Google Cloud:
```Bash
git clone https://github.com/GoogleCloudPlatform/asl-ml-immersion.git
cd asl-ml-immersion
export PATH=$PATH:~/.local/bin
make install
```
- Validação: O desenvolvedor deve verificar no diretório se os arquivos foram baixados corretamente. Este repositório contém todos os notebooks do curso.

### Fase 4: Implementando a Privacidade Diferencial (Tarefa 3)
Esta é a fase onde a engenharia de privacidade acontece na prática.
- **Navegação:** Na interface do JupyterLab, o desenvolvedor deve seguir o caminho estrutural: asl-ml-immersion > notebooks > responsible_ai > privacy > solutions e abrir o arquivo alvo: privacy_dpsgd.ipynb.
  - (**Nota:** O termo "dpsgd" no nome do arquivo refere-se ao algoritmo de Gradiente Descendente Estocástico Diferencialmente Particular, abordado no resumo anterior).
- **Higienização do Notebook:** Antes de começar, é uma boa prática clicar em Editar > Limpar saídas de todas as células para garantir que você está rodando o código do zero e visualizando seus próprios resultados.
- **Execução Prática:** A partir deste ponto, o desenvolvedor lê as instruções internas do notebook e executa as células de código sequencialmente (usando SHIFT+ENTER). Durante a execução, ele observará na prática como a injeção de ruído afeta os gradientes, como o modelo é treinado de forma segura e qual é a métrica matemática de privacidade gerada ao final do processo.

---

## Laboratório 4:
