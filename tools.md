# 🛠 Tools – Ariadne Data

## Herramientas de consulta, modelado y reporting

---

## Capa 1 — Tools nativas Supabase (consultas directas)

Queries SQL directas a PostgreSQL. Sin LLM intermedio. Resultado crudo + narrativa opcional.

| # | Tool | Propósito | Tablas | Tipo |
|---|------|-----------|--------|------|
| 1 | `funnel_conversion` | % conversión por etapa | `crm_leads` + `crm_deals` | RPC |
| 2 | `funnel_velocity` | Tiempo entre etapas | `crm_leads` + `crm_activities` | RPC |
| 3 | `revenue_by_period` | Ingresos por rango | `crm_deals` + `bookings` | RPC |
| 4 | `revenue_by_hotel` | Ingresos por hotel | `crm_deals` + `hotels_master` | RPC |
| 5 | `margin_analysis` | Márgenes brutos/netos | `crm_deals` + `rates` | RPC |
| 6 | `stale_leads` | Leads sin actividad >48h | `crm_leads` | RPC |
| 7 | `segment_summary` | Distribución por segmento | `client_profiles` | RPC |

### RPCs a crear en Supabase

```sql
-- Ejemplo: funnel_conversion
CREATE OR REPLACE FUNCTION public.funnel_conversion(
  p_from_date date DEFAULT CURRENT_DATE - 30,
  p_to_date date DEFAULT CURRENT_DATE
)
RETURNS jsonb AS $$
  SELECT jsonb_build_object(
    'nuevo', COUNT(*) FILTER (WHERE stage = 'nuevo_contacto'),
    'conversacion', COUNT(*) FILTER (WHERE stage = 'conversacion_inicial'),
    'descubrimiento', COUNT(*) FILTER (WHERE stage = 'descubrimiento'),
    'cotizacion', COUNT(*) FILTER (WHERE stage = 'cotizacion_enviada'),
    'cierre', COUNT(*) FILTER (WHERE stage = 'cierre'),
    'en_pagos', COUNT(*) FILTER (WHERE stage = 'en_pagos'),
    'cerrado', COUNT(*) FILTER (WHERE stage = 'cerrado'),
    'perdido', COUNT(*) FILTER (WHERE stage = 'perdido')
  )
  FROM crm_leads
  WHERE created_at BETWEEN p_from_date AND p_to_date + interval '1 day';
$$ LANGUAGE sql STABLE;
```

---

## Capa 2 — Tools de análisis (requieren LLM para interpretación)

| # | Tool | Propósito | Input | Output |
|---|------|-----------|-------|--------|
| 1 | `anomaly_detection` | Detecta desviaciones | métrica + ventana | alerta con causa probable |
| 2 | `lead_score` | Scoring predictivo | lead_id | score 0-100 + factores |
| 3 | `churn_risk` | Riesgo de abandono | lead_id o phone | probabilidad + señal + acción |
| 4 | `campaign_attribution` | Atribución multi-touch | campaign_id | first/last/assisted touch |
| 5 | `trend_narrative` | Genera narrativa de tendencia | datos crudos | texto ejecutivo |

---

## Capa 3 — Tools de reporting

| # | Tool | Propósito | Formato | Entrega |
|---|------|-----------|---------|---------|
| 1 | `daily_briefing` | Resumen matutino | Texto bullets | Telegram DM Director |
| 2 | `weekly_report` | Reporte semanal | Markdown | Telegram DM Director |
| 3 | `alert_format` | Formato de alerta estándar | Texto + dato | Destino según prioridad |

---

## Capa 4 — Tools de memoria (compartidas con Hermes Commercial)

| # | Tool | Propósito | Tabla |
|---|------|-----------|-------|
| 1 | `get_conversation_context` | Contexto completo de cliente | `client_profiles` + `conversation_messages` |
| 2 | `consultar_pipeline` | Estado del embudo | `crm_leads` + `crm_deals` |

---

## Dependencias

| Variable | Uso |
|----------|-----|
| `SUPABASE_URL` | Conexión a PostgreSQL |
| `SUPABASE_SERVICE_ROLE_KEY` | Acceso service role |
| `OPENROUTER_API_KEY` | Interpretación LLM |
| `TELEGRAM_BOT_TOKEN` | Entrega de reportes |
| `TELEGRAM_CHAT_ID` | DM del Director |

---

## Columnas auditadas Supabase (production)

Misma doctrina que Hermes Commercial: NUNCA asumir. Siempre auditar con `information_schema.columns`.

```
crm_leads:      id, phone, name, stage, source, created_at, updated_at
crm_deals:      id, lead_id, hotel_slug, total_usd, margin_pct, status, created_at
crm_activities:  id, lead_id, type, content, created_at
client_profiles: id, phone, name, segment, budget_level, total_bookings, total_revenue_usd
conversation_messages: id, conversation_id, lead_id, direction, sender_type, content, created_at
bookings:       id, deal_id, hotel_id, check_in, check_out, status
rates:          adult_rate, valid_from, valid_to, is_active
exchange_rates:  currency_pair, rate_sell, rate_buy, is_active
```

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
