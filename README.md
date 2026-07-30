# Ariadne Data
> Dominio: **Analytics · KPIs · Inteligencia Operativa · Self-Assessment**

## Identidad
**Rol en el swarm:** recommender
**Propósito:** Memoria ejecutiva del COS. Genera inteligencia operativa, reportes semanales y recomendaciones de prioridad para el Director.

## Dependencias
| Tipo | Fuente |
|------|--------|
| Constitución | [atlas-cos-v1](https://github.com/aliuntravelsrl-hash/atlas-cos-v1) |
| Protocolos activos | TPP-v1 · KBP-v1 · POI-v1 · SPI-v1 · ONP-v1 |
| MCP / Herramientas | Supabase · OpenRouter |
| Knowledge Manifest | `atlas-cableados/knowledge/manifests/ariadne-data.yaml` |

## Fuente Canónica
Toda doctrina, protocolo y especificación vive en **atlas-cos-v1**.
Este repositorio **implementa** — nunca duplica doctrina.

```
atlas-cos-v1 (Constitución)
      │
      ▼
Ariadne Data
(Implementación de dominio)
```

## Sub-agentes
escuchador_crm.py (daemon CRM)

## Repos relacionados
- `atlas-cos-v1` — fuente canónica del COS
- `atlas-cableados` — rehidratación y knowledge manifests
- `aliun-rrhh-v2` — perfiles RRHH-IA y roles

## Estado
`CONVERGENCIA EN PROGRESO` — REPO-MOD-001 Fase 2

## Últimos cambios
Ver commits del repositorio.

---
*Aliun Travel SRL · Director Aldo Hilario · ATLAS-TECH*
*COS-v3.5 · [atlas-cos-v1](https://github.com/aliuntravelsrl-hash/atlas-cos-v1)*
