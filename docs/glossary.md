# Glosario de Trading Cuantitativo y Data Science

Este documento reúne los principales conceptos financieros,
estadísticos y de ciencia de datos utilizados a lo largo del proyecto.

El glosario será actualizado progresivamente a medida que se incorporen
nuevos conceptos durante el desarrollo y evaluación de las estrategias.

---

## Retorno (Return)

Representa la variación porcentual del precio de un activo entre dos
momentos.

Para un período:

R(t) = (P(t) - P(t-1)) / P(t-1)

Ejemplo:

Si Bitcoin pasa de USD 100 a USD 105:

Return = (105 - 100) / 100 = 0.05 = 5%

Un retorno positivo representa un aumento del precio y uno negativo,
una disminución.

---

## Retorno diario (Daily Return)

Es el retorno de un activo entre dos observaciones diarias consecutivas.

En el proyecto se calcula mediante:

    btc["daily_return"] = btc["Close"].pct_change()

Los retornos permiten analizar las variaciones relativas del activo
en lugar de trabajar únicamente con sus precios absolutos.

---

## Volatilidad (Volatility)

La volatilidad mide la magnitud de las variaciones de los retornos de
un activo.

Habitualmente se utiliza la desviación estándar de los retornos:

    volatility = btc["daily_return"].std()

Una volatilidad elevada indica que los retornos presentan grandes
variaciones alrededor de su promedio.

En este proyecto, la volatilidad será utilizada como una de las
principales medidas de riesgo.

---

## Skewness (Asimetría)

Mide qué tan simétrica es la distribución de los retornos.

Interpretación general:

- Skewness ≈ 0: distribución aproximadamente simétrica.
- Skewness > 0: mayor extensión de la cola positiva.
- Skewness < 0: mayor extensión de la cola negativa.

Una asimetría negativa puede indicar una mayor presencia relativa de
movimientos negativos extremos.

---

## Kurtosis (Curtosis)

Mide características relacionadas con las colas de una distribución
y la presencia de observaciones extremas.

Pandas utiliza excess kurtosis:

- Kurtosis ≈ 0: similar a una distribución normal en esta medida.
- Kurtosis > 0: mayor presencia relativa de valores extremos.
- Kurtosis < 0: menor presencia relativa de valores extremos.

Una curtosis elevada puede indicar que los movimientos extremos son
más frecuentes de lo que sugeriría una distribución normal.

---

## Rentabilidad acumulada (Cumulative Return)

Representa cuánto habría aumentado o disminuido una inversión durante
un período completo considerando la capitalización de los retornos.

No se obtiene simplemente sumando los retornos diarios.

Se calcula mediante:

Cumulative Return = ∏(1 + R(t)) - 1

Ejemplo:

Una inversión de USD 1.000 con una rentabilidad acumulada del 50%
terminaría con:

USD 1.000 × 1.50 = USD 1.500

Esta métrica permitirá comparar el resultado total de nuestra
estrategia contra Buy & Hold.

---

## Buy & Hold

Estrategia de referencia que consiste en comprar un activo y
mantenerlo durante todo el período analizado, sin realizar operaciones
intermedias.

En este proyecto será utilizada como benchmark.

La pregunta no será únicamente:

"¿Nuestra estrategia genera ganancias?"

sino:

"¿Cómo se comporta nuestra estrategia comparada con simplemente
comprar Bitcoin y mantenerlo?"

---

## Benchmark

Es una estrategia o referencia utilizada para comparar el desempeño
de otra estrategia.

En la V1 del proyecto:

    Benchmark = Buy & Hold BTC

Esto permite determinar si la complejidad adicional de una estrategia
de trading aporta algún beneficio frente a una alternativa sencilla.

---

## Maximum Drawdown (MDD)

Representa la mayor caída porcentual experimentada desde un máximo
histórico del capital hasta un mínimo posterior.

Ejemplo:

Capital máximo: USD 10.000
Capital posterior: USD 7.000

Maximum Drawdown = -30%

Esta métrica permite responder:

"¿Cuál fue la peor caída que habría experimentado el capital durante
la estrategia?"

Es especialmente importante porque dos estrategias con rentabilidades
similares pueden haber asumido niveles de riesgo muy diferentes.

---

## Sharpe Ratio

Mide el retorno obtenido en relación con el riesgo asumido,
habitualmente utilizando la volatilidad como medida de riesgo.

De manera simplificada:

Sharpe Ratio =
(Retorno de la estrategia - Tasa libre de riesgo) / Volatilidad

Un Sharpe Ratio mayor indica una mayor cantidad de retorno por unidad
de volatilidad.

Debe interpretarse junto con otras métricas y no como una medida
completa del riesgo, especialmente cuando los retornos presentan
asimetría o colas pesadas.

---

## SMA — Simple Moving Average

Una media móvil simple representa el promedio del precio durante una
cantidad determinada de períodos.

Por ejemplo:

SMA 20 = promedio de los últimos 20 precios

SMA 50 = promedio de los últimos 50 precios

En la primera estrategia del proyecto se utilizarán SMA 20 y SMA 50
para intentar identificar tendencias del mercado.

