# Entendendo as Regiões

Nessa seção, vamos abordar como a Feature Store organiza os dados de acordo com o local ao qual o dado se refere.

## O que são as Regiões da Feature Store?

Toda série temporal ou conjunto de dados está associado a um local específico, onde as observações, ou dados brutos, foram coletadas. O componente de região da Feature Store indica esse local ao qual as séries se associam.

Por exemplo, além de mensurar o <a href="https://app.4intelligence.ai/feature-store/indicators/BRGDP0081" target="_blank" rel="noreferrer">Produto Interno Bruto (PIB)</a> do país como um todo, há também quebras regionais que quantificam o PIB por grande região e por estado. A visão regional nos permite compreender como diferentes partes do país contribuem para a economia nacional e identificar tendências e desafios regionais específicos.

Cada uma dessas quebras regionais, assim como o dado nacional, caracterizam séries diferentes dentro de um mesmo indicador da Feature Store. Essas séries são identificadas no componente região através do nome da localidade.

## Quais são as Regiões disponíveis na Feature Store?

Indicadores sobre economia e clima brasileiros compõem a maior parte dos dados disponibilizados pela Feature Store. Para esses indicadores, há grande variedade de quebras regionais, como grandes regiões, estados, região metropolitana e até municípios. A disponibilidade de regiões para um indicador depende do contexto de geração dos dados.

Há também indicadores de economia internacional, com foco em países da América Latina, como Argentina, Chile, Colombia, Equador, Peru e México, e grandes economias, como Estados Unidos, China e União Europeia. Nesses casos, a Feature Store dispõe majoritamente de indicadores no nível nacional.

No entanto, existem conjuntos de dados que não estão vinculados a um local específico, mas sim a contextos mais amplos. Considere o <a href="https://app.4intelligence.ai/feature-store/indicators/WDPRC0118" target="_blank" rel="noreferrer">Índice de Commodities CRB</a>, que acompanha a evolução das cotações internacionais de uma cesta de produtos. Nesse caso, o indicador não está ligado a um único local, mas sim ao comércio internacional, por isso, a Feature Store indica Mundo como região.

<style>
blue4i {
  color: #4C94FF;
}
</style>

<blue4i>**No [próximo artigo](/help-center/feature-store/data-organization/frequencia.md), você entenderá como a Feature Store organiza os dados de acordo com a sua periodicidade e como transformar a periodicidade dos dados.**</blue4i>
