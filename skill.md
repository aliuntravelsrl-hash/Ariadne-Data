# 🧠 Skill – Ariadne Data

## Capacidades analíticas que puede ejecutar

---

## Categoría 1 — Funnel Analytics

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `funnel_conversion` | Tasa de conversión por etapa del embudo | rango de fechas | % por etapa, drop-off, benchmark |
| `funnel_dropoff` | Detección de fugas en el embudo | etapa específica | causas probables, top 3 razones |
| `funnel_velocity` | Tiempo promedio entre etapas | lead_id o rango | días/horas por transición |

## Categoría 2 — Lead Scoring

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `score_lead` | Puntuación predictiva de cierre | lead_id o phone | score 0-100, factores, probabilidad |
| `segment_leads` | Segmentación automática | criterios o auto | clusters con perfil y tamaño |
| `churn_prediction` | Predicción de abandono | lead_id o rango | probabilidad, señal de riesgo, acción sugerida |

## Categoría 3 — Revenue Analytics

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `revenue_by_period` | Ingresos por período | rango fechas, granularidad | total, promedio, tendencia |
| `revenue_by_hotel` | Ingresos por hotel/destino | hotel_slug o zona | ranking, share, ADR promedio |
| `revenue_by_segment` | Ingresos por segmento cliente | segmento | valor promedio, LTV, frecuencia |
| `margin_analysis` | Análisis de márgenes | rango fechas | margen bruto/neto, excepciones |

## Categoría 4 — Campaign Attribution

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `campaign_roi` | ROI por campaña | campaign_id o rango | gasto, revenue, ROAS, CPA |
| `channel_attribution` | Atribución por canal de entrada | rango fechas | last-touch, first-touch, asistido |
| `creative_performance` | Rendimiento por tipo de contenido | tipo o plataforma | CTR, conversión, costo por lead |

## Categoría 5 — Operational Alerts

| Skill | Descripción | Trigger | Output |
|-------|-------------|---------|--------|
| `anomaly_detection` | Detecta desviaciones significativas | >2σ del promedio móvil | alerta con contexto y causa probable |
| `sla_breach` | Incumplimiento de SLA interno | tiempo > umbral | tipo, lead afectado, acción sugerida |
| `stale_lead_alert` | Leads sin actividad >48h | crm_leads.updated_at | lista de leads, prioridad, agente asignado |

## Categoría 6 — Reporting

| Skill | Descripción | Frecuencia | Output |
|-------|-------------|------------|--------|
| `daily_briefing` | Resumen operativo matutino | 08:00 RD diario | KPIs clave, alertas, oportunidades |
| `weekly_report` | Reporte semanal ejecutivo | Lunes 08:00 RD | tendencias, ranking, predicciones |
| `custom_query` | Consulta ad-hoc del Director | On-demand | resultado estructurado + visualización |

---

## Fuentes de datos

| Fuente | Tablas principales | Tipo |
|--------|-------------------|------|
| Supabase (MCP) | `crm_leads`, `crm_deals`, `crm_activities`, `conversation_messages`, `client_profiles`, `bookings`, `rates` | PostgreSQL |
| Supabase (MCP) | `marketing_offers`, `hotels_master`, `rooms` | PostgreSQL |
| n8n | Ejecuciones de workflows, logs de agentes | API |
| Meta Business | Métricas de campaña WA | API (futuro) |

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
