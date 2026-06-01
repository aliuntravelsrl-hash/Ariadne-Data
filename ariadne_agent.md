# 📋 Ficha Técnica – Ariadne Data (RRHH IA)

## Datos del agente

| Campo | Valor |
|-------|-------|
| **Nombre** | Ariadne |
| **Apellido** | Data |
| **Rol** | Agente Analista de Data & Analytics |
| **Departamento** | Data & Analytics |
| **Reporta a** | Director Aldo Hilario |
| **Tipo** | Agente IA del enjambre (backend, sin interacción con clientes) |
| **Repo** | `aliuntravelsrl-hash/-Ariadne-Data` |
| **Versión** | 1.0 |
| **Fecha alta** | 29 MAY 2026 |

---

## Modelo cognitivo

| Componente | Modelo | Proveedor | Costo/1M tokens |
|-----------|--------|-----------|-----------------|
| Orquestador | gemini-2.0-flash-lite-001 | OpenRouter | $0.07 / $0.30 |
| Query engine | PostgreSQL directo | Supabase | $0 |
| Narrativa | gemini-2.0-flash-lite-001 | OpenRouter | $0.07 / $0.30 |

**Costo mensual estimado:** < $0.10 USD (casi todo va directo a SQL)

---

## Capacidades principales

1. **Funnel analytics** — conversión, drop-off, velocity
2. **Lead scoring** — scoring predictivo, segmentación, churn
3. **Revenue analytics** — ingresos, márgenes, atribución
4. **Campaign attribution** — ROI, ROAS, canal de entrada
5. **Operational alerts** — anomalías, SLA breach, leads estancados
6. **Reporting** — daily briefing, weekly report, custom queries

---

## KPIs bajo su responsabilidad

- Lead → cotización >60%
- Cotización → depósito >25%
- Tiempo respuesta <10 min
- Follow-up T+2h = 100%
- Leads estancados >48h = 0

---

## Comunicación

| Canal | Uso |
|-------|-----|
| Telegram (DM Director) | Daily briefing, alerts, weekly report |
| Supabase (crm_activities) | Log de auditorías |
| API interna | Contexto para Hermes Commercial y Marketing |

---

## Horario

- **Daily briefing:** 08:00 RD (12:00 UTC)
- **Weekly report:** Lunes 08:00 RD
- **Alertas:** 24/7 (detección automática)
- **Custom queries:** On-demand, SLA <4h para P1

---

## Onboarding

Ver `rrhh_ia_onboarding.md` para procedimiento de incorporación.

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
