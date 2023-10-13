# Entendendo as Projeções

Nessa seção, vamos abordar como são feitas as projeções que estão disponíveis na Feature Store

## O que são valores históricos e projeções?

Você já deve ter notado que alguns indicadores da Feature Store tem dois tipos de valores, representados graficamente por duas cores: azul e rosa. Os valores em azul são históricos e os valores em rosa são projeções.


**- Valores históricos:** Os valores históricos são dados realizados, ou seja, já observados. Esses dados são coletados diretamente da fonte primária através de *crawlers*. Os *crawlers* são robôs da 4intelligence que percorrem a internet automaticamente, visitando diferentes sites para coletar dados. Eles ainda realizam tratamentos e transformações nos dados para que você tenha informações diferentes criadas a partir do dado bruto realizado.

Caso você queira saber mais sobre esses tratamentos e transformações volte para os artigos sobre os indicadores e seus elementos.

**- Valores projetados:** Já os valores projetados são previsões do comportamento futuro de cada série de tempo. Baseando-se em conhecimentos setoriais, análise de conjuntura, tendências históricas e utilizando o nosso motor de modelagem, nossos especialistas constrõem essas projeções que são disponibilizadas na Feature Store.

Portanto, ao utilizar as projeções da Feature Store em suas análises e relatórios você está usufruindo dos ganhos de precisão proprocionados por nossos algoritmos preditivos.

## Como funciona o motor de modelagem?

O nosso motor de modelagem é um algoritmo que busca sempre encontrar o modelo que gera a previsão mais precisa sobre o futuro.

Por exemplo, imagine que você deseja prever quantas televisões serão vendidas no próximo ano e que você tenha 5 anos de dados históricos de vendas. 

O primeiro passo é deixar de lado os dados realizados do último ano, porque eles serão usados para medir a precisão das previsões. 

O segundo passo é reunir informações complementares, que ajudam a explicar o comportamento das vendas, como o preço médio de uma televisão, a renda média dos compradores, ocorrência de grandes eventos televisionados como a Copa do Mundo, entre outros. 

Depois de coletar todos esses dados, o terceiro passo é estimar vários modelos diferentes. Cada modelo é a combinação de uma técnica de modelagem e um conjunto de dados. Estime utilizando apenas o preço médio, depois utilizando preço médio e renda, depois estime outro modelo utilizando com renda e Copa do Mundo... E assim por diante, até exaurir todas as possibilidades de técnicas e dados. Nesse processo, dependendo de quantas possibilidades existem, é necessário estimar dezenas de milhares de modelos!

Finalmente, o último passo é construir projeções para aquele ano que foi deixado de lado lá no primeiro passo e verificar a precisão da projeção de cada modelo frente aos dados reais. 

Todos esses passos são executados de forma automática e otimizada pelo nosso algoritmo de modelagem, até mesmo a coleta de informações complementares. Dessa forma, garantimos que, dadas as informações e técnicas estatísticas disponíveis, construímos a maneira mais precisa de fazer projeções.

Para aqueles leitores que buscam informações mais técnicas, em breve, disponibilizaremos documentação técnica sobre os tipos de modelos que o nosso algoritmo é capaz de estimar, sobre a validação fora da amostra, sobre tratamentos nos dados como loglinearização e sobre feature selection.


## Com que frequência as projeções são atualizadas?

xxxxxxxxxxxxxxxxxxx

## Todos os indicadores da Feature Store tem projeção?

xxxxxxxxxxxxxxxxxxx

---CTA para próximo artigo---
