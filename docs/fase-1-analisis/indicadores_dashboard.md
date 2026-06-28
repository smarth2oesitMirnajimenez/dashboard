DOCUMENTO DE ESPECIFICACIÓN: INDICADORES CLAVE DE RENDIMIENTO (KPIs)
Proyecto: SmartH2O – Telemetría y Analítica de Recursos Hídricos 
Cliente: Dirección de Administración de Infraestructura y Recursos (DAIR) 
Responsable: Desarrollador Dashboard Jr. 
1. Propósito de la Visualización
El objetivo de estos indicadores es transformar las lecturas de telemetría simuladas en un centro de control visual dentro de Grafana. Esto permitirá a la DAIR mitigar la falta de visibilidad operativa, identificar fugas de manera temprana y controlar los costos de consumo institucional antes de recibir la facturación mensual. 
2. Matriz de Indicadores del Dashboard
Indicator 1: Consumo Acumulado por Punto de Medición (Volumen Total)
•	Descripción: Muestra la cantidad total de agua (en litros o $m^3$) utilizada por cada edificio, sede o zona en un rango de tiempo seleccionado. 
•	Tipo de Gráfico en Grafana: Gráfico de Barras (Bar Chart) o Tarjeta Estadística (Stat). 
•	Valor para el Cliente: Permite comparar qué instalaciones están gastando más agua y proyectar el impacto financiero por sede antes de la facturación global. 
Indicator 2: Caudal Instantáneo y Tendencia Histórica
•	Descripción: Gráfica el flujo continuo del agua en intervalos de tiempo reales (de 10 a 60 segundos). 
•	Tipo de Gráfico en Grafana: Serie Temporal (Time Series). 
•	Valor para el Cliente: Permite analizar el comportamiento del flujo y observar visualmente si existen picos atípicos o si el consumo se estabiliza dentro de los parámetros esperados. 
Indicator 3: Registro y Conteo de Eventos Anómalos (Alertas)
•	Descripción: Un contador digital y una lista detallada que registra cuántas veces y en qué puntos se han superado los umbrales de seguridad. 
•	Tipo de Gráfico en Grafana: Panel de Estado (State Timeline) o Lista de Alertas (Alert List). 
•	Valor para el Cliente: Visibiliza la "fuga silenciosa" inmediatamente, sirviendo como evidencia directa para activar las órdenes de mantenimiento correctivo. 
Indicator 4: Caudal Promedio en Horario No Laboral (Monitoreo de Fugas Nocturnas)
•	Descripción: Filtra y calcula el promedio del caudal de agua exclusivamente durante las madrugadas, noches y fines de semana. 
•	Tipo de Gráfico en Grafana: Medidor de Aguja (Gauge) o Texto Estadístico (Stat) con filtro de tiempo condicional. 
•	Valor para el Cliente: Es el indicador más crítico para la detección de fugas ocultas. Si un edificio administrativo vacío registra un caudal mayor a cero a las 3:00 AM de manera constante, es una alerta automática de desperdicio o fuga. 
Indicator 5: Pico Máximo de Consumo por Franja Horaria
•	Descripción: Registra el valor máximo de caudal alcanzado durante el día, identificando la hora exacta del evento. 
•	Tipo de Gráfico en Grafana: Gráfico de Densidad o Histograma (Histogram). 
•	Valor para el Cliente: Ayuda a identificar comportamientos ineficientes en las operaciones rutinarias (como riegos excesivos de áreas verdes o limpieza fuera de horarios optimizados). 
Indicator 6: Disponibilidad y Estado de la Red de Sensores (SLA de Telemetría)
•	Descripción: Monitorea si los sensores simulados están transmitiendo datos activamente o si hay ausencia de lecturas. 
•	Tipo de Gráfico en Grafana: Panel de Estado de Luces (Status History / semáforo verde/rojo). 
•	Valor para el Cliente: Asegura la confianza en el sistema. Si un punto de medición deja de reportar datos por más de un minuto, el panel avisa que el sensor está "Fuera de línea", evitando lecturas erróneas o falsos negativos en las alertas.

