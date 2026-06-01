# 🔀 Routing Logic – Ariadne Data

## Cuándo se activa Ariadne y cómo recibe tareas

---

## Triggers de activación

### Automáticos (sin intervención humana)

| Trigger | Condición | Acción de Ariadne |
|---------|-----------|-------------------|
| Cron matutino | 08:00 RD diario | Genera `daily_briefing` → envía al Director |
| Cron semanal | Lunes 08:00 RD | Genera `weekly_report` → envía al Director |
| Anomalía | Métrica >2σ del promedio móvil 7d | Lanza `anomaly_detection` → alerta inmediata |
| Lead estancado | `crm_leads.updated_at` >48h sin cambio | Lanza `stale_lead_alert` → notifica a Ventas |
| Deal cerrado | Nuevo registro en `crm_deals` con status=closed | Actualiza `revenue_by_period` + `margin_analysis` |
| Nueva campaña | Registro en `marketing_offers` | Inicia tracking de `campaign_roi` |

### On-demand (por solicitud)

| Quién solicita | Tipo de solicitud | Ejemplo |
|----------------|------------------|---------|
| Director Aldo | `custom_query` | "¿Cuánto revenue generó Punta Cana este mes vs el anterior?" |
| Hermes Commercial | `funnel_dropoff` | "¿Por qué estamos perdiendo leads en etapa descubrimiento?" |
| QA Comercial | `funnel_velocity` | "¿Cuánto tarda un lead de cotización a depósito?" |
| Hermes Marketing | `campaign_roi` | "¿Qué ROI tiene la campaña de Semana Santa?" |

---

## Flujo de routing

```
EVENTO (cron / webhook / solicitud)
  ↓
ORQUESTADOR identifica tipo de tarea
  ↓
¿Es analítica? → SÍ → despacha a Ariadne
  ↓
Ariadne ejecuta skill correspondiente
  ↓
Genera output estructurado (dato + contexto + recomendación)
  ↓
Entrega al solicitante:
  - Director → Telegram DM
  - Hermes Commercial → API context injection
  - Hermes Marketing → API segment delivery
  - QA → CRM activity log
```

---

## Priorización de tareas

| Prioridad | Tipo | SLA interno |
|-----------|------|-------------|
| 🔴 P0 — Crítica | Anomalía operativa, SLA breach, data integrity | <1h |
| 🟡 P1 — Alta | Solicitud Director, lead scoring urgente | <4h |
| 🟢 P2 — Normal | Daily briefing, campaign attribution | <24h |
| ⚪ P3 — Baja | Custom queries, LTV updates, research | <48h |

---

## Formato de entrega estándar

Toda entrega de Ariadne sigue este formato:

```json
{
  "insight": "La tasa de conversión lead→cotización bajó 12% esta semana",
  "evidence": {
    "current": "48%",
    "previous": "60%",
    "trend": "declining_3d",
    "sample_size": 142
  },
  "context": "Corresponde al período post-cambio de prompt del vendedor v2.1",
  "recommendation": "Revertir cambio en nodo 03_AI_AGENT o hacer A/B test",
  "confidence": "high",
  "affected_departments": ["ventas", "qa"]
}
```

---

## Modelo y costo

| Componente | Modelo | Contexto | Costo/1M tokens |
|-----------|--------|----------|-----------------|
| Orquestador | `google/gemini-2.0-flash-lite-001` | 1M | $0.07 / $0.30 |
| Query engine | Direct PostgreSQL / Supabase RPC | — | $0 (sin LLM) |
| Reportes complejos | `google/gemini-2.0-flash-lite-001` | 1M | $0.07 / $0.30 |

La mayoría de las queries van directo a PostgreSQL sin pasar por LLM. Solo la interpretación y narrativa usa el modelo.

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
