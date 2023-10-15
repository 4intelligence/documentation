# Ajustes finos

## **Cross-validation**

A validação cruzada é uma técnica usada para garantir que os modelos possam generalizar bem, evitando o que é chamado de *overfitting* (quando um modelo funciona bem com dados conhecidos, mas mal quando exposto a novos dados). Essa técnica consiste em reamostrar os dados fornecidos em diferentes conjuntos de treinamento e teste para avaliar como o modelo se comporta nessas diferentes combinações de subamostras. 

Existem vários tipos de validação cruzada, mas para séries temporais usamos a validação cruzada deslizante (rolling cross-validation), na qual as amostras são tomadas em ordem e o modelo é treinado e faz previsões N passos à frente, onde N é o horizonte de previsão fornecido. O processo de subdivisão do conjunto de dados original pode ser visto abaixo: 

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/time-series/modelagem/img/cross_validation.png)

Após todas as iterações serem concluídas, as medidas de precisão são resumidas pelo valor médio ou mediano dos resultados obtidos em cada iteração (o que chamamos de janela), e esses são os resultados fornecidos para cada modelo na previsão final. 

**Horizonte de Previsão (*n_steps*) + Janela de Teste (*n_windows*)** 

O Horizonte de Previsão, ou *n_steps*, é o tamanho do conjunto de teste na validação cruzada, que deve ser baseado no número de observações a serem previstas. Por outro lado, o parâmetro de janela de teste, ou *n_windows*, descreve quantas vezes o modelo aplicará a validação cruzada no conjunto de dados. 

## Log

**Quando e por quê?**

Log é a abreviação para o logaritmo natural. A transformação logarítmica é uma transformação de dados na qual o valor original é substituído por seu logaritmo natural. Para aplicar a transformação logarítmica, a variável deve ter apenas valores estritamente positivos, ou seja, nem zeros nem números negativos. 

É frequentemente usado em modelagem quantitativa devido às suas propriedades matemáticas convenientes. Quando aplicado, o logaritmo natural reduz a escala da variável sem alterar as relações entre as observações dentro e entre as séries. Uma vantagem da transformação logarítmica é a tendência de reduzir o impacto de valores discrepantes (outliers) e diminuir a variância da série. 

Para modelos lineares, como o ARIMA, a transformação logarítmica implica que interpretamos os coeficientes estimados como elasticidades, quando tanto as variáveis dependentes quanto as independentes estão em logaritmo (também chamados de modelos log-log), ou como semi-elasticidade, quando apenas a variável dependente está em logaritmo (também chamados de modelo log-linear). 

\* Valores discrepantes (outliers) podem enviesar a estimativa dos coeficientes. 

** A redução na variância da variável pode auxiliar nos testes de hipóteses estatísticas. 

**Nossas Regras** 

Na plataforma, existe a possibilidade de aplicar a transformação logarítmica às variáveis no conjunto de dados. O padrão é tentar aplicar a transformação logarítmica a todas as variáveis permitidas, ou seja, séries temporais sem zeros ou números negativos. 

Se você tiver ambos os tipos de variáveis no conjunto de dados, a transformação é aplicada apenas às permitidas. 

Para as variáveis sem transformação logarítmica, é adicionado o prefixo "z_" ao nome (por exemplo, z_gap). Dessa forma, você pode identificar facilmente as variáveis tratadas no formato original. 

É importante destacar que não se aplica a transformação logarítmica a variáveis indicadoras, como valores discrepantes (outliers), variáveis sazonais ou qualquer tipo de variável dicotômica 0-1. 

## Sazonalidade

Dentro do pipeline, a sazonalidade é tratada como aditiva, com a inclusão de variáveis explicativas categóricas para cada período dos dados (com o prefixo 'd4i_'). 

A sazonalidade aditiva assume que o efeito das janelas sazonais permanece constante ao longo do tempo. Por exemplo, modelar uma variável dependente mensal com essa abordagem assume que, apesar das mudanças na tendência, o tamanho do efeito na variável a cada dezembro é mais ou menos o mesmo ao longo dos anos. 

As variáveis indicadoras sazonais adicionadas ao conjunto de dados aparecerão com o prefixo 'd4i_', e o tipo de variáveis indicadoras depende da frequência dos dados, como: 

- Para dados mensais, semanais e quinzenais, é adicionada uma variável indicadora para cada mês do ano. 

- Para dados bimensais, é adicionada uma variável indicadora para cada bimestre do ano. 

- Para dados trimestrais, é adicionada uma variável indicadora para cada trimestre do ano. 

- Para dados semestrais, é adicionada uma variável indicadora para cada semestre do ano. 

- Para dados anuais, nenhuma variável indicadora é adicionada. 

- Para dados diários, é adicionada uma variável indicadora para cada mês do ano, bem como uma variável indicadora para cada dia da semana (isso é chamado de sazonalidade múltipla). 

Exceto para o modelo de Random Forest, uma linha de base é sempre removida das variáveis indicadoras sazonais, evitando a dependência linear entre as variáveis explicativas e o intercepto. 

<!-- TODO: finalizar -->