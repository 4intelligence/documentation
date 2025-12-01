# Cálculo de Impactos: Simulado e Analítico

## Interpretação de Modelos: Cálculo de Impactos

No módulo **AI Models**, nós entregamos mais do que a previsão ("o que vai acontecer"). Entregamos a explicação matemática por trás dela ("por que vai acontecer").

A plataforma oferece duas lentes distintas para interpretar os resultados: **Impacto Simulado** e **Impacto Analítico**. Ambas respondem à pergunta "o que moveu meu número?", mas sob óticas diferentes.

---

#### **1. Impacto Simulado (Visão Diagnóstica)**

_Aprofunde-se na dinâmica, nas interações e nas causas da variação._

> **ℹ️ O que é?**

O Impacto Simulado é uma ferramenta de **diagnóstico explicativo** desenhada para entender **por que o resultado mudou de um período para outro**.

Baseado na tecnologia **SHAP (SHapley Additive exPlanations)**, o algoritmo realiza milhares de simulações que constroem cenários alternativos: ele "liga" e "desliga" cada variável e combina suas diferentes configurações. Esse processo permite **isolar a contribuição individual de cada fator**, ao mesmo tempo em que captura **interações complexas** que influenciam o resultado.

> **ℹ️ Valor Gerado**

**Diagnóstico de Causa Raiz:**  
Revela, de forma precisa, os fatores que explicam por que o número atual ficou acima ou abaixo do período anterior. A análise considera não apenas o efeito de cada variável isoladamente, mas também como elas interagiram naquele momento específico.

**Leitura do Movimento:**  
Foca na dinâmica da mudança. Em vez de olhar apenas o valor final, mostra **como** e **por que** o resultado se deslocou entre os períodos.

ℹ️**Quando utilizar?**

- Use quando sua pergunta for **comparativa**, especialmente quando há interações relevantes:

- “Por que minhas vendas caíram em relação ao ano passado, se o preço se manteve estável?”

- “Qual foi a contribuição exata da sazonalidade para a alta deste mês?”

- “Quais fatores explicam uma mudança inesperada no resultado?”

---

#### **2. Impacto Analítico (Visão Estrutural)**

_Entenda como cada variável afeta o resultado de forma direta._

> **ℹ️ O que é?**

O Impacto Analítico é uma ferramenta de leitura estrutural do modelo. Ele mostra **como a mudança das variáveis explicativas entre dois períodos influencia o resultado**, usando diretamente os **coeficientes estimados** pelo modelo.

O algoritmo atribui a cada fator a parcela exata do movimento que ele provoca no resultado — sem a necessidade de simulações ou combinações alternativas.

Essa abordagem revela o _efeito direto_ de cada variável segundo o próprio modelo estatístico, permitindo interpretar a sensibilidade do resultado a mudanças específicas.

ℹ️**Valor Gerado**

**Transparência Estrutural:**  
Mostra de forma objetiva a contribuição de cada variável, refletindo exatamente a lógica interna do modelo (especialmente útil em modelos lineares ou com elasticidades conhecidas).

**Compreensão de Sensibilidades:**  
Permite entender o “quanto o resultado mexe” quando cada variável sobe ou desce.

**Estabilidade na Interpretação:**  
Ideal quando você quer uma decomposição direta, previsível e fácil de replicar em diferentes períodos.

**Quando utilizar?**

Use quando sua pergunta for sobre **sensibilidade ou efeito direto**:

- “Quanto da variação do faturamento veio especificamente do aumento de clientes ativos?”

- “Se o preço subiu 3%, qual parte da mudança no resultado é explicada só por isso?”

- “Quero ver a decomposição exata, sem simulações — apenas o impacto direto de cada variável.”

🧩 **Glossário de Componentes**

_Ao analisar qualquer uma das visões (Simulada ou Analítica), você encontrará componentes que explicam a dinâmica da série temporal:_

- **Sazonalidade (Seasonal):** A soma dos efeitos cíclicos (como mês do ano ou dias da semana, dependendo da frequência dos dados).

- **Persistência (Persistence):** A "inércia" ou memória da série. Mostra quanto do resultado atual é reflexo da tendência recente (derivado dos componentes AR e MA).

- **Efeitos Pontuais (One-off):** O impacto de _outliers_ ou eventos atípicos que geram desvios momentâneos na curva.

- **Mudança de Patamar (Level Effects):** Alterações estruturais no nível da série que perduram por mais de um período (comuns quando há pontos de outlier em modelos diferenciados).

- **Variáveis Explicativas:** O impacto das variáveis externas (Preço, PIB, Clima) inseridas no modelo.

---

> **✅ Resumo Comparativo: Qual metodologia escolher?**

Embora ambas mostrem o impacto das variáveis, elas funcionam de formas diferentes. Veja qual se adapta ao seu objetivo:

| **Característica**        | **🔮 Impacto Simulado (SHAP)**                                              | **📐 Impacto Analítico (Coeficientes)**                                            |
| ------------------------- | --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Foco Principal**        | Dinâmica e Interações                                                       | Estrutura e Fórmula                                                                |
| **Como calcula?**         | **Simulação:** Cria cenários alternativos ("ligando/desligando" variáveis). | **Fórmula:** Aplica a diferença da variável diretamente ao coeficiente da equação. |
| **Considera Interações?** | **Sim.** Captura como uma variável afeta a outra (efeitos conjuntos).       | **Não.** Isola o efeito conforme a estrutura linear do modelo.                     |
| **Aplica-se a...**        | Modelos simples ou complexos (Lineares e Machine Learning).                 | Apenas modelos com forma fechada (Lineares/ARIMA).                                 |
| **A Resposta é...**       | _"Quanto esta variável contribuiu, considerando todo o contexto?"_          | _"O que a fórmula matemática diz sobre esta variável?"_                            |
