# Número Reprodutivo Básico $\(\mathcal{R}_0\)$ – Modelo Geral (Dengue)

Este repositório implementa o cálculo e a **análise de sensibilidade global** do número reprodutivo básico $\(\mathcal{R}_0\)$ de um modelo imune‑viral para dengue, usando amostragem **eFAST/FAST99** sobre um grande espaço de parâmetros biológicos.

## Visão geral

A expressão analítica de $\(\mathcal{R}_0\)$ considerada é

$$
\mathcal{R}_0 =  \dfrac{1}{\gamma_{Y}}\dfrac{\Omega}{\gamma_{X}}
\left(\dfrac{\Phi}{\xi_{1} \dfrac{\Lambda}{\gamma_{A}} + \gamma_{V}}\right)
\left(\beta_{1} \dfrac{\theta_{1}^{n-p}\left(\dfrac{\Lambda}{\gamma_{A}}\right)^{p}}{\theta_{1}^{n} + \left(\dfrac{\Lambda}{\gamma_{A}}\right)^{n}}+\beta_{2}\right).
$$

O código trabalha com combinações de parâmetros epidemiológicos/imunológicos (produção de anticorpos, células suscetíveis, partículas virais, taxas de infecção etc.) e estima como a incerteza em cada parâmetro afeta $\(\mathcal{R}_0\)$.

## O que o código faz

- Define o **problema de sensibilidade** para 11 parâmetros (incluindo um `dummy`) em escala logarítmica.
- Gera $\(10^5\)$ amostras de parâmetros usando o **FAST sampler** da biblioteca `SALib`.
- Implementa a função vetorizada `calc_R0(Y)` para cálculo rápido de $\(\mathcal{R}_0\)$.
- Calcula estatísticas descritivas de $\(\mathcal{R}_0\)$ e plota:
  - Gráfico de barras com os **índices de sensibilidade total (ST)** para cada parâmetro.
- Usa o parâmetro `dummy` como **limiar de significância**, destacando quais parâmetros têm influência relevante sobre \(\mathcal{R}_0\).

## Principais parâmetros

O estudo é feito em termos de:

- $\(Q_1 = \Lambda / \gamma_A\)$: anticorpos em equilíbrio.
- $\(Q_2 = \Omega / \gamma_X\)$: células alvo em equilíbrio.
- $\(\Phi\)$: produção de partículas virais.
- $\(\beta_1, \beta_2\)$: taxas de infecção/contágio.
- $\(\xi_1\)$: termo de consumo de vírus pela formação de complexos antígeno‑anticorpo.
- $\(\gamma_Y, \gamma_V\)$: remoção de células infectadas e partículas virais.
- $\(n, p\)$: expoentes de Hill na função de ocupação de receptores.
- `dummy`: parâmetro artificial usado como base para comparação de significância.

Os intervalos de cada parâmetro são derivados de dados da literatura e detalhados na tese associada.


## Interpretação dos resultados

- `Si['S1']`: índice de **primeira ordem** (efeito direto de cada parâmetro).
- `Si['ST']`: índice de **efeito total** (efeito direto + interações).
- Parâmetros com `ST` maior que o `dummy` são considerados **influentes**.
- No exemplo apresentado, parâmetros agregados como `Q1`, `Q2`, `xi1`, `Phi`, `beta1`, `beta2` e `gammaY` se destacam como principais determinantes de $\(\mathcal{R}_0\)$, enquanto expoentes de Hill (`n`, `p`) e \(\gamma_V\) têm influência relativamente menor.

## Aplicações

- Estudo da **robustez** do modelo de dengue em relação à incerteza paramétrica.
- Modelagem matemática em epidemiologia.
- Análise de sensibilidade global (eFAST/FAST99).
- Interpretação biológica do número reprodutivo básico.

## Referência principal

A fundamentação teórica do modelo e dos intervalos de parâmetros pode ser encontrada na tese de doutorado associada. Disponível em:  
https://repositorio.unesp.br/server/api/core/bitstreams/8ae4b41f-3490-4972-8755-878082b36789/content


