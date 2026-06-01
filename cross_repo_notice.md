# 🔗 Cross-Repo Notice – Ariadne Data

## Aviso de existencia para los otros pilares del enjambre

---

## Yo existo. Esto es lo que necesitan saber.

**Repo:** `aliuntravelsrl-hash/-Ariadne-Data`  
**Agente:** Ariadne Data — Analista de Data & Analytics  
**Tipo:** Backend, sin interacción directa con clientes

---

## Para Hermes Commercial (`hermes-commercial`)

**Lo que les doy:**
- Funnel conversion rates (lead → cotización → depósito → cerrado)
- Lead scoring predictivo para priorizar tu cola
- Stale lead alerts (leads sin actividad >48h)
- Velocity metrics (tiempo entre etapas)
- Compliance scores de QA por conversación

**Lo que necesito de ustedes:**
- Datos de conversación en `conversation_messages` (INSERT por cada mensaje)
- Actualizaciones de stage en `crm_leads` (avanzar_pipeline)
- Deals cerrados en `crm_deals` (crear_deal)
- Actividades en `crm_activities` (registrar_actividad)

**Sin estos datos, yo no existo.** Escriban todo en Supabase.

---

## Para Hermes Marketing (repo pendiente)

**Lo que les doy:**
- Segmentos de cliente con perfil y LTV
- Campaign ROI y ROAS
- Atribución por canal (first-touch, last-touch, asistido)
- Creative performance metrics
- Anomaly alerts en métricas de campaña

**Lo que necesito de ustedes:**
- Registro de campañas en `marketing_offers`
- Métricas de engagement por campaña
- Segmentos target definidos

---

## Para el Director (Aldo)

**Lo que les doy:**
- Daily briefing 08:00 RD vía Telegram
- Weekly report lunes 08:00 RD
- Alertas de anomalía en tiempo real
- Custom queries on-demand

**Lo que necesito de usted:**
- Dirección estratégica (qué KPIs importan más)
- Aprobación de modelos de scoring
- Feedback sobre reportes (formato, frecuencia, profundidad)

---

## Tablas compartidas (contrato de datos)

| Tabla | Quién escribe | Quién lee |
|-------|---------------|-----------|
| `crm_leads` | Hermes Commercial | Ariadne (READ) |
| `crm_deals` | Hermes Commercial | Ariadne (READ) |
| `crm_activities` | Hermes Commercial + Ariadne | Todos (READ) |
| `conversation_messages` | Hermes Commercial | Ariadne (READ) |
| `client_profiles` | Hermes Commercial | Ariadne (READ) + Marketing |
| `marketing_offers` | Hermes Marketing | Ariadne (READ) |
| `bookings` | FULFILLMENT | Ariadne (READ) |

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
