# Entendendo as Transformações Secundárias

Nessa seção, vamos abordar o que são transformações secundárias, quais cálculos desse tipo estão disponíveis na Feature Store, destacando porque esses cálculos são importantes.

## O que são Transformações Secundárias?

Após entender se é necessário tratar os dados brutos para prosseguir com sua análise, ou seja, após selecionar uma transformação primária, seleciona-se a transformação secundária. Caso tenha dúvidas sobre as transformações primárias, retorne ao [artigo anterior](/help-center/feature-store/indicators/transformacao-primaria.md).

As transformações secundárias envolvem cálculos e manipulações adicionais que geram métricas mais específicas. Para entender melhor porque transformações secundárias são importantes para fazer uma análise bem sucedida, considere os exemplos abaixo:

**Finanças públicas**: Imagine que você precise avaliar a sustentabilidade do endividamento do governo brasileiro. Há vários indicadores que você pode utilizar para abordar essa questão de forma objetiva, como a [dívida bruta do Governo Geral](https://4casthub.ai/feature-store/indicators/BRPUB0020). Porém, para responder a questão, é recomendável comparar o volume da dívida com um outro indicador, o PIB, que indica o tamanho da economia. Portanto, a métrica a ser acompanhada é a dívida bruta como porcentagem do PIB. Tal métrica traz uma visão mais clara sobre a capacidade do governo de gerenciar a dívida pública.

**Atividade econômica**: Suponha que você queira inferir se os preços estão aumentando. Você pode utilizar o indicador [Índice de Preços ao Consumidor, o IPCA](https://4casthub.ai/feature-store/indicators/BRPRC0046), para abordar essa questão de forma objetiva. No entanto, o IPCA é um número-índice, e para calcular a inflação precisamos de uma transformação secundária. Calculando a variação percentual do IPCA contra o mês anterior, temos a inflação mensal e calculando a variação percentual do IPCA contra o mesmo mês do ano anterior, temos a inflação anual. Com essas métricas é possível acompanhar se os preços estão aumentando ou reduzindo em cada período.

## Quais são as Transformações Secundárias disponíveis na Feature Store?

As principais transformações secundárias são aquelas que constroem métricas para acompanhar variações ao longo do tempo, acumular valores dentro de algum período e fazer comparações. Porém, existem diversas transformações secundárias disponíveis na Feature Store, sendo que as transformações disponíveis para cada indicador variam de acordo com a natureza dos indicadores. Você não precisa se preocupar com curadoria dessas métricas, a 4intelligence já deixou os calculos prontos para você!

Abaixo você encontra as transformações secundárias mais comuns:

**1) Variações no tempo**

-   Variação percentual contra igual período do ano anterior.

-   Variação percentual contra período imediatamente anterior.

-   Cálculos recomendado para o exemplo de análise de atividade econômica.

**2) Valores acumulados no tempo**

-   Valor médio acumulado em 12 meses.

-   Soma dos valores acumulados em 12 meses.

**3) Comparativas**

-   Valor em porcentagem do PIB.

-   Cálculo recomendado para o exemplo de finanças públicas.

<style>
blue4i {
  color: #4C94FF;
}
</style>

<blue4i>**Agora você já conhece toda a organização e tratamentos de dados da Feature Store. [Qual série você irá incluir na sua análise?](https://4casthub.ai/feature-store/indicators)**</blue4i>
