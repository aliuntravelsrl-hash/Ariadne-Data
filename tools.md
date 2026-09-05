# 🛠 Tools — Ariadne Data (Referencia Canónica)

## 1. RPCs SQL Determinísticas de PostgreSQL (Supabase)

| Función RPC | Propósito Operativo | Tablas Auditadas | Tipo |
| :--- | :--- | :--- | :---: |
| `funnel_conversion()` | Total de leads, etapas del embudo y % de conversión global | `crm_leads` | RPC |
| `funnel_velocity()` | Tiempo promedio de avance entre etapas (<72h meta) | `crm_leads`, `crm_event_log` | RPC |
| `revenue_by_period(p_from, p_to)` | Facturación e ingresos en rangos de fechas específicos | `bookings`, `atlas_payments` | RPC |
| `revenue_by_hotel()` | Ingresos brutos y netos desglosados por propiedad hotelera | `bookings`, `hotels_master` | RPC |
| `margin_analysis()` | Márgenes porcentuales y en USD por tipo de producto | `bookings`, `rates_data` | RPC |
| `stale_leads()` | Identificación en caliente de prospectos con >7 días sin actividad | `crm_leads` | RPC |
| `segment_summary()` | Distribución y comportamiento por tipo de viajero (Familia, Pareja, Grupo) | `crm_leads` | RPC |
| `crm_pipeline_stats()` | Rendimiento y velocidad de respuesta de ventas | `crm_leads`, `crm_event_log` | RPC |

---

## 2. Telemetría y Conexiones de Panel (/ariadne)
- `vps_metrics_reader`: Monitoreo de memoria RAM en tiempo real por cada nodo VPS.
- `atlas_tasks_reader`: Consulta de tareas activas del Swarm para cruce de avance.
- `logs_operativos_reader`: Auditoría de eventos en vivo (`ERROR`, `WARNING`, `INFO`).
- `exchange_rates_reader`: Lectura de la tasa soberana oficial (59.00 DOP/USD fija).

---

## 3. Conexiones Cognitivas y Alertas
- `agent_persistent_memory`: Acceso a 4 capas de memoria (`episodic`, `semantic`, `procedural`, `reflection_learning`).
- `intel_feed_receiver`: Ingesta de alertas de tarifas XML enviadas por **Atlas Intel**.
- `telegram_executive_alert`: Notificación directa de oportunidades con margen $\ge 20\%$ al Director General.
