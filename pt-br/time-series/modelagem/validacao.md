# Validação

Nessa seção, vamos abordar algumas validações feitas durante o pré-processamento de uma modelagem.

## Dimensão dos dados

### Linhas

Pontos de dados podem ser descartados de um conjunto de dados devido a valores ausentes nas variáveis dependentes ou explicativas: 

- Qualquer valor ausente da variável dependente antes de sua primeira ocorrência é removido do conjunto de dados (resultando na exclusão da linha inteira). Valores ausentes entre a primeira e a última ocorrência são preenchidos usando o Filtro de Kalman com matrizes derivadas de um ARIMA univariado, exceto para conjuntos de dados com frequência diária, caso em que a observação é descartada. 

- As linhas no início do conjunto de dados com mais de 20% de valores ausentes para as variáveis explicativas são eliminadas do conjunto de dados. 

### Colunas 

Com o objetivo de evitar a imputação de um alto percentual de valores ausentes, variáveis com mais de 20% de valores ausentes no período de modelagem (ou seja, pontos de dados nos quais valores para a variável dependente estão disponíveis) são removidas do conjunto de dados. Se você tiver tais variáveis em seu conjunto de dados, receberá um aviso indicando as variáveis que foram removidas do conjunto de dados devido a um alto percentual de valores ausentes. 

## Métodos de imputação de dados

Nossa plataforma remove automaticamente as variáveis redundantes do conjunto de dados. Variáveis redundantes são características cujas informações já estão completamente contidas em outras variáveis. Tecnicamente, elas são chamadas de variáveis linearmente dependentes. 

A dependência linear é um conceito matemático que afirma que uma variável é linearmente dependente se pudermos compor essa variável com uma ou qualquer combinação linear de outras séries temporais dentro do conjunto de dados. É importante removê-las, pois isso acelera o tempo de processamento e também é necessário para a estimativa de alguns modelos, que dependem de métodos que requerem inversão de matriz. 

Você pode verificar na plataforma as variáveis que foram excluídas do conjunto de dados por meio de uma mensagem de aviso que aparece na tela durante a criação de um projeto. 