---

## Backtesting

Proceso mediante el cual una estrategia de trading se ejecuta
simuladamente sobre datos históricos.

Permite estudiar cómo se habría comportado una estrategia en el pasado.

Un backtest debe considerar, entre otros factores:

- Retornos
- Riesgo
- Costos de transacción
- Drawdowns
- Número de operaciones
- Benchmark
- Sesgos en los datos

Un buen resultado histórico no garantiza resultados futuros.

---

## Long Position

Una posición long representa una posición que se beneficia cuando el
precio del activo aumenta.

En nuestra V1:

    signal = 1 → Long BTC
    signal = 0 → Fuera del mercado

Inicialmente no utilizaremos posiciones short.

---

## Feature Engineering

Proceso de creación de nuevas variables a partir de los datos
originales para representar información potencialmente útil.

Ejemplos que utilizaremos:

    Close
      ↓
    SMA 20
    SMA 50
    Volatilidad
    Retornos

Estas variables podrán utilizarse posteriormente para construir
señales y modelos cuantitativos.

---

## Trading Signal

A **trading signal** is a rule or condition used to determine whether a
strategy should enter, exit, or remain in a market position.

In this project, the signal is generated from the relationship between two
simple moving averages:

- `1` when SMA 20 > SMA 50.
- `0` when SMA 20 <= SMA 50.

The signal itself does not represent the executed position. The strategy
delays its application by one period to avoid look-ahead bias.

---

## Position

A **position** represents the actual market exposure of the strategy during
a given period.

In this project:

- `1` represents a long position in BTC.
- `0` represents being out of the market.

The position is obtained by shifting the trading signal by one period:

`position = signal.shift(1)`

This ensures that information from the current period is not used to
retroactively generate returns for that same period.

---

## Look-Ahead Bias

**Look-ahead bias** occurs when a backtest uses information that would not
have been available at the moment an investment decision was made.

This can artificially improve historical results and produce an unrealistic
evaluation of a strategy.

In this project, look-ahead bias is reduced by shifting the trading signal
by one period before calculating strategy returns.

---

## Transaction

A **transaction** represents an individual change in market position.

In this project:

- `+1` represents an entry into the market.
- `-1` represents an exit from the market.
- `0` represents no change in position.

An entry and a subsequent exit therefore represent two transactions, but
together they form one completed round trip.

---

## Transaction Costs

**Transaction costs** are expenses associated with buying or selling an asset.

They may include trading commissions, exchange fees, spreads, and other
execution-related costs.

In the current backtest, a hypothetical fixed cost of **0.10% per
transaction** is applied whenever the strategy changes position.

Transaction costs are deducted from the strategy return before calculating
the net cumulative performance.

---

## Slippage

**Slippage** is the difference between the expected execution price of a
trade and the price at which the trade is actually executed.

It can occur because prices move between the generation of a trading signal
and the execution of the corresponding order, particularly during periods
of high volatility or limited liquidity.

Slippage is not explicitly modeled in the current version of the backtest
and is considered one of its limitations.

---

## Gross Return

**Gross return** is the return generated by a strategy before deducting
transaction costs or other execution expenses.

In this project, `strategy_return` represents the daily gross return of the
SMA 20/50 strategy.

---

## Net Return

**Net return** is the return remaining after transaction costs or other
modeled expenses have been deducted.

In this project:

`strategy_return_net = strategy_return - transaction_cost`

The net return is used to estimate a more realistic version of the
strategy's historical performance.

---

## Annualized Volatility

**Annualized volatility** estimates the variability of returns over a
one-year horizon.

For daily returns, it is calculated as:

`annualized_volatility = daily_volatility × sqrt(periods_per_year)`

Because Bitcoin trades every day, this project uses **365 periods per year**.

Higher volatility indicates greater variability in historical returns, while
lower volatility indicates a less variable return series.

---

## Risk-Adjusted Return

**Risk-adjusted return** evaluates investment performance relative to the
amount of risk taken to obtain that return.

A strategy with a higher absolute return does not necessarily provide a
better relationship between return and risk.

In this project, the **Sharpe Ratio** is used as one measure of
risk-adjusted performance.

---

## Equity Curve

An **equity curve** represents the evolution of invested capital through
time according to a sequence of returns.

In this project, cumulative strategy and Buy & Hold returns are converted
into equity curves using compounded returns:

`equity = (1 + return).cumprod()`

A value of `7.43`, for example, represents approximately **7.43 times the
initial capital**, not a return of 743%.

The corresponding cumulative return is calculated as:

`cumulative_return = final_equity - 1`

---

## Peak

A **peak** is the highest value reached by an equity curve up to a given
point in time.

It can be calculated using the cumulative maximum of the equity curve:

`peak = equity.cummax()`

Peaks are used as the reference point for calculating drawdowns.

---

## Drawdown

A **drawdown** measures the decline of an investment from a previous equity
peak.

It is calculated as:

`drawdown = (equity / peak) - 1`

A drawdown of `-0.30`, for example, means that the investment is 30% below
its previous historical peak.

The most severe drawdown observed during the analyzed period is called the
**Maximum Drawdown**.