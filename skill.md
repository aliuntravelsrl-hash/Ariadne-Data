# 🧠 Skills — Ariadne Data (Referencia Canónica)

## 1. `skill-profit-margin-engine` (Modelador de Rentabilidad y Markup)
- **Propósito:** Procesar las alertas de tarifas netas XML reportadas por Atlas Intel y calcular el precio óptimo de venta.
- **Entradas:** Tarifa neta de proveedor, impuestos, tasa soberana (59.00) y precio público de OTAs.
- **Salida:** Propuesta de PVP, margen neto proyectado ($ y %) y proyección de beneficio total.

## 2. `skill-funnel-health-diagnostics` (Auditor de Embudo y Leads Estancados)
- **Propósito:** Detectar fugas de conversión y abandono de clientes en el pipeline.
- **Entradas:** `funnel_conversion()` y `stale_leads()`.
- **Salida:** Alertas a Hermes Commercial con la lista priorizada de prospectos por reactivar.

## 3. `skill-ltv-retention-analyst` (Analista de Valor de Vida y Cross-Selling)
- **Propósito:** Medir la recurrencia y la efectividad del empaquetamiento (Hotel + Traslado + Excursión).
- **Salida:** Ratio de Cross-Selling por propiedad y recomendaciones de empaquetamiento a Marketing.

## 4. `skill-executive-briefing` (Sintetizador Ejecutivo para el Director General)
- **Propósito:** Redactar diagnósticos concisos, comprensibles y accionables para la toma de decisiones soberanas.
- **Formato:** Hecho Numérico ➔ Diagnóstico ➔ Impacto Financiero ➔ Acción Sugerida.
