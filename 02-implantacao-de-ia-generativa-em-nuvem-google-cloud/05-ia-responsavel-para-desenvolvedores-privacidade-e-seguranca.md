# IA responsável para Desenvolvedores: Privacidade e Segurança

---

## Privacidade em Treinamento de Dados: Técnicas de Desidentificação

### O que é a Segurança de Dados no Contexto de IA?

A segurança de dados de treinamento foca na proteção de informações sensíveis que alimentam os sistemas de Inteligência Artificial. 
O princípio fundamental e mais recomendado é diminuir ao máximo o uso de dados sensíveis, preferencialmente bloqueando-os logo na fase de coleta (ex: coletando dados agregados em vez de interações individuais).

Para proteger os dados que precisam ser processados, a indústria adota duas abordagens não exclusivas:
- **Desidentificação:** Técnicas que alteram os dados originais (ex: encobrimento, mascaramento, tokenização).
- **Randomização:** Métodos matemáticos que adicionam "ruído" aos dados (ex: perturbação de dados e privacidade diferencial).

### Fatores de Avaliação das Técnicas (Os 2 Pilares)

Ao escolher uma abordagem de desidentificação, deve-se avaliar dois fatores críticos que definem os riscos e benefícios para o modelo:
1. **Reversibilidade (Risco de Vazamento vs. Auditoria):** É possível desfazer a técnica e reidentificar os dados originais?
  - **Prós:** Abordagens reversíveis são excelentes para auditoria e recuperação de dados.
  - **Contras:** Aumentam a probabilidade de vazamento de dados e reidentificação maliciosa.

2. **Integridade Referencial (Consistência vs. Privacidade):** A relação estrutural entre os registros é mantida após a anonimização?
  - **Prós:** Quando garantida, melhora drasticamente a consistência e o desempenho do modelo de Machine Learning, pois a IA ainda consegue extrair padrões válidos.
  - **Contras:** Apresenta os mesmos riscos de segurança da reversibilidade se os padrões forem correlacionados por atacantes.

### Visão Geral das Técnicas de Desidentificação
Para exemplificar cada técnica abaixo, utilizaremos o cenário de uma tabela transacional contendo as seguintes colunas: ID, Data, Hora, Valor ($), E-mail e Produto.

1. **Encobrimento (Exclusão)**
  - **A Abordagem:** É o processo bruto de excluir total ou parcialmente um valor sensível da visualização.
  - **Perfil Técnico:** Irreversível e não mantém a integridade referencial.
  - **Exemplo:** Remover completamente a coluna "E-mail" da tabela.
  - **Fraqueza (Perda de Dados):** O encobrimento destrói informações que poderiam ser valiosas para o Machine Learning, afetando a precisão e generalização. Exemplo: Encobrir dados de localização impede o modelo de aprender padrões geoespaciais vitais.

2. **Substituição**
  - **A Abordagem:** Troca um valor sensível por um valor alternativo genérico (escolhido por você ou aleatoriamente de uma lista).
  - **Perfil Técnico:** Irreversível e não mantém a integridade referencial.
  - **Exemplo:** Substituir todos os endereços da coluna "E-mail" pelo texto estático "Endereço de E-mail".
  - **Fraqueza:** Possui as mesmas limitações do Encobrimento: a perda drástica de dados impede o modelo de diferenciar os usuários.

3. **Mascaramento**
  - **A Abordagem:** Substitui alguns ou todos os caracteres de um valor sensível por outros (frequentemente usando hashes).
  - **Perfil Técnico:** Irreversível e não mantém a integridade referencial.
  - **Exemplo:** Mascarar a coluna "E-mail" alterando o identificador do usuário para um hash, mas mantendo o domínio da empresa visível.
  - **Diferença para Substituição:** Enquanto a substituição remove o dado e coloca um rótulo genérico no lugar, o mascaramento cobre os dados originais parcial ou integralmente de acordo com parâmetros específicos.

4. **Tokenização (Para Valores Categóricos)**
  - **A Abordagem:** Substitui um valor sensível por "tokens" gerados aleatoriamente, sendo cada token exclusivo para o valor que ele representa.
  - **Perfil Técnico:** Reversível e mantém a integridade referencial.
  - **Exemplo:** A coluna "E-mail" recebe tokens únicos (ex: User_A vira Token_99X).
  - **Vantagem e Risco:** Como a integridade é mantida, o ML continua aprendendo padrões perfeitamente. No entanto, por ser reversível, os dados ficam vulneráveis a ataques cibernéticos focados em descriptografar a base original.

