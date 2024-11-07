# Regressão Regularizada

As regressões regularizadas são métodos projetados para reduzir os coeficientes em direção a zero, penalizando coeficientes maiores na função de perda. A ideia é que esse tipo de modelo generalize melhor, uma vez que cada regressor contribui um pouco para o resultado, obtendo resultados mais "suaves". As regularizações podem ser do tipo L1 (Lasso) ou L2 (Ridge), com o ElasticNet combinando ambos.

Os tipos L1 e L2 impõem uma penalização na função de perda, que é proporcional ao tamanho dos coeficientes absolutos para L1 e quadrático para L2. O modelo Lasso representa a regularização L1 e o Ridge L2, sendo que o Lasso pode reduzir os coeficientes a zero, e o Ridge pode reduzi-los em direção a zero, mas nunca alcançando-o completamente. Há um parâmetro, _lambda_, que controla o grau dessa penalidade; se ele tender ao infinito, os coeficientes se moverão em direção a zero.

O ElasticNet combina L1 e L2 e possui um parâmetro adicional, _alpha_, que é uma espécie de peso dado para L1, com seu peso "correspondente" proporcional a _1 - alpha_ para L2.