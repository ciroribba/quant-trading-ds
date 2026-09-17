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