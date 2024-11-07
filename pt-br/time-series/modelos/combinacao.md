# Combinação de Modelos

Conforme o nome sugere, os métodos de combinação de previsões combinam valores previstos por diferentes modelos, seja linearmente ou usando técnicas mais sofisticadas, para gerar novas previsões. Atualmente, é testada a combinação dos 10 melhores modelos de acordo com o critério de acurácia escolhido pelo usuário (como o "MAPE"), de modo que os modelos 1 e 2 sejam combinados e métricas sejam calculadas, depois 1, 2 e 3 são combinados, e assim por diante. Todos os métodos são executados para cada combinação. Para cada técnica, é escolhida a combinação com o melhor critério escolhido pelo usuário.

Para simplificar a explicação dos métodos usados, eles foram divididos em 3 blocos: A) Métodos Simples; B) Métodos de Regressão; C) Abordagem de Autovetores.

### A) Métodos Simples

- **Bates/Granger (1969) - comb_BG**

Ideia principal: Ponderar as previsões usando o inverso do erro médio quadrado da previsão (média da diferença ao quadrado entre a previsão e os valores reais).

- **Combinação de Previsão de Classificação Inversa - comb_invW**

Ideia principal: Classificar o modelo com a menor previsão de erro quadrado médio como 1, o segundo menor como 2, etc. Em seguida, pegar a classificação inversa e verificar seu peso dividindo a classificação inversa pela soma das classificações inversas.

<!-- - **Combinação de Previsão Mediana - comb_MED**

Ideia principal: Usar a mediana das previsões em cada ponto no tempo. -->

- **Combinação de Previsão Média Simples - comb_SA**

Ideia principal: Usar a média das previsões em cada ponto no tempo.

<!-- - **Combinação de Previsão Média Aparada - comb_TA**

Ideia principal: Aparar um número desejado de modelos com base na classificação (MAE, MAPE ou RMSE) e tirar a média da previsão. Atualmente, é usado o RMSE. -->

<!-- - **Combinação de Previsão Média Winsorizada - comb_WA**

Ideia principal: Usar a média winsorizada das previsões em cada ponto no tempo. A ideia da média winsorizada é substituir os valores mais altos e mais baixos pelas observações mais próximas. -->

- **Combinação de Previsão Newbold/Granger (1974) - comb_NG**

Ideia principal: Semelhante a "Combinação de Previsão Padrão de Autovetor", mas impondo a restrição linear _e'w = 1_, em que _e_ é um vetor de uns.

### B) Métodos de Regressão

- **Combinação de Previsão de Mínimos Quadrados Ordinários - comb_OLS**

Ideia principal: O método OLS executa um modelo linear simples com interceptação usando as previsões como regressores e os valores reais como variável dependente.

- **Combinação de Previsão de Mínimos Quadrados Restritos - comb_CLS**

Ideia principal: Funciona como combinações de previsão de mínimos quadrados ordinários (_comb_OLS_), mas adiciona restrições: os pesos devem ser não negativos; os pesos devem somar um.

- **Combinação de Previsão de Desvio Absoluto Mínimo - comb_LAD**

Ideia principal: Funciona de forma semelhante a uma combinação por meio de mínimos quadrados ordinários, mas minimiza o valor absoluto dos erros em vez de erros ao quadrado. Este método é mais robusto a valores atípicos, pois a magnitude da penalização é menor do que erros ao quadrado.

### C) Abordagem de Autovetores

- **Combinação de Previsão Padrão de Autovetor - comb_EIG1**

Ideia principal: Minimizar o erro médio quadrado de previsão _(v)_ por meio de uma combinação linear (_w'((vv’)\*w_, em que _w_ é o vetor de peso). Se a restrição imposta for do formato _w'w = 1_, a solução é encontrar o menor autovetor, que por sua vez está associado ao menor autovalor.

- **Combinação de Previsão de Autovetor com Correção de Viés - comb_EIG2**

Ideia principal: Muito semelhante ao _comb_EIG1_, mas agora cada vetor de erro de previsão é subtraído de sua média, eliminando possíveis vieses.

- **Combinação de Previsão de Autovetor Aparada - comb_EIG3**

Ideia principal: Muito semelhante ao _comb_EIG1_, mas pré-seleciona os melhores modelos que entrarão na combinação de acordo com um critério de otimização: MAE, MAPE ou RMSE, e mantém o número de modelos definidos pelo algoritmo de otimização incorporado. Atualmente, é usado o RMSE.

- **Combinação de Previsão de Autovetor com Viés Aparado - comb_EIG4**

Ideia principal: Combina _comb_EIG2_ e _comb_EIG3_.