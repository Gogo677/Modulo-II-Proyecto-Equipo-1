# Análisis Estadístico del Precio de Vehículos BMW

**Diplomado en Técnicas Estadísticas en Minería de Datos**
**Módulo II — Modelos Estadísticos · Proyecto Final**

> Identificación de la distribución de probabilidad que mejor modela el precio de
> vehículos BMW usados, estimación de sus parámetros por máxima verosimilitud y
> contraste de hipótesis sobre las diferencias de precio entre segmentos del mercado.

## Equipo 1

- Jose Manuel Gómez Vaca
- Diego Jimenez Gonzalez
- Sophia Castañeda Ayala
- Victor Hugo Espinoza Torres
- Israel Alejandro Altamirano García

---

## 1. Planteamiento del problema

El mercado de vehículos usados de BMW presenta una amplia dispersión de precios que depende
de múltiples factores (modelo, año, kilometraje, tipo de combustible, transmisión y tamaño de
motor). Para un comprador, vendedor o analista resulta difícil saber **qué patrón estadístico
gobierna los precios** y **si las diferencias observadas entre segmentos del mercado son reales
o producto del azar**.

Estadísticamente, el precio es una variable continua, positiva y con **sesgo a la derecha**
(muchos vehículos económicos y unos pocos de precio muy elevado). Esta característica sugiere
que la distribución Normal podría no ser el mejor modelo, y que distribuciones como la
**Log-Normal** o la **Gamma** podrían describir mejor el fenómeno.

## 2. Preguntas de investigación

1. ¿Qué distribución de probabilidad (**Normal**, **Log-Normal** o **Gamma**) modela mejor el
   precio de los vehículos BMW?
2. ¿Existe una diferencia significativa en el **precio medio** entre vehículos con transmisión
   **Automática** y **Manual**?

## 3. Descripción del dataset

**Fuente:** [BMW Sales and Pricing Trends — Kaggle](https://www.kaggle.com/datasets/ayeshaimran1619/bmw-sales-and-pricing-trends)
· Archivo local: [`bmw.csv`](bmw.csv)

| Característica | Detalle |
|---|---|
| Observaciones | 10,781 vehículos |
| Rango de años | 1996 – 2020 |
| Variable de interés | `price` (precio en libras esterlinas, £) |
| Variables continuas | `price`, `mileage`, `mpg`, `engineSize`, `tax` |
| Variables categóricas | `model`, `year`, `transmission`, `fuelType` |

**Estadísticos descriptivos del precio:**

| Estadístico | Valor |
|---|---|
| Media | £22,733 |
| Mediana | £20,462 |
| Desviación estándar | £11,416 |
| Mínimo | £1,200 |
| Máximo | £123,456 |
| Asimetría (skewness) | 1.587 |

Que la **media (£22,733) sea mayor que la mediana (£20,462)** y que la asimetría sea claramente
positiva confirman el sesgo a la derecha del precio, lo que motiva el uso de distribuciones
asimétricas.

**Tamaños de grupo:**

- **Combustible:** Diésel (7,027), Gasolina (3,417), Híbrido (298), Otro (36), Eléctrico (3)
- **Transmisión:** Semi-automática (4,666), Automática (3,588), Manual (2,527)

## 4. Distribuciones a aplicar

- **Normal** — modelo de referencia simétrico.
- **Log-Normal** — apropiada para variables positivas con sesgo a la derecha.
- **Gamma** — alternativa flexible para variables positivas asimétricas.

## 5. Métodos estadísticos

- **Estimación puntual** de los parámetros de cada distribución por **máxima verosimilitud (MLE)**
  con `scipy.stats`.
- **Comparación del ajuste** mediante AIC, prueba de **Kolmogorov–Smirnov**, densidad teórica
  sobre el histograma y **gráficos Q-Q**.
- **Intervalo de confianza al 95 %** para el precio medio, por el método *t* de Student y por
  **bootstrap** (10,000 remuestreos).
- **Prueba de hipótesis** para comparar el precio medio entre transmisión Automática y Manual:
  - H₀: μ_Auto = μ_Manual (no hay diferencia de precio medio)
  - H₁: μ_Auto ≠ μ_Manual (existe diferencia)
  - Mediante prueba *t* de Welch (varianzas desiguales) y, como respaldo no paramétrico, la
    prueba de Mann–Whitney U.

## 6. Estructura del repositorio

```
.
├── README.md            # Este documento (propuesta y guía del proyecto)
├── analisis_bmw.ipynb   # Notebook con el análisis estadístico completo
├── bmw.csv              # Dataset utilizado
└── requirements.txt     # Dependencias de Python
```

## 7. Cómo reproducir el análisis

```bash
# 1. Instalar las dependencias
pip install -r requirements.txt

# 2. Abrir el notebook
jupyter notebook analisis_bmw.ipynb
```

> El notebook lee `bmw.csv` mediante una ruta relativa, por lo que debe ejecutarse desde la
> raíz del repositorio (donde se encuentran ambos archivos).

## 8. Resultados esperados

- Identificación justificada de la distribución que mejor describe el precio de los BMW.
- Parámetros estimados con su interpretación en el contexto del mercado.
- Conclusión estadística sobre si el precio medio difiere entre segmentos del mercado.

## 9. Criterios de evaluación

| Criterio | Peso |
|---|---|
| Identificación y justificación de la distribución | 20 % |
| Estimación puntual con método adecuado (MLE, momentos) | 20 % |
| Intervalo de confianza 95 % con interpretación correcta | 20 % |
| Prueba de hipótesis | 25 % |
| Código Python reproducible y documentado | 15 % |

## 10. Bibliografía y recursos

- Documentación `scipy.stats`: <https://docs.scipy.org/doc/scipy/reference/stats.html>
- Python: <https://www.python.org/>
- Kaggle Learn: <https://www.kaggle.com/learn>
