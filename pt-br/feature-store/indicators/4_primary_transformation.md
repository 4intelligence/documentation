# Entendendo as Transformações Primárias

Nessa seção, vamos abordar o que são transformações primárias, quais tratamentos desse tipo estão disponíveis na Feature Store, destacando porque esses tratamentos são importantes.

## O que são transformações primárias?

Nem sempre o dado bruto é suficiente para compreender um fenômeno de forma completa. Para compatibilizar os dados com o objetivo da análise utilizamos as transformações primárias. São tratamentos iniciais aplicados na série bruta, ou seja, sem tratamentos, para torná-los mais relevantes frente ao objetivo da análise.

Para entender melhor porque transformações primárias são importantes para fazer uma análise bem suscedida, considere os exemplos a baixo:

**Mercado de trabalho**: Imagine que você queria entender se o mercado de trabalho brasileiro está aquecido. Há vários indicadores que você pode utilizar para abordar essa questão de forma objetiva como a [taxa de desemprego](https://4casthub.ai/feature-store/indicators/BREMP0018), que quantifica é o percentual de pessoas desocupadas em relação às pessoas na força de trabalho. Por conta de características estruturais do mercado de trabalho brasileiro, esse indicador apresenta padrões contundentes que se repetem: aumento de desemprego no primeiro trimestre e redução no quarto trimestre. Padrões que se repetem de forma previsível em um período de tempo são denominados de sazonalidade. Para responder a pergunta, é preciso primeiro expurgar esses padrões repetitivos que dificultam a identificação de tendências.

**Crédito**: Suponha que você queira verificar se há maior disponibilidade de crédito na economia. Você pode utilizar o indicador de [saldo de crédito](https://4casthub.ai/feature-store/indicators/BRCRD0026) para abordar essa questão de forma objetiva. Devido a inflação, o valor do dinheiro tende a diminuir ao longo do tempo, logo, não é recomendado comparar o valor monetério do saldo de crédito ao longo do tempo de forma direta, afinal R\$10 em 2010 não compra os mesmos bens e serviços que R\$ 10 nos dias de hoje. Para responder a pergunta, é preciso primeiro realizar uma correção monetária.

## Quais são as transformações primárias disponíveis na Feature Store?

**1) Original**

-   Série bruta sem nenhum tratamento

**2) Real**

-   Série bruta com valores foram ajustados para levar em consideração mudanças no poder de compra da moeda devido à inflação ou deflação. Esse tratamento permite uma análise mais precisa das variações nos valores ao longo do tempo.
-   Tratamento recomendado para o exemplo análise de crédito

**3) Ajuste sazonal**

-   Série bruta sem padrões repetitivos já esperados devido a questões estruturais. Esse tratamento permite uma análise mais clara das tendências da série.
-   Tratamento recomendado para o exemplo de análise de mercado de trabalho

**4) Dados reais ajustados sazonalmente**

-   Série bruta com dois tratamentos, um para correção monetérias e outro para expurgar padrões sazonais.

Antes de concluir sua análise, atente-se também para as transformações secundárias. No próximo artigo, você encontra informações sobre essas transformações.
