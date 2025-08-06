Análisis de Evasión de Clientes (Churn) - Telecom X
​Descripción del Proyecto
​Este proyecto forma parte de un análisis de datos para la empresa Telecom X, cuyo objetivo es investigar y comprender los factores que contribuyen a la evasión de clientes (Churn). A través del procesamiento y análisis de datos, se busca identificar patrones y tendencias clave que permitan desarrollar estrategias efectivas para la retención de clientes.
​El análisis se ha estructurado en varias fases, desde la limpieza de datos hasta la generación de conclusiones e insights estratégicos.
​El Problema
​Telecom X enfrenta una alta tasa de cancelación de servicios, lo que impacta directamente en sus ingresos y crecimiento. El equipo de Data Science necesita una base sólida de conocimiento sobre el comportamiento de los clientes para poder avanzar en la creación de modelos predictivos y tomar decisiones informadas.
​Objetivos del Análisis
​Extracción, Transformación y Carga (ETL): Preparar el conjunto de datos para el análisis, asegurando su calidad y consistencia.
​Análisis Exploratorio de Datos (EDA): Identificar la distribución de la evasión y su relación con variables clave del cliente (demográficas, de servicio y de cuenta).
​Visualización de Datos: Utilizar gráficos estratégicos para ilustrar los hallazgos y facilitar la comprensión de los patrones.
​Generación de Insights: Extraer conclusiones significativas que sirvan de base para la toma de decisiones estratégicas.
​Conjunto de Datos
​El análisis se ha realizado utilizando el archivo Datos_TelecomX.csv, que contiene información detallada sobre 7.043 clientes. Las columnas clave incluyen:
​Churn: Variable objetivo (Yes/No) que indica si el cliente se dio de baja.
​customer.tenure: Antigüedad del cliente en meses.
​account.Contract: Tipo de contrato del cliente (mes a mes, un año, dos años).
​internet.InternetService: Tipo de servicio de internet (DSL, Fibra óptica, No).
​account.Charges.Monthly: Cargo mensual del cliente.
​account.Charges.Total: Cargo total acumulado.
​Metodología y Herramientas
​El proyecto se desarrolló utilizando el lenguaje de programación Python en un entorno de Google Colab, con las siguientes bibliotecas:
​Pandas: Para la manipulación y el análisis de los datos.
​Matplotlib y Seaborn: Para la creación de visualizaciones estadísticas.
​Fases del Análisis
​Limpieza y Preprocesamiento: Se convirtió la columna account.Charges.Total a tipo numérico y se imputaron los valores nulos con 0, asumiendo que corresponden a clientes nuevos sin cargos acumulados.
​Análisis Descriptivo: Se calcularon métricas básicas como la media, mediana y desviación estándar para las variables numéricas.
​Análisis de Evasión: Se evaluó la distribución de la evasión por variables categóricas y numéricas, utilizando gráficos de barras, boxplots e histogramas.
​Conclusiones e Insights Clave
​Antigüedad del Cliente (customer.tenure): La antigüedad es el predictor más fuerte de la evasión. Los clientes que cancelan su servicio tienen una antigüedad significativamente menor, lo que subraya la importancia de la retención en las primeras etapas.
​Tipo de Contrato (account.Contract): Los clientes con contratos "Month-to-month" muestran una tasa de evasión notablemente superior a la de aquellos con contratos de uno o dos años. La falta de compromiso a largo plazo es un factor de riesgo.
​Servicio de Internet (internet.InternetService): El servicio de "Fiber optic" presenta una tasa de abandono significativamente más alta que otros servicios, lo que podría estar relacionado con problemas de calidad o costos percibidos.
​Otros Factores: El método de pago "Electronic check" también se asocia a una mayor tasa de abandono.
​Recomendaciones Estratégicas
​Basado en los hallazgos, se sugieren las siguientes acciones para mitigar el Churn:
​Programa de Bienvenida: Crear un programa de seguimiento especial para los clientes durante sus primeros seis meses de servicio para garantizar una experiencia positiva.
​Revisión del Servicio de Fibra Óptica: Investigar las causas detrás de la insatisfacción de los clientes de fibra óptica (p.ej., calidad del servicio, soporte técnico, precios).
​Incentivos para Contratos a Largo Plazo: Ofrecer descuentos o beneficios exclusivos para alentar a los clientes con contratos mes a mes a migrar a planes anuales.