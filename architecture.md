# 🏗 Architecture – Ariadne Data

## Arquitectura de la agente dentro del enjambre

---

## Posición en el swarm

```
                    ┌─────────────┐
                    │  Director   │
                    │  (Aldo)     │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
     ┌────────▼───┐  ┌────▼─────┐  ┌──▼──────────┐
     │  Hermes    │  │  Hermes  │  │  Ariadne    │
     │ Commercial │  │ Marketing│  │  Data       │
     │ (Ventas)   │  │ (Mktg)   │  │ (Analytics) │
     └─────┬──────┘  └────┬─────┘  └──────┬──────┘
           │              │               │
           │   ┌──────────┼───────────────┘
           │   │          │
     ┌─────▼───▼──────────▼──────┐
     │     Supabase PostgreSQL   │
     │  (fuente de verdad)       │
     └───────────────────────────┘
```

Ariadne **no interactúa con clientes**. Es un agente de backend que lee datos, genera inteligencia y la distribuye.

---

## Flujo de datos

```
DATOS ENTRAN:
  Hermes Commercial → crm_leads, crm_deals, conversation_messages
  Hermes Marketing → marketing_offers, campaign_metrics
  Clientes WhatsApp → conversation_messages (inbound)
  Meta Cloud API → wa_message_status events

ARIADNE PROCESA:
  1. Lee Supabase (PostgreSQL queries directas)
  2. Ejecuta skills analíticos (con o sin LLM)
  3. Genera insights estructurados

ARIADNE ENTREGA:
  Director → Telegram DM (daily briefing, alerts, weekly report)
  Hermes Commercial → API context (funnel data, lead scores)
  Hermes Marketing → API segments (campaign ROI, attribution)
  QA Comercial → CRM activities (audit results, compliance scores)
```

---

## Modelo

**Orquestador:** `google/gemini-2.0-flash-lite-001` ($0.07/$0.30 por 1M)

La mayoría de las queries van directo a PostgreSQL sin LLM. Solo interpretación y narrativa usa el modelo.

### Costo mensual estimado
- Queries SQL directas: **$0** (sin LLM)
- Daily briefing narrativo: ~2K tokens/día = **$0.01/mes**
- Weekly report narrativo: ~5K tokens/semana = **$0.02/mes**
- Alertas + interpretación ad-hoc: ~20K tokens/mes = **$0.03/mes**
- **Total estimado: < $0.10/mes** (casi todo va directo a SQL)

---

## Infraestructura

| Componente | URL/Path | Propósito |
|-----------|----------|-----------|
| Supabase | `oyihiyivdhfxpyiwnmqk.supabase.co` | Fuente de verdad (SSOT per Constitution §VIII) |
| MCP Server | `https://n8n-atlas-sales-mcp.xaruuo.easypanel.host/mcp` | Tools RPC |
| n8n | `https://n8n-n8n.xaruuo.easypanel.host` | Orquestación workflows |
| Telegram Bot | `@Hermes_ALDO_bot` | Entrega de reportes |

---

## Tablas que lee (lectura为主, escritura mínima)

| Tabla | Permisos | Uso |
|-------|---------|-----|
| `crm_leads` | READ | Funnel, scoring, stale leads |
| `crm_deals` | READ | Revenue, margins, attribution |
| `crm_activities` | READ + INSERT | Lee historial, escribe auditorías |
| `conversation_messages` | READ | Análisis de conversación, response time |
| `client_profiles` | READ | Segmentación, LTV |
| `marketing_offers` | READ | Campaign tracking |
| `hotels_master` | READ | Revenue por hotel |
| `bookings` | READ | Revenue confirmation |
| `exchange_rates` | READ | Conversión USD/DOP |

**Ariadne escribe MÍNIMAMENTE:** solo logs de auditoría en `crm_activities` y alertas.

---

## Separación de responsabilidades

| Lo que Ariadne HACE | Lo que Ariadne NO hace |
|--------------------|-----------------------|
| Analizar datos | Hablar con clientes |
| Generar reportes | Tomar decisiones operativas |
| Detectar anomalías | Ejecutar acciones sobre leads |
| Proponer recomendaciones | Implementar cambios en prompts |
| Calcular scores | Asignar agentes a leads |

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
