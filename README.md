# SmartH2O — `dashboard`

> **Repositorio:** `smarth2o-esit/dashboard`
> **Componente:** Dashboard de visualización en Grafana
> **Fase activa:** Fase 3 – Semanas 6 y 8

---

## ¿Qué hace este componente?

Este repositorio contiene la configuración del dashboard de Grafana para SmartH2O: paneles de consumo hídrico, tendencias históricas, comparación entre zonas, detección visual de anomalías y estado de alertas activas.

No requiere código de aplicación; su principal artefacto es el archivo JSON exportado de Grafana (`smarth2o_dashboard.json`) que puede importarse en cualquier instancia de Grafana conectada a la base de datos del proyecto.

---

## Estructura del repositorio

```
dashboard/
├── grafana/
│   ├── smarth2o_dashboard.json   # Dashboard exportado (importar en Grafana)
│   ├── datasource_influxdb.yaml  # Configuración del datasource (Grafana provisioning)
│   ├── panels/
│   │   ├── consumo_por_punto.md      # Documentación del panel y query
│   │   ├── consumo_diario.md
│   │   ├── caudal_promedio.md
│   │   ├── heatmap_horario.md
│   │   ├── anomalias_detectadas.md
│   │   └── alertas_recientes.md
│   └── screenshots/              # Capturas del dashboard para evidencias
├── docker-compose.yml            # Grafana local para desarrollo
├── .env.example
├── .gitignore
└── README.md
```

---

## Paneles del dashboard

| Panel                     | Tipo          | Fuente de datos          | Descripción                                      |
|---------------------------|---------------|--------------------------|--------------------------------------------------|
| Consumo por punto         | Time series   | `flow_rate` por sensor   | Línea por cada punto de medición                 |
| Consumo acumulado del día | Stat          | `cumulative_volume`      | Total del día vs. día anterior                   |
| Caudal promedio actual    | Gauge         | `flow_rate` media 1h     | Caudal promedio de la última hora                |
| Mapa de calor horario     | Heatmap       | `flow_rate` por hora     | Patrones de consumo por franja del día           |
| Anomalías detectadas      | Table / Alert | `anomaly_flag = true`    | Listado de eventos anómalos recientes            |
| Estado de alertas         | Alert list    | Grafana Alerting         | Alertas activas, resueltas y silenciadas         |
| Comparación entre zonas   | Bar chart     | GROUP BY zone            | Consumo relativo por zona en el período          |

---

## Variables de plantilla (filtros interactivos)

El dashboard incluye variables de plantilla que permiten filtrar la vista sin recargar la página:

| Variable    | Descripción                        | Ejemplo               |
|-------------|------------------------------------|-----------------------|
| `$building` | Filtrar por edificio               | "Edificio Central"    |
| `$zone`     | Filtrar por zona dentro del edificio | "Sanitarios Piso 1" |
| `$sensor`   | Filtrar por sensor específico      | "AARD-A-SAN-P1"      |
| `$interval` | Resolución temporal del gráfico    | 5m / 1h / 1d          |

---

## Importar el dashboard en Grafana

1. Abrir Grafana → **Dashboards** → **Import**
2. Subir el archivo `grafana/smarth2o_dashboard.json`
3. Seleccionar el datasource de InfluxDB configurado
4. Hacer clic en **Import**

---

## Configuración local (desarrollo)

```bash
cp .env.example .env
docker-compose up -d   # Grafana en localhost:3000
```

```env
GRAFANA_ADMIN_USER=admin
GRAFANA_ADMIN_PASSWORD=

INFLUXDB_URL=http://localhost:8086
INFLUXDB_TOKEN=
INFLUXDB_ORG=smarth2o
INFLUXDB_BUCKET=water_telemetry
```

Grafana se levanta en `http://localhost:3000`. El datasource de InfluxDB se configura automáticamente si se usa el archivo `datasource_influxdb.yaml` con Grafana provisioning.

---

## Exportar cambios al repositorio

Después de modificar paneles en Grafana, exportar el JSON actualizado y sobrescribir el archivo en el repositorio:

```
Grafana → Dashboard → Share → Export → Save to file
→ Guardar como grafana/smarth2o_dashboard.json
→ git add · git commit · git push
```

Esto asegura que cualquier miembro del equipo pueda reproducir el dashboard exacto.

---

## Responsable

| Rol                      | Nombre                        | GitHub     |
|--------------------------|-------------------------------|------------|
| Desarrollador Dashboard Jr.|Mirna Yesenia Jimenez Moreno | [@usuario] |

---

## Relacionado con

| Repositorio                                                          | Relación                               |
|----------------------------------------------------------------------|----------------------------------------|
| [`smarth2o-esit/database`](https://github.com/smarth2o-esit/database)   | Fuente de datos (InfluxDB)             |
| [`smarth2o-esit/alerts`](https://github.com/smarth2o-esit/alerts)       | Las reglas de alerta se configuran aquí en Grafana Alerting |

---

> Proyecto SmartH2O · ESIT – Estancia Profesional · Servicios en la Nube
