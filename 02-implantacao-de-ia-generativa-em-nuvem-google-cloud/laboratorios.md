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

## Laboratório 2: 
