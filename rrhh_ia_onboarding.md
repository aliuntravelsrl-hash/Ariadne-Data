# 📝 Onboarding RRHH IA – Ariadne Data

## Procedimiento de incorporación de Ariadne al enjambre

---

## Fase 1 — Verificación de acceso (5 min)

| # | Verificación | Comando | Resultado esperado |
|---|-------------|---------|-------------------|
| 1 | Supabase conexión | `curl -s SUPABASE_URL/rest/v1/crm_leads?select=id&limit=1` | 200 OK |
| 2 | Tabla crm_leads existe | Query `information_schema.columns` WHERE table_name='crm_leads' | Columnas visibles |
| 3 | Tabla crm_deals existe | Mismo método | Columnas visibles |
| 4 | Tabla conversation_messages existe | Mismo método | Columnas visibles |
| 5 | Tabla client_profiles existe | Mismo método | Columnas visibles |
| 6 | OpenRouter API key activa | `curl -s https://openrouter.ai/api/v1/models -H "Authorization: Bearer $KEY"` | Lista de modelos |
| 7 | Telegram bot activo | Mensaje de prueba al chat del Director | Confirmación |

---

## Fase 2 — Despliegue de RPCs (15 min)

Crear las RPCs analíticas en Supabase:

| # | RPC | Propósito | Dependencias |
|---|-----|-----------|-------------|
| 1 | `funnel_conversion(p_from_date, p_to_date)` | % conversión por etapa | `crm_leads` |
| 2 | `funnel_velocity(p_from_date, p_to_date)` | Tiempo entre etapas | `crm_leads` + `crm_activities` |
| 3 | `revenue_by_period(p_from_date, p_to_date)` | Ingresos por rango | `crm_deals` |
| 4 | `revenue_by_hotel(p_from_date, p_to_date)` | Ingresos por hotel | `crm_deals` + `hotels_master` |
| 5 | `margin_analysis(p_from_date, p_to_date)` | Márgenes | `crm_deals` |
| 6 | `stale_leads(p_hours)` | Leads sin actividad | `crm_leads` |
| 7 | `segment_summary()` | Distribución por segmento | `client_profiles` |

**Nota:** Todos los parámetros con prefijo `p_` (convención del proyecto).

---

## Fase 3 — Cableado de cron jobs (10 min)

| # | Job | Horario | Entrega | Prompt |
|---|-----|---------|---------|--------|
| 1 | Daily briefing | `0 12 * * *` (08:00 RD) | Telegram Director | "Genera el daily briefing operativo. Ejecuta funnel_conversion, stale_leads, revenue_by_period para hoy. Formato bullets con emoji." |
| 2 | Weekly report | `0 12 * * 1` (Lunes 08:00 RD) | Telegram Director | "Genera weekly report ejecutivo. Compara semana actual vs anterior. Incluye tendencias, top 5 hoteles, anomalías detectadas." |
| 3 | Stale leads scan | `0 */4 * * *` (cada 4h) | Telegram Director + Hermes Commercial | "Ejecuta stale_leads(p_hours:=48). Si hay resultados, lista leads con teléfono y stage." |

---

## Fase 4 — Verificación E2E (10 min)

| # | Test | Método | Resultado esperado |
|---|------|--------|-------------------|
| 1 | Daily briefing se genera | `hermes cron run <id>` | Mensaje llega a Telegram |
| 2 | Funnel RPC responde | `curl` directo a Supabase | JSON con datos |
| 3 | Alerta de stale lead funciona | Crear lead de test, no actualizar 48h | Alerta generada |
| 4 | Custom query responde | Solicitar query por Telegram | Respuesta con dato + contexto |

---

## Fase 5 — Documentación cruzada (5 min)

| # | Acción | Destino |
|---|--------|---------|
| 1 | Actualizar `cross_repo_notice.md` en Hermes Commercial | `aliuntravelsrl-hash/hermes-commercial` |
| 2 | Crear entrada en Notion War Room | BD3 Enchufes o BD4 Incidentes |
| 3 | Actualizar memoria de Hermes | `memory` tool |

---

## Checklist de onboarding completado

- [ ] Fase 1: Verificación de acceso — 7/7 checks OK
- [ ] Fase 2: RPCs desplegadas — 7/7 funcionando
- [ ] Fase 3: Cron jobs configurados — 3/3 activos
- [ ] Fase 4: E2E test — 4/4 pasando
- [ ] Fase 5: Documentación cruzada — 3/3 completada

**Cuando todo esté ✓, Ariadne está operativa.**

---

*Ariadne Data · Swarm Atlas Travel Solutions · v1.0*