5. **Agrupamento / Bucketing (Para Valores Numéricos)**
  - **A Abordagem:** Generaliza um número exato substituindo-o por um intervalo de valores.
  - **Perfil Técnico:** Irreversível e não mantém a integridade referencial.
  - **Exemplo:** Na coluna "Valor ($)", uma transação de $56 é substituída pelo intervalo genérico "50 a 60".
  - **O Desafio da Granularidade:** O engenheiro precisa equilibrar privacidade e desempenho. Se os intervalos (buckets) forem muito amplos (ex: "0 a 1000"), o modelo de ML não conseguirá prever nuances e perderá eficácia.

6. **Mudança (Para Valores de Data e Hora)**
  - **A Abordagem:** Altera um valor sensível de tempo/data somando ou subtraindo um fator de tempo aleatório.
  - **Perfil Técnico:** Reversível e mantém a integridade referencial.
  - **Exemplo:** Adicionar exatamente 1 dia a todas as entradas da coluna "Data e Hora". A sequência cronológica e a duração entre as transações permanecem idênticas.
  - **Risco:** Assim como a tokenização, se um atacante descobrir qual foi o "fator de mudança" (ex: descobrir que tudo foi adiantado em 1 dia), ele reverterá toda a tabela instantaneamente.

### Análise e Avaliação: O Risco da Reidentificação
O maior alerta na engenharia de privacidade é: nenhuma técnica garante 100% que os dados não serão reidentificados, nem mesmo as técnicas irreversíveis. O objetivo dessas abordagens é apenas minimizar o risco de ataques baseados em correlação de dados cruzados.

Para avaliar matematicamente a eficácia da sua estratégia antes de validá-la, a indústria utiliza duas métricas (ou técnicas) clássicas de privacidade:

1. **$k$-Anonimato (Proteção contra Correlação)**
  - **O Conceito:** Um conjunto de dados atinge o $k$-anonimato se cada combinação de valores sensíveis na tabela aparecer de forma idêntica em pelo menos $k$ registros diferentes.
  - Por que importa? Mesmo que você encubra o nome de uma pessoa, se ela for a única "Mulher, 25 anos, residente no CEP 12345" na tabela, ela será facilmente reidentificada. O $k$-anonimato força os dados a se "esconderem na multidão" garantindo que existam várias linhas com atributos idênticos.

2. **$l$-Diversidade (A Evolução do $k$-Anonimato)**
  - O Problema do $k$-Anonimato: Se você tem 10 pessoas agrupadas com os mesmos atributos (garantindo um $k$ de 10), mas todas as 10 possuem a mesma doença na coluna de diagnóstico, o agrupamento falha em proteger a privacidade, pois a dedução é óbvia.
  - A Solução ($l$-Diversidade): É uma extensão que garante que, dentro de cada grupo anonimizado, existam pelo menos $l$ valores diferentes para cada atributo sensível final. É uma medida estrita de diversidade interna.

**A Regra de Ouro:** A combinação ideal na engenharia de dados é aplicar técnicas de perturbação e anonimização até que o conjunto de dados alcance uma métrica sólida e predefinida de $k$-anonimato e $l$-diversidade, 
garantindo o melhor equilíbrio possível entre utilidade para a Inteligência Artificial e segurança para o usuário final.

---

## Privacidade em Treinamento de Dados: Técnicas de Ordem Aleatória

### O que são as Técnicas de Randomização?

Enquanto a desidentificação foca em ocultar ou remover informações diretas, a randomização visa preservar a privacidade ao injetar ruído ou perturbação matemática nos conjuntos de dados de treinamento. 
O objetivo é proteger a identidade individual sem destruir a capacidade do modelo de Inteligência Artificial de aprender as tendências gerais.

Neste contexto, a indústria trabalha com duas abordagens principais que se diferenciam pela complexidade e pelo nível de garantia de segurança:
- **Perturbação de Dados:** Uma técnica mais simples e fácil de implementar, baseada em pequenas modificações pontuais.
- **Privacidade Diferencial:** Uma abordagem rigorosa, com base matemática sólida, que oferece garantias formais de privacidade.

### 1. Perturbação de Dados
- **A Abordagem:** Consiste em inserir ruídos aleatórios ou realizar pequenas modificações estruturais para ocultar o valor real e sensível de um dado.
- **O Princípio:** Apesar da alteração individual, o conjunto de dados como um todo continua refletindo os padrões estatísticos originais, impedindo que um invasor identifique uma pessoa específica, mas permitindo que a IA extraia insights válidos.
- **O Desafio de Engenharia:** O nível de perturbação exige um equilíbrio delicado. Se o ruído for muito baixo, a privacidade falha; se for muito alto, os dados perdem a utilidade analítica e prejudicam o treinamento do modelo.

#### Técnicas Comuns de Perturbação:
1. **Adição de Ruído Aleatório (Para valores numéricos):** Soma-se ou subtrai-se um pequeno valor aleatório de cada ponto de dados. Exemplo: Uma idade de 34 anos pode ser registrada como 32 ou 35.
2. **Mudança Aleatória (Para valores numéricos e categóricos):** Troca ou embaralha os valores de diferentes pontos de dados aleatoriamente dentro do conjunto.
3. **Arredondamento Aleatório (Para valores numéricos):** Modifica a precisão dos dados, arredondando pontos numéricos exatos para níveis variáveis. Exemplo: Renda de $4.321 pode ser arredondada para $4.300 ou $4.500.
4. **Mapeamento Aleatório de Categoria (Para valores categóricos):** Reatribui aleatoriamente valores de texto para diferentes categorias dentro da mesma variável.

### 2. Privacidade Diferencial
- **A Abordagem:** É considerada a técnica padrão-ouro e "rigorosa" do mercado. Ela garante que a inclusão ou exclusão dos dados de um único indivíduo não tenha um impacto significativo na saída (resultado) final da análise.
- **O Objetivo:** Permitir que as empresas compartilhem métricas de alto nível ou façam inferências sobre grupos, tornando matematicamente impossível fazer engenharia reversa para descobrir se uma pessoa específica fazia parte daquele grupo ou não.

#### O Estudo de Caso (O Ataque de Diferença na Conferência):
Para entender o poder da Privacidade Diferencial, analise este cenário:
- **Dia 1:** O painel mostra o número de participantes por país (Itália no topo, Alemanha por último). Nenhuma identidade individual é revelada.
- **Dia 2:** O painel mostra uma nova contagem. Os números são quase iguais, mas você sabe que apenas uma pessoa nova entrou na conferência neste dia.
- **A Falha:** Ao cruzar os dados exatos do Dia 1 com o Dia 2, você percebe que a contagem da Alemanha subiu em 1. Logo, você deduz facilmente que o novo participante é alemão, quebrando o anonimato.
- **A Solução com Privacidade Diferencial:** O algoritmo altera aleatoriamente (injeta ruído) na contagem exibida nos dois dias. Os dados ficam ligeiramente menos precisos, mas a tendência geral (Itália no topo) se mantém. Se você tentar cruzar os dias agora, a diferença matemática será fruto do ruído, inviabilizando descobrir de onde o novo participante veio.

### Parâmetros-Chave da Privacidade Diferencial
A aplicação prática dessa técnica depende de dois parâmetros técnicos fundamentais que moldam o algoritmo:

#### 1. Parâmetro de Privacidade (Epsilon / $\epsilon$)
  - **O que é:** Um valor não negativo que quantifica o nível de rigor da proteção de privacidade aplicada pelo mecanismo.
  - **Como funciona (A Balança):**
    - Um valor de Epsilon menor oferece uma proteção muito mais forte, mas exige a injeção de uma quantidade massiva de ruído, o que pode destruir a utilidade do modelo.
    - Um valor maior melhora a precisão analítica do Machine Learning, mas enfraquece a garantia de privacidade.

#### 2. Sensibilidade
  - **O que é:** Uma métrica que avalia o impacto máximo que uma única pessoa pode causar no sistema. É a diferença absoluta máxima no resultado de uma consulta quando os dados de apenas um indivíduo são adicionados ou removidos.
  - **Por que importa:** A sensibilidade atua como a "bússola" do sistema. É com base nela que o engenheiro e o algoritmo determinam exatamente a proporção de ruído necessária para cobrir os rastros daquele indivíduo sem distorcer o conjunto total.

---

## Privacidade em Treinamento de Machine Learning: DP-SGD

