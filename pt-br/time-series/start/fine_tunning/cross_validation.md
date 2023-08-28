# Cross-validation
## O que é e como fazemos

A validação cruzada é uma técnica usada para garantir que os modelos possam generalizar bem, evitando o que é chamado de overfitting (quando um modelo funciona bem com dados conhecidos, mas mal quando exposto a novos dados). Essa técnica consiste em reamostrar os dados fornecidos em diferentes conjuntos de treinamento e teste para avaliar como o modelo se comporta nessas diferentes combinações de subamostras. 

Existem vários tipos de validação cruzada, mas para séries temporais usamos a validação cruzada deslizante (rolling cross-validation), na qual as amostras são tomadas em ordem e o modelo é treinado e faz previsões N passos à frente, onde N é o horizonte de previsão fornecido. O processo de subdivisão do conjunto de dados original pode ser visto abaixo: 


Após todas as iterações serem concluídas, as medidas de precisão são resumidas pelo valor médio ou mediano dos resultados obtidos em cada iteração (o que chamamos de janela), e esses são os resultados fornecidos para cada modelo na previsão final. 
