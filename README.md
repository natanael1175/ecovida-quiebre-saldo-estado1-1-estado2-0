```markdown
![Python 3.x](https://img.shields.io/badge/Python-3.x-blue) ![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange) ![pandas](https://img.shields.io/badge/pandas-DataFrame-green) ![License MIT](https://img.shields.io/badge/License-MIT-lightgrey)

# Análisis de Quiebre de Saldo — Ecovida / Alimentos Claudet

Identificación, cuantificación y priorización de líneas de pedido con saldo pendiente sin despachar (ESTADO1=1, ESTADO2=0) sobre 86.932 transacciones registradas en el ERP Bsoft entre 2021 y 2025, con el objetivo de revelar el riesgo operacional y financiero real que representan los quiebres activos para la operación comercial de Ecovida y Alimentos Claudet.

---

## Contexto de Negocio

Ecovida / Alimentos Claudet es una empresa chilena de alimentos que comercializa productos como galletas, biscuits y emparedados a múltiples canales de venta, gestionando su operación de pedidos y despachos a través del ERP Bsoft. Un quiebre de saldo ocurre cuando una línea de pedido queda comprometida (ESTADO1=1) pero no es despachada (ESTADO2=0), generando una brecha entre la demanda registrada y la entrega efectiva al cliente. Este fenómeno compromete el nivel de servicio, expone a la empresa a penalizaciones contractuales y representa un monto en pesos inmovilizado que puede escalar silenciosamente si no se gestiona con datos. El presente análisis convierte ese riesgo difuso en cifras concretas, productos identificados y clientes priorizados, habilitando decisiones operativas y comerciales inmediatas.

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
| 1 | Contexto de Negocio y Universo de Quiebres de Saldo | Filtrado booleano, estadística descriptiva, KPIs agregados | Cuantificación del monto total en pesos comprometido en saldo pendiente sin despachar |
| 2 | Productos con Mayor Exposición a Quiebres de Saldo | Análisis de concentración (regla 80/20), ranking por unidades y valor | Un conjunto reducido de SKUs concentra la mayoría del riesgo económico y de inventario |
| 3 | Clientes con Mayor Exposición a Quiebres Activos | Ranking de clientes por saldo pendiente, análisis de valor acumulado | Un grupo acotado de clientes acumula desproporcionadamente el riesgo comercial y contractual |
| 4 | Evolución Temporal de Quiebres de Saldo 2021-2025 | Serie de tiempo mensual, detección de peaks y tendencias | Determinación de si el quiebre es un problema estructural creciente o asociado a eventos puntuales |
| 5 | Estacionalidad y Patrones de Quiebre por Mes y Año | Heatmap mes-año, análisis de estacionalidad multianual | Identificación de meses con concentración sistemática de quiebres para planificación preventiva |
| 6 | Síntesis Ejecutiva, Riesgos Priorizados y Recomendaciones | Cruce producto-cliente-período, scoring de riesgo combinado | El perfil de riesgo prioritario emerge de la intersección entre SKU crítico, cliente de alto valor y período de mayor frecuencia |

---

## Stack Técnico

| Herramienta | Uso en este proyecto |
|-------------|---------------------|
| Python 3.x | Lenguaje base para toda la cadena de análisis |
| pandas | Carga, limpieza, filtrado y agregación del dataset de 86.932 transacciones |
| matplotlib | Construcción de series de tiempo y gráficos de barras para análisis evolutivo |
| seaborn | Generación del heatmap de estacionalidad mes-año y gráficos de distribución |
| Jupyter Notebook | Entorno de análisis interactivo con narrativa integrada y visualizaciones en línea |

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

4. Iniciar Jupyter Notebook:
   ```bash
   jupyter notebook
   ```

5. Abrir el archivo principal:
   ```
   notebooks/analisis_quiebre_saldo_ecovida.ipynb
   ```

---

## Estructura del Repositorio

```
quiebre-saldo-ecovida/
│
├── data/
│   └── raw/
│       └── quiebre_saldo_ecovida.csv       # Dataset original — 86.932 transacciones, 46 variables
│
├── notebooks/
│   └── analisis_quiebre_saldo_ecovida.ipynb  # Notebook principal con las 6 secciones de análisis
│
├── img/
│   ├── grafico_1.png                        # KPIs del universo de quiebres de saldo
│   ├── grafico_2.png                        # Ranking de productos por exposición (80/20)
│   ├── grafico_3.png                        # Ranking de clientes por saldo pendiente
│   ├── grafico_4.png                        # Serie temporal mensual 2021-2025
│   └── grafico_5.png                        # Heatmap de estacionalidad mes-año
│
├── requirements.txt                         # Dependencias del proyecto (pandas, matplotlib, seaborn)
├── LICENSE                                  # Licencia MIT
└── README.md                                # Documentación del repositorio
```

---

## Visualizaciones

### Sección 1 — Universo de Quiebres de Saldo

![KPIs del universo de quiebres de saldo](img/grafico_1.png)

El panel de indicadores cuantifica el total de líneas con quiebre activo, las unidades comprometidas y el monto total en pesos que permanece pendiente de despacho, estableciendo la magnitud real del problema para la dirección de operaciones.

### Sección 2 — Productos con Mayor Exposición

![Ranking de productos por unidades y valor en quiebre](img/grafico_2.png)

El gráfico de barras ordenado por valor pendiente evidencia que un conjunto reducido de SKUs concentra la mayor parte del riesgo económico, validando la regla 80/20 y permitiendo focalizar las acciones de reabastecimiento en los productos de mayor impacto.

### Sección 3 — Clientes con Mayor Exposición

![Ranking de clientes por saldo pendiente de despacho](img/grafico_3.png)

La visualización revela qué clientes acumulan desproporcionadamente el saldo sin despachar, identificando las cuentas donde el riesgo de relación comercial y de penalización contractual es más urgente de resolver.

### Sección 4 — Evolución Temporal 2021-2025

![Serie temporal mensual de quiebres de saldo](img/grafico_4.png)

La serie de tiempo mensual permite distinguir si los quiebres responden a un deterioro estructural sostenido, a estacionalidad recurrente o a eventos puntuales de disrupción operacional, orientando el tipo de solución requerida.

### Sección 5 — Heatmap de Estacionalidad

![Heatmap de quiebres por mes y año 2021-2025](img/grafico_5.png)

El heatmap expone con precisión qué combinaciones de mes y año concentran sistemáticamente la mayor frecuencia de quiebres, habilitando una planificación preventiva de inventario y logística basada en patrones históricos demostrables.

---

## Hallazgos Clave

- **Concentración en productos críticos:** Un número reducido de SKUs, probablemente dentro del portafolio de mayor rotación (galletas y biscuits), explica la mayor parte del valor monetario comprometido en quiebre, lo que implica que resolver el abastecimiento de esos productos tiene un efecto desproporcionado sobre el riesgo total.

- **Exposición asimétrica en clientes:** Un grupo acotado de clientes concentra la mayoría del saldo pendiente activo; la gestión prioritaria de esas cuentas reduce la exposición comercial y financiera de forma inmediata sin necesidad de intervenir en toda la cartera.

- **Quiebre con componente estacional identificable:** El análisis temporal multianual revela que ciertos meses del año presentan una concentración sistemáticamente superior de quiebres entre 2021 y 2025, lo que indica que parte del problema es predecible y puede anticiparse con ajustes de inventario previos a esos períodos.

- **Riesgo financiero cuantificable y accionable:** La traducción de las unidades en quiebre a valor en pesos entrega a la dirección un número concreto para dimensionar el costo de oportunidad y priorizar inversión en capacidad de despacho o stock de seguridad, convirtiendo el análisis en una herramienta de decisión financiera directa.

---

*Desarrollado por [Analista de Datos] — 2025*
```