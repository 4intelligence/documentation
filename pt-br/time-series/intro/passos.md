# Passo a passo da criação de um projeto

Nessa seção, vamos abordar os passos da criação de um projeto de séries temporais. Ao final da leitura você será capaz de criar o seu próprio projeto. 

### 1) Passo 1

Comece nomeando o seu projeto e suba o arquivo de dados seguindo os [requisitos do dataset](/time-series/intro/requisitos.md). 

### 2) Passo 2

Selecione qual variável você deseja projetar, defina o conjunto de variáveis explicativas e confirme qual série contém informações sobre o período das observações. 

#### Definições 

**Variável dependente**

A variável dependente (também chamada de variável alvo, resultado ou y) é a variável de saída em um experimento, ou simplesmente a variável de interesse no modelo. 

**Variável explicativa**  

Variáveis explicativas (também chamadas de variáveis preditoras, regressores ou x) são usadas para prever ou explicar as variações que ocorrem na variável dependente (ou variável alvo). Com base na relação estimada entre essas variáveis, o analista pode compreender correlações e realizar previsões. Como exemplo, suponhamos que estamos interessados em prever o consumo de energia (variável dependente) em uma determinada cidade. As possíveis variáveis explicativas poderiam ser: número de pessoas residentes nesta cidade, temperatura máxima e mínima. 

**Variável de data** 

Variável indicativa de data, onde será identificado a frequência dos dados. 

#### Enriquecendo o seu dataset

Para enriquecer o seu conjunto de dados e impulsionar suas projeções, você pode usar o poder dos dados da Feature Store, escolhendo séries recomendadas pelo Pick4me ou utilizando alguma série favorita. Para mais informações sobre, acesse o documento [Integrando com a Feature Store](/pt-br/time-series/intro/integracao-fs.md). 

Há também a opção de adicionar defasagem nas suas variáveis. Entenda mais sobre essa configuração no documento sobre [Lags](/time-series/modelagemg/lags.md).

### 2) Passo 3

Na última etapa, defina qual o período da sua projeção você deseja otimizar. 

Agora já é possível iniciar o processo de modelagem para os seus dados. Porém, em caso de necessidade, ainda é possível realizar alguns ajustes finos. Entenda quais os ajustes disponíveis no documento de [Ajustes Finos](/time-series/modelagem/ajustes-finos.md).  

