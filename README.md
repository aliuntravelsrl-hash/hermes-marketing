# 🎨 Hermes Marketing — Agente de Marketing del Enjambre

## Propósito

Generar demanda, segmentar audiencias y activar campañas publicitarias basadas en datos del CRM. Hermes Marketing es el puente entre la inteligencia de Ariadne y las plataformas publicitarias (Meta Ads, Google Ads).

## Identidad

**Hermes Marketing** — el agente que convierte datos en demanda. Recibe segmentos de Ariadne, crea contenido, programa publicación y sincroniza con plataformas publicitarias.

## Arquitectura del Enjambre

```
                    ┌─────────────┐
                    │  Director   │
                    │  (Aldo)     │
                    └──────┬──────┘
                           │ Telegram
              ┌────────────┼────────────┐
              │            │            │
     ┌────────▼───┐  ┌────▼─────┐  ┌──▼──────────┐
     │  Hermes    │  │  Hermes  │  │  Hermes     │
     │  (Ops)     │  │Commercial│  │  Marketing  │
     │ +Ariadne   │  │ (Ventas) │  │ (Demand)    │
     └─────┬──────┘  └────┬─────┘  └──────┬──────┘
           │              │               │
           └─── Supabase (bus datos) ────┘
           └─── n8n (bus eventos) ──────┘
```

## 📦 Documentación

| Documento | Descripción |
|-----------|-------------|
| soul.md | Personalidad, tono y misión del agente |
| skill.md | Capacidades de marketing (creación + publicación) |
| department.md | Departamento Marketing y OKRs |
| routing_logic.md | Triggers de activación y priorización |
| tools.md | Herramientas nativas + Meta/Google APIs |
| architecture.md | Arquitectura y integración con enjambre |
| marketing_agent.md | Ficha técnica RRHH IA |
| cross_repo_notice.md | Contrato de datos con Ariadne + Commercial |
| rrhh_ia_onboarding.md | Procedimiento de incorporación |

## 🔗 Integración CRM → Marketing → Ads

| Funcionalidad | Agente responsable | Skill/Tool |
|---------------|-------------------|------------|
| Públicos desde conversaciones + intención | Ariadne | `audience_segmentation` + `crm_data_fetcher` |
| Recuperar leads abandonados | Ariadne detecta → Hermes ejecuta | `churn_prediction` + `lead_magnet_flow` |
| Activar/pausar ads por pipeline stage | Hermes Marketing | `ad_trigger_from_pipeline` ⭐ NEW |
| Públicos desde interacciones (WhatsApp, IG) | Ariadne | `audience_segmentation` con condiciones |
| Lookalike desde mejores clientes | Ariadne | `segment_builder` + `attribution_model_runner` |
| Sincronizar con Meta/Google Ads | Hermes Marketing | `ads_platform_sync` ⭐ NEW |

⭐ = Skills nuevas específicas de Marketing

---

Versión: 1.0  
Autor: Swarm Atlas Travel Solutions