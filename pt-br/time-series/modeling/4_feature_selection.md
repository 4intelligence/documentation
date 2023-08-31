# Feature Selection


## Ideia geral  

A seleção de características tem como objetivo escolher as características (variáveis) contínuas mais relevantes a partir do conjunto de opções disponíveis, reduzindo a dimensionalidade da matriz de regressores, o que geralmente é um problema para a convergência do modelo. 

O motor de modelagem realiza uma busca exaustiva pela melhor combinação de características (que cresce exponencialmente com o número de variáveis) e, ao reduzir a dimensionalidade, permite uma busca de modelo mais focada. 

Por fim, em muitos casos, existem mais características do que valores observados, o que pode ser um problema na identificação dos parâmetros do modelo; a seleção de características reduz a probabilidade de tal problema ocorrer. 

## Métodos 

**Random Forest (Floresta Aleatória)** 

Após ajustar uma floresta aleatória, as características são embaralhadas, uma por uma, e o aumento no Erro Quadrado Médio (MSE) é calculado. Variáveis que levam a maiores variações no MSE são consideradas mais importantes do que outras. É gerado um ranking que é reduzido para selecionar o número desejado de variáveis. 

**Filtro de Correlação de Pearson** 

Funciona filtrando primeiro as variáveis com uma correlação absoluta maior que 0,2 com a variável dependente (resposta). Com esse subconjunto, ele inicia uma análise em pares das características mais correlacionadas, obtendo o par mais correlacionado e eliminando a característica com menor correlação absoluta com a variável dependente, repetindo esse processo até que o número de características seja reduzido ao desejado. 

**Lasso** 

Executa um modelo Lasso com dados padronizados. Como os dados são padronizados, os coeficientes podem ser usados para medir a "relevância da variável", e ao ordenar os coeficientes, é possível selecionar as principais N características. O Lasso é interessante, pois retorna um coeficiente igual a zero para as características menos "prominentes". 
