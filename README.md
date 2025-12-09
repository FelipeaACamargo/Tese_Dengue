# Modelo Matemático de Dengue Grave em Adultos e Crianças

Implementação em Python de um modelo de equações diferenciais ordinárias (EDOs) que descreve a dinâmica da infecção por dengue durante uma segunda infecção (heteróloga), considerando anticorpos neutralizantes e não neutralizantes, com ênfase em dengue grave em adultos e crianças.

## Descrição do modelo

O código implementa um sistema não linear de 5 EDOs para as variáveis: anticorpos de reação cruzada $\(A_1\)$, anticorpos neutralizantes $\(A_2\)$, células-alvo suscetíveis $\(X\)$, células infectadas $\(Y\)$ e vírus livres $\(V\)$.
As funções de aprimoramento $\(E(A_1)\)$ e neutralização $\(N(A_2)\)$ são modeladas por funções de Hill, permitindo estudar efeitos de ADE (*antibody-dependent enhancement*) e neutralização parcial na carga viral. 

## Principais funcionalidades

- Implementação do modelo completo de 5 equações diferenciais com parâmetros biológicos calibrados a partir da literatura. 
- Implementação do método de Runge–Kutta de 4ª ordem (RK4). 
- Rotinas de solução numérica com `scipy.integrate.solve_ivp` usando métodos apropriados para sistemas stiff: `Radau` e `LSODA`. 
- Geração de gráficos (matplotlib) da Dinâmica Populacional

## Estrutura do código

- Definição dos parâmetros biológicos 
- Função `ModeloGeral(t, u)` que retorna o vetor \((dA_1/dt, dA_2/dt, dX/dt, dY/dt, dV/dt)\) 
- Implementação de:
  - `RungeKutta4(f, s0, h, tf)` (método explícito clássico). 
  - `solve_ode_radau(f, s0, h, tf)` (método implícito Radau com passo adaptativo). 
  - `solve_ode_lsoda(f, s0, h, tf)` (LSODA, alternando automaticamente entre regimes stiff e não-stiff).
- Blocos de simulação separados para RK4, Radau e LSODA, todos com mesmas condições iniciais e parâmetros. 

## Análises implementadas

- Discussão numérica da rigidez (stiffness) do sistema e comparação qualitativa entre RK4 e métodos stiff. 
- Cálculo e visualização dos picos de anticorpos, células e carga viral, com marcação de máximos, interseções e geração de uma tabela de resumo em Markdown. 
- Estudo numérico da influência dos parâmetros $\(\theta_1\)$ (aprimoramento) e $\(\theta_2\)$ (neutralização) na intensidade e duração da viremia, incluindo interpretação biológica desses limiares. 

## Como executar

1. Copiar ou baixar o repositório e abrir o arquivo `.py` ou notebook correspondente.
2. Garantir as dependências instaladas:
   - `numpy`
   - `matplotlib`
   - `scipy` 
3. Executar o script para gerar as simulações (14 dias) usando RK4, Radau e LSODA, visualizando os gráficos gerados. 

## Aplicações

- Material para uso:
  - Equações Diferenciais Ordinárias.
  - Modelagem Matemática em Epidemiologia.
  - Métodos Numéricos para EDOs (incluindo problemas stiff). 
- Base computacional para estender o modelo a cenários clínicos (adultos vs. crianças), calibração de parâmetros e análise de sensibilidade em ADE/neutralização.

## Referências
- Tese: https://repositorio.unesp.br/server/api/core/bitstreams/8ae4b41f-3490-4972-8755-878082b36789/content
- Artigo: https://link.springer.com/article/10.1007/s11538-021-00919-y
