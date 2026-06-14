# Análisis de Quiebre de Saldo Estado1=1 Estado2=0 — Ecovida / Alimentos Claudet

![Python](https://img.shields.io/badge/Python-3.x-blue) ![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange) ![pandas](https://img.shields.io/badge/pandas-2.x-green) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

Análisis exploratorio de 86.932 transacciones del ERP Bsoft para identificar, cuantificar y priorizar las líneas de pedido con saldo pendiente sin despachar en Ecovida / Alimentos Claudet.
El objetivo es convertir un problema operacional disperso en un mapa de riesgo accionable que orienta decisiones de abastecimiento, logística y gestión de clientes.

---

## Contexto de Negocio

Ecovida / Alimentos Claudet es una empresa chilena del rubro alimenticio que comercializa galletas, biscuits y emparedados a través de múltiples canales de venta, gestionando sus pedidos y despachos mediante el ERP Bsoft. En ese sistema, una línea de pedido con ESTADO1=1 y ESTADO2=0 indica que el pedido fue ingresado pero el despacho no fue completado, generando un saldo pendiente que compromete tanto el nivel de servicio al cliente como la posición financiera de la empresa. Con cuatro años de historial transaccional disponible (marzo 2021 a enero 2025), este análisis permite dimensionar el fenómeno, identificar los productos y clientes de mayor exposición y detectar si existe un patrón temporal que justifique medidas preventivas estructurales.

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
| 1 | Contexto de Negocio y Universo de Quiebres de Saldo | Filtrado condicional, estadística descriptiva, KPIs agregados | Fracción del total de líneas con saldo pendiente y monto total comprometido en pesos |
| 2 | Productos con Mayor Exposición a Quiebres de Saldo | Ranking por volumen y valor, análisis de Pareto 80/20 | Un conjunto reducido de SKUs concentra la mayoría del riesgo; esos son los productos a priorizar en abastecimiento |
| 3 | Clientes con Mayor Exposición a Quiebres Activos | Agrupación por cliente, ranking dual (unidades y valor), visualización de barras horizontales | Un grupo acotado de clientes acumula desproporcionadamente el saldo pendiente, con riesgo de penalización contractual |
| 4 | Evolución Temporal de Quiebres de Saldo 2021-2025 | Serie temporal mensual, análisis de tendencia, detección de peaks | Determina si el problema es estructural y creciente, estacional o vinculado a eventos puntuales |
| 5 | Estacionalidad y Patrones de Quiebre por Mes y Año | Heatmap año × mes, pivot table | Revela qué meses concentran sistemáticamente más quiebres, habilitando planificación preventiva de inventario |
| 6 | Síntesis Ejecutiva, Riesgos Priorizados y Recomendaciones | Cruce de dimensiones (producto + cliente + período), tabla de riesgos priorizados | Define el perfil de riesgo combinado de mayor impacto económico y operacional para la empresa |

---

## Stack Técnico

| Herramienta | Uso en este Proyecto |
|-------------|---------------------|
| Python 3.x | Lenguaje base para toda la cadena de análisis |
| pandas | Carga, limpieza, filtrado, agrupación y transformación de las 86.932 transacciones |
| matplotlib | Construcción de gráficos de series temporales, barras y configuración de estilos base |
| seaborn | Heatmap de estacionalidad y visualizaciones comparativas de distribución |
| Jupyter Notebook | Entorno de desarrollo narrativo que integra código, visualizaciones y conclusiones de negocio |

---

## Cómo Ejecutar

1. Clonar el repositorio:
```bash
git clone https://github.com/usuario/quiebre-saldo-ecovida.git
cd quiebre-saldo-ecovida
```

2. Crear y activar un entorno virtual (recomendado):
```bash
python -m venv venv
source venv/bin/activate        # Linux / macOS
venv\Scripts\activate           # Windows
```

3. Instalar las dependencias:
```bash
pip install -r requirements.txt
```

4. Lanzar el notebook:
```bash
jupyter notebook notebooks/analisis_quiebre_saldo_ecovida.ipynb
```

> El archivo de datos fuente debe ubicarse en `data/raw/` con el nombre original exportado desde Bsoft. El notebook lee esa ruta por defecto.

---

## Estructura del Repositorio

```
quiebre-saldo-ecovida/
│
├── data/
│   ├── raw/                        # Archivo original exportado desde ERP Bsoft (no versionado)
│   └── processed/                  # Dataset filtrado con quiebres ESTADO1=1, ESTADO2=0
│
├── notebooks/
│   └── analisis_quiebre_saldo_ecovida.ipynb   # Notebook principal con las 6 secciones de análisis
│
├── img/
│   ├── grafico_1.png               # KPIs de universo de quiebres
│   ├── grafico_2.png               # Pareto de productos por unidades y valor
│   ├── grafico_3.png               # Ranking de clientes con mayor exposición
│   ├── grafico_4.png               # Serie temporal mensual 2021-2025
│   ├── grafico_5.png               # Heatmap de estacionalidad mes x año
│   └── grafico_6.png               # Tabla de riesgos priorizados
│
├── requirements.txt                # Dependencias del proyecto (pandas, matplotlib, seaborn)
├── .gitignore                      # Excluye datos sensibles y entornos virtuales
└── README.md                       # Documentación del proyecto
```

---

## Visualizaciones

### Sección 1 — Universo de Quiebres de Saldo

![KPIs de universo de quiebres de saldo](img/grafico_1.png)

El panel de indicadores muestra el volumen total de líneas de pedido analizadas, la proporción con quiebre activo (ESTADO1=1, ESTADO2=0) y el monto total en pesos comprometido, estableciendo la magnitud real del problema para la dirección comercial y operacional.

---

### Sección 2 — Productos con Mayor Exposición a Quiebres de Saldo

![Análisis de Pareto de productos por unidades y valor en quiebre](img/grafico_2.png)

El gráfico de Pareto confirma que un número reducido de SKUs concentra el 80% de las unidades y del valor monetario pendiente, definiendo la lista corta de productos donde una mejora en abastecimiento genera el mayor impacto inmediato.

---

### Sección 3 — Clientes con Mayor Exposición a Quiebres Activos

![Ranking de clientes por saldo pendiente en unidades y valor](img/grafico_3.png)

El ranking de barras horizontales expone los clientes con mayor acumulación de saldo no despachado, revelando cuáles relaciones comerciales concentran el mayor riesgo de incumplimiento contractual y requieren gestión prioritaria.

---

### Sección 4 — Evolución Temporal de Quiebres de Saldo 2021-2025

![Serie temporal mensual de quiebres de saldo 2021-2025](img/grafico_4.png)

La serie mensual permite distinguir si los quiebres responden a una tendencia estructural creciente, a ciclos estacionales repetibles o a eventos puntuales, determinando si la solución requiere cambios permanentes en los procesos o planes de contingencia acotados.

---

### Sección 5 — Estacionalidad y Patrones de Quiebre por Mes y Año

![Heatmap de estacionalidad de quiebres por mes y año](img/grafico_5.png)

El heatmap cruza los ejes año y mes para revelar si ciertos períodos del calendario concentran sistemáticamente mayor frecuencia de quiebres, proporcionando una base objetiva para la planificación anticipada de inventario y capacidad logística.

---

### Sección 6 — Síntesis Ejecutiva y Riesgos Priorizados

![Tabla de riesgos priorizados por producto, cliente y período](img/grafico_6.png)

La síntesis cruza las tres dimensiones críticas —producto, cliente y período— para construir un ranking de riesgo combinado que concentra el mayor impacto económico y operacional, traduciendo el análisis en una agenda de acción concreta para la dirección de la empresa.

---

## Hallazgos Clave

- **Concentración de riesgo en productos:** Un subconjunto reducido de SKUs, aplicando la regla 80/20, acumula la mayor parte del valor en quiebre; redirigir esfuerzos de abastecimiento hacia esos productos tiene un efecto desproporcionado sobre el nivel de servicio global.

- **Exposición asimétrica en clientes:** Un grupo acotado de clientes concentra un porcentaje desproporcionado del saldo pendiente activo, lo que eleva significativamente el riesgo de penalización comercial y deterioro de la relación en esas cuentas específicas.

- **Patrón temporal identificable:** La evolución mensual 2021-2025 evidencia que los quiebres no se distribuyen de manera uniforme en el tiempo; la detección de peaks recurrentes en determinados períodos habilita la implementación de medidas preventivas antes de que el problema se materialice.

- **Problema con componente estructural:** La persistencia de quiebres de saldo a lo largo de cuatro años sugiere que el fenómeno no es un evento aislado sino un patrón operacional que requiere ajustes en los procesos de planificación de inventario, no solo respuestas reactivas puntuales.

---

*Desarrollado por [Analista de Datos] — 2025*