# Entendendo as Projeções

Nessa seção, vamos abordar xxxxxxxxxxxxxxxxxxx

## Dados históricos e projeções

Você já deve ter notado que alguns indicadores da Features tem dois tipos de valores, representados graficamente em duas cores diferentes, azul e rosa. Os valores em azul são históricos e os valores em rosa são projeções.

--- print gráfico com tabela ---

**- Valores históricos:** Os valores históricos são coletados diretamente da fonte primária através de *crawlers*. Esses *crawler* são robôs da 4intelligence que percorrem a internet automaticamente, visitando diferentes sites para coletar dados. Os nossos *crawlers* ainda realizam tratamentos e transformações no dados para que você tenha disponível informações diferentes criada a partir do dado bruto.

Caso você queira saber mais sobre esses tratamentos e transformações volte para os artigos sobre indicadores.

**- Valores projetados:** Já os valores projetados são previsões do comportamento futuro de cada série de tempo. Baseando-se em conhecimentos setoriais, comportamentos e tendências históricas e análise de conjuntura, e utilizando o nosso motor de modelagem, nossos especialistas, constrõem essas projeções que são disponibilizadas na Feature Store.

Portanto, ao utilizar as projeções da Feature Store em suas análises e relatórios você está usufruindo dos ganhos de acurácia proprocionados por nossos algoritmos preditivos.

## Com que frequência os valores históricos são atualizadas?

Os valores históricos são atualizados conforme a frequência de divulgação de novos dos dados brutos ou revisão pela fonte primária. 

Por exemplo, o Instituto Brasileiro de Geografia e Estatística (IBGE) é a fonte primária do [Índice de Preços ao Consumidor Amplo (IPCA)](https://4casthub.ai/feature-store/indicators/BRPRC0046), que é o principal indicador para mensurar inflação ao consumidor final no Brasil. Esse indicador tem frequência mensal, sendo que o IBGE divulga um novo valor a cada mês com a inflação referente ao mês imediatamente anterior. No mesmo dia, em que esse novo valor é divulgado, nossos *crawlers* o capturam e disponibilizam na Feature Store.

## Com que frequência as projeções são atualizadas?

xxxxxxxxxxxxxxxxxxx

## Todos os indicadores da Feature Store tem projeção?

xxxxxxxxxxxxxxxxxxx

---CTA para próximo artigo---
