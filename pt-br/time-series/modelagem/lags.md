# Variáveis defasadas
## Definição

Uma variável defasada (lag) é uma variável construída de tal forma que seus valores sejam os números provenientes de períodos anteriores na série temporal. 

Podemos defasar uma variável tanto quanto tivermos períodos de tempo para isso, mas é importante notar que, a cada vez que você defasa uma variável, perde-se a observação mais antiga. Se você desejar defasar duas vezes, perderá as duas observações mais antigas. O número de períodos passados que você deseja defasar é chamado de "ordem de defasagem". 

A tabela abaixo mostra o exemplo para as ordens de defasagem um (l1_vendas) e dois (l2_vendas). 

|       Data           |      Vendas  |      l1_Vendas  |      l2_Vendas  |
|----------------------|:------------:|:---------------:|:---------------:|
|      Dezembro/2021   |     100      |     -           |     -           |
|      Janeiro/2022    |     108      |     100         |     -           |
|      Fevereiro/2022  |     110      |     108         |     100         |
|      Março/2022      |     105      |     110         |     108         |
|      Maio/2022       |     106      |     105         |     110         |
|      Abril/2022      |     100      |     106         |     105         |
|      Junho/2022      |     112      |     100         |     106         |
|      Julho/2022      |     115      |     112         |     100         |

Variáveis defasadas são importantes quando desejamos considerar a influência direta do passado no modelo. Por exemplo, ao decidir o nível de estoque de um produto em uma loja para o próximo mês, você considera as vendas desse produto no mês anterior. 

## Aplicação

É possível adicionar automaticamente variáveis defasadas (lags) das variáveis explicativas ao seu conjunto de dados de modelagem em nossa plataforma. Ao longo do pipeline, o algoritmo escolherá a ordem de atraso com maior correlação com a variável dependente e a adicionará ao conjunto de dados. Este conjunto de dados seguirá para nossas etapas regulares de seleção de recursos (se apropriado) e modelagem. 

**Aqui estão algumas regras que você deve ter em mente:**

- Variáveis com atraso são adicionadas ao conjunto de dados com o prefixo 'l', seguido do número de atraso e do nome da variável original. Por exemplo, ao aplicar um atraso de 2 à variável 'x1', a variável 'l2_x1' será criada. 

<!-- - Atualmente, não é possível adicionar versões defasadas de variáveis categóricas ou variáveis indicadoras (consulte 'Variáveis categóricas' para entender quais variáveis se enquadram nessa categoria).  -->

- Variáveis com atraso são adicionadas ao conjunto de dados depois que todas as imputações e pré-processamentos foram aplicados, o que significa que se a variável original tiver valores ausentes, sua versão defasada terá os mesmos valores imputados para eles. 

- Valores ausentes adicionados devido a variáveis defasadas não são preenchidos por nenhum método. Isso implica que se o atraso 'x' (por exemplo, 5) foi adicionado ao seu conjunto de dados, as primeiras 'x' linhas do conjunto de dados serão excluídas. 

- Ao trabalhar com conjuntos de dados próximos ao limite de pontos de dados requeridos (consulte a documentação de [requisitos](/help-center/time-series/intro/requisitos.md), pode haver uma limitação para o número de defasagens das variáveis explicativas que você pode adicionar ao conjunto de dados. Você só poderá adicionar ordens de defasagem que não reduzam o número de pontos de dados abaixo do mínimo exigido. Se a defasagem selecionada for maior que o máximo permitido, aparecerá um aviso. 

- Para todos as defasagens de cada variável explicativa, é realizada uma busca de defasagem escolhendo a ordem de defasagem com maior correlação com a variável dependente. A menos que a variável defasada seja escolhida como uma Variável de Ouro, não há garantia de que ela aparecerá nos modelos, uma vez que a seleção regular de recursos/modelos (se apropriada) é realizada. 
<!-- TODO: documentação golden variables e incluir links aqui -->
- Se uma ou mais variáveis com defasagem forem escolhidas como Variáveis de Ouro, a busca de defasagem para essa variável explicativa será ignorada, e as variáveis com defasagem funcionarão como qualquer Variável de Ouro. No entanto, as variáveis não serão incluídas se as variáveis com defasagem não estiverem disponíveis (devido ao número mínimo de pontos de dados ou a outros detalhes de pré-processamento). 
<!-- TODO: documentação exclusions e incluir links aqui -->
- Qualquer variável com defasagem incluída no conjunto de dados pode ser usada como Exclusão. 