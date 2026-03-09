# Clasificador multiclase de objetos a partir de datos radar 2D

Desarrollo de un clasificador multiclase en R para identificar el tipo de objeto (coche, vehículo grande, bicicleta, persona, etc.) a partir de las mediciones brutas de un sensor radar 2D.

## Clases detectadas

| Código | Clase                               |
|--------|-------------------------------------|
| 0      | Coche                               |
| 1      | Vehículo grande (camión + autobús)  |
| 5      | Bicicleta                           |
| 7      | Persona (incluye grupo de personas) |
| 10     | Otro objeto dinámico                |
| 11     | Background estático                 |

## Resultados

| Conjunto      | mAP    |
|---------------|--------|
| Entrenamiento | 0.9488 |
| Validación    | 0.4399 |

**Clase Persona (7) con umbral = 0.9:**

| Métrica   | Train | Validación |
|-----------|-------|------------|
| Precisión | 0.989 | 0.873      |
| Recall    | 0.939 | 0.773      |

## Estructura del análisis

1.  Carga y reasignación de etiquetas (bus/camión → vehículo grande; grupo → persona)
2.  Separación train / validación (primeros y siguientes 200k registros)
3.  Análisis exploratorio del RCS por clase en función de la distancia (Wilcoxon + gráfico mediana ± MAD)
4.  Entrenamiento de Random Forest multiclase (`ranger`) con muestreo de 20k registros
5.  Cálculo de AP por clase vs. resto y mAP en train y validación
6.  Evaluación del AP por subgrupos de distancia y ángulo de azimuth
7.  Selección del umbral de operación para Persona (7) priorizando precisión

## Tecnologías

-   R
-   Librerías: `dplyr`, `ggplot2`, `ranger`, `PRROC`, `caret`, `tidyr`

## Nota sobre los datos

El fichero `Entregable2.RData` no está incluido en el repositorio. El notebook se comparte únicamente como referencia del análisis.
