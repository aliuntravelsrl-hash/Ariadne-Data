# 🔍 Swarm Agency Agents – Ariadne Data

Ariadne es la agente analista del enjambre. Su misión es transformar cada interacción, clic y conversación en inteligencia accionable para que Hermes Marketing y el departamento de ventas tomen decisiones basadas en datos, no en intuiciones.

## 📦 Documentación de la agente

| Documento | Descripción |
|-----------|-------------|
| soul.md | Personalidad, tono y misión de la agente |
| skill.md | Capacidades analíticas que puede ejecutar |
| department.md | Departamento de Data & Analytics y sus OKRs |
| routing_logic.md | Cuándo se activa Ariadne y cómo recibe tareas |
| tools.md | Herramientas de consulta, modelado y reporting |
| architecture.md | Arquitectura de la agente dentro del enjambre |
| ariadne_agent.md | Ficha técnica oficial para RRHH IA |
| cross_repo_notice.md | Aviso de existencia para los otros pilares |
| rrhh_ia_onboarding.md | Documento de onboarding para RRHH IA |

## 🔗 Integración en el sistema existente

- **PostgreSQL**: fuente de verdad para todos los datos de leads, eventos, ventas y viajes
- **CRM**: obtiene perfiles de cliente cerrados y datos de fidelización
- **Hermes Marketing**: recibe segmentos, puntuaciones y alertas; devuelve datos de campaña
- **Ventas (QA)**: consume reportes de conversión y atribución; envía resultados de llamadas
- **Hermes Commercial**: consume métricas de conversión por lead; recibe auditorías de QA

Ariadne es el pegamento que convierte el ruido operativo en una máquina de mejora continua.

---

Versión: 1.0  
Autor: Swarm Atlas Travel Solutions
