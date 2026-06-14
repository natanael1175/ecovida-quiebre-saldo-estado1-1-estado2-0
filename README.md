# Análisis de Quiebre de Saldo Estado1=1 Estado2=0 Ecovida

![Python](https://img.shields.io/badge/Python-3.x-blue) ![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange) ![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-green) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

Análisis exhaustivo de las líneas de pedido con saldo pendiente sin despachar en el ERP Bsoft de Ecovida / Alimentos Claudet, cuantificando el riesgo operacional y financiero real asociado a quiebres de saldo entre 2021 y 2025.
Este proyecto convierte 86.932 transacciones en decisiones concretas de abastecimiento, priorización de clientes y planificación preventiva de inventario.

---

## Contexto de Negocio

Ecovida / Alimentos Claudet es una empresa chilena de alimentos que comercializa galletas, biscuits y emparedados bajo las marcas Ecovida y Alimentos Claudet, gestionando sus pedidos y despachos a través del ERP Bsoft. En su operación diaria, una fracción de las líneas de pedido queda registrada con ESTADO1=1 y ESTADO2=0, condición que identifica saldo comprometido pero no despachado, generando un riesgo financiero y operacional que hasta ahora no había sido sistematizado ni cuantificado. Este análisis cubre el período comprendido entre el 23 de marzo de 2021 y el 13 de enero de 2025, procesando 86.932 transacciones con 46 variables, para transformar ese riesgo latente en información accionable. Identificar qué productos, qué clientes y qué períodos concentran los quiebres de saldo es el primer paso para reducir pérdidas comerciales, mejorar el nivel de servicio y fortalecer las relaciones con los canales de venta.

---

## Preguntas que Responde este Análisis

1. ¿Cuántas líneas de pedido presentan quiebre de saldo (ESTADO1=1 y ESTADO2=0) y cuál es el valor total en pesos comprometido en ese saldo pendiente?
2. ¿Qué productos concentran la mayor cantidad de unidades en saldo con quiebre (ESTADO1=1, ESTADO2=0) y cuáles representan el mayor riesgo económico?
3. ¿Qué clientes tienen mayor exposición a quiebres de saldo activos (ESTADO1=1, ESTADO2=0) en términos de unidades y valor pendiente de despacho?
4. ¿Cómo ha evolucionado la frecuencia y magnitud de los quiebres de saldo (ESTADO1=1, ESTADO2=0) a lo largo del período 2021-2025, identificando peaks o tendencias críticas?

---

## Estructura del Análisis

| # | Sección | Técnica Aplicada | Insight Clave |
|---|---------|-----------------|---------------|
| 1 | Contexto de Negocio y Universo de Quiebres de Saldo | Filtrado de estados, estadística descriptiva, KPIs agregados | Cuantificación del monto total en pesos comprometido en saldo pendiente |
| 2 | Productos con Mayor Exposición a Quiebres de Saldo | Análisis de Pareto (80/20), ranking por unidades y valor monetario | Un conjunto reducido de SKUs concentra la mayoría del riesgo económico |
| 3 | Clientes con Mayor Exposición a Quiebres Activos | Segmentación por cliente, acumulación de saldo pendiente | Un grupo acotado de clientes acumula desproporcionadamente el riesgo comercial |
| 4 | Evolución Temporal de Quiebres de Saldo 2021-2025 | Serie de tiempo mensual, detección de peaks y tendencias | Determina si los quiebres son estructurales, estacionales o por eventos puntuales |
| 5 | Estacionalidad y Patrones de Quiebre por Mes y Año | Heatmap mes-año, análisis de estacionalidad cruzada | Revela meses críticos recurrentes para planificación preventiva de inventario |
| 6 | Síntesis Ejecutiva, Riesgos Priorizados y Recomendaciones | Combinación de dimensiones: producto, cliente y período | Perfil de riesgo prioritario que concentra el mayor impacto económico y operacional |

---

## Stack Técnico

| Herramienta | Uso en este Proyecto |
|-------------|---------------------|
| Python 3.x | Lenguaje base del análisis y procesamiento de datos |
| pandas | Carga, limpieza, filtrado y agregación de las 86.932 transacciones |
| matplotlib | Construcción de gráficos de serie de tiempo y barras horizontales |
| seaborn | Generación del heatmap de estacionalidad mes-año y visualizaciones complementarias |
| Jupyter Notebook | Entorno de análisis reproducible con narrativa integrada y visualizaciones inline |

---

## Cómo Ejecutar

1. Clonar el repositorio en tu máquina local:

```bash
git clone https://github.com/tu-usuario/analisis-quiebre-saldo-ecovida.git
cd analisis-quiebre-saldo-ecovida
```

2. Crear y activar un entorno virtual (recomendado):

```bash
python -m venv venv
source venv/bin/activate        # Linux / macOS
venv\Scripts\activate           # Windows
```

3. Instalar las dependencias requeridas:

```bash
pip install -r requirements.txt
```

4. Lanzar Jupyter Notebook y abrir el archivo de análisis:

```bash
jupyter notebook
```

5. Abrir el archivo `notebooks/analisis_quiebre_saldo_ecovida.ipynb` y ejecutar las celdas en orden secuencial.

> **Nota:** El archivo de datos fuente debe ubicarse en la carpeta `data/raw/` con el nombre `quiebre_saldo_ecovida.xlsx`. Por razones de confidencialidad, el dataset no se incluye en este repositorio.

---

## Estructura del Repositorio

```
analisis-quiebre-saldo-ecovida/
│
├── data/
│   ├── raw/                          # Datos originales exportados desde ERP Bsoft (no versionados)
│   └── processed/                    # Datos limpios y filtrados generados durante el análisis
│
├── notebooks/
│   └── analisis_quiebre_saldo_ecovida.ipynb   # Notebook principal con el análisis completo
│
├── img/
│   ├── grafico_1.png                 # KPIs del universo de quiebres de saldo
│   ├── grafico_2.png                 # Pareto de productos por unidades y valor en quiebre
│   ├── grafico_3.png                 # Ranking de clientes con mayor saldo pendiente
│   ├── grafico_4.png                 # Serie de tiempo mensual de quiebres 2021-2025
│   └── grafico_5.png                 # Heatmap de estacionalidad por mes y año
│
├── requirements.txt                  # Dependencias del proyecto (pandas, matplotlib, seaborn)
├── .gitignore                        # Exclusión de datos sensibles y entornos virtuales
└── README.md                         # Documentación del proyecto
```

---

## Visualizaciones

### Sección 1: Universo de Quiebres de Saldo

![KPIs del universo de quiebres de saldo](img/grafico_1.png)

El panel de indicadores cuantifica el total de líneas con quiebre activo (ESTADO1=1, ESTADO2=0), el monto total comprometido en pesos y el porcentaje que representa sobre el universo completo de pedidos, estableciendo la magnitud real del problema operacional.

### Sección 2: Productos con Mayor Exposición

![Pareto de productos por unidades y valor en quiebre](img/grafico_2.png)

La curva de Pareto confirma que un conjunto reducido de SKUs concentra el 80% de las unidades y del valor monetario en quiebre, señalando con precisión los productos donde una intervención de abastecimiento genera el mayor retorno operacional.

### Sección 3: Clientes con Mayor Exposición a Quiebres Activos

![Ranking de clientes con mayor saldo pendiente](img/grafico_3.png)

El ranking de clientes expone qué cuentas acumulan desproporcionadamente el saldo pendiente de despacho, permitiendo priorizar la gestión comercial y reducir el riesgo de penalizaciones contractuales en los vínculos de mayor valor.

### Sección 4: Evolución Temporal de Quiebres 2021-2025

![Serie de tiempo mensual de quiebres 2021-2025](img/grafico_4.png)

La serie de tiempo mensual revela si la frecuencia y magnitud de los quiebres sigue una tendencia creciente, un patrón estacional o responde a eventos puntuales, orientando si la solución requiere cambios estructurales en la operación o planes de contingencia específicos.

### Sección 5: Heatmap de Estacionalidad por Mes y Año

![Heatmap de estacionalidad por mes y año](img/grafico_5.png)

El heatmap cruza mes y año para exponer si ciertos meses concentran sistemáticamente más quiebres a lo largo del período analizado, revelando estacionalidad explotable para la planificación preventiva de inventario y la coordinación logística anticipada.

---

## Hallazgos Clave

- **Concentración en productos críticos:** Un grupo acotado de SKUs, equivalente a menos del 20% del catálogo activo con quiebre, concentra la mayor parte del valor monetario comprometido, validando que la intervención debe focalizarse en esos productos antes de escalar acciones al resto del portafolio.

- **Riesgo concentrado en clientes estratégicos:** Un segmento reducido de clientes acumula desproporcionadamente el saldo pendiente de despacho, lo que implica un riesgo relacional elevado y una exposición a penalizaciones contractuales que exige gestión prioritaria e inmediata.

- **Estacionalidad identificable y explotable:** El análisis temporal revela que determinados meses del año concentran sistemáticamente una mayor frecuencia e intensidad de quiebres, lo que indica que el problema tiene un componente estacional predecible que puede anticiparse con planificación de inventario y logística.

- **El quiebre de saldo es un problema estructural, no puntual:** La distribución de eventos a lo largo de los cuatro años analizados indica que los quiebres no responden exclusivamente a crisis aisladas, sino a una brecha recurrente entre la demanda comprometida en pedidos y la capacidad efectiva de despacho, que requiere una solución operacional de fondo.

---

*Desarrollado por Analista de Datos — 2025*