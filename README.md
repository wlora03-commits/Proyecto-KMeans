# Segmentación de Clientes con K-Means

## Descripción

Este proyecto utiliza aprendizaje no supervisado mediante el algoritmo K-Means para segmentar clientes con características similares.

El objetivo es identificar grupos de clientes según su antigüedad, cargos, servicios contratados y valor del cliente.

## Dataset

El dataset contiene 7,043 clientes y variables relacionadas con:

- Datos demográficos
- Antigüedad
- Servicios contratados
- Tipo de contrato
- Método de pago
- Cargos mensuales
- Gastos acumulados
- CLTV

Las variables relacionadas directamente con Churn no fueron utilizadas como variables de entrada del modelo.

## Preparación de los datos

Se realizaron los siguientes procesos:

1. Conversión de `Total Charges` a formato numérico.
2. Tratamiento de valores nulos.
3. Eliminación de identificadores y variables geográficas.
4. Eliminación de variables relacionadas con Churn.
5. Separación de variables numéricas y categóricas.
6. Estandarización de variables numéricas.
7. Codificación One-Hot de variables categóricas.

Después del procesamiento se obtuvieron 47 variables para el modelo.

## Modelo K-Means

Se evaluaron valores de K entre 2 y 10 utilizando:

- Método del codo.
- Coeficiente de Silhouette.

Se seleccionó:

**K = 3**

Configuración utilizada:

```python
KMeans(
    n_clusters=3,
    random_state=42,
    n_init=10
)
```

## Resultados

| Cluster | Clientes | Porcentaje |
|---|---:|---:|
| 0 | 1,526 | 21.7% |
| 1 | 3,261 | 46.3% |
| 2 | 2,256 | 32.0% |

### Cluster 0

Clientes sin Internet y con bajo gasto.

- 1,526 clientes
- Antigüedad promedio: 30.55 meses
- Cargo mensual promedio: $21.08
- Gasto total promedio: $662.60
- CLTV promedio: $4,374.38
- 100% no tiene servicio de Internet

### Cluster 1

Clientes más recientes con Internet y predominio de contratos mensuales.

- 3,261 clientes
- Antigüedad promedio: 15.56 meses
- Cargo mensual promedio: $68.63
- Gasto total promedio: $1,065.37
- CLTV promedio: $3,974.63
- 86% tiene contrato mensual

### Cluster 2

Clientes antiguos, con mayor gasto y mayor utilización de servicios adicionales.

- 2,256 clientes
- Antigüedad promedio: 57.90 meses
- Cargo mensual promedio: $88.72
- Gasto total promedio: $5,128.92
- CLTV promedio: $5,033.11

## Visualizaciones

El proyecto incluye gráficas sobre:

- Cantidad de clientes por segmento.
- Cargo mensual promedio por segmento.
- Antigüedad promedio por segmento.
- Visualización de los clusters mediante PCA.

Las gráficas se encuentran en la carpeta `graficas/`.

## Estructura del proyecto

```text
Proyecto KMeans/
│
├── data/
│   └── clientes_segmentados.csv
│
├── graficas/
│   ├── clientes_por_segmento.png
│   ├── cargo_mensual_por_segmento.png
│   └── antiguedad_por_segmento.png
│
├── kmeans_experimento.ipynb
├── README.md
└── requirements.txt
```

## Tecnologías utilizadas

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Jupyter Notebook
- Visual Studio Code

## Conclusión

El modelo K-Means permitió identificar tres segmentos de clientes con características diferenciadas principalmente por antigüedad, nivel de gasto, tipo de contrato, servicio de Internet y contratación de servicios adicionales.

La segmentación proporciona una base para analizar posteriormente el comportamiento de los diferentes grupos de clientes.