# 🧠 Skill — Hermes Marketing

## Capacidades de marketing que puede ejecutar

---

## Categoría 1 — Creación de Contenido

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `copywriting` | Redacción de copy para ads, posts, emails | Brief + segmento + objetivo | Texto listo para approval |
| `visual_brief` | Brief visual para diseñador/Claude | Copy + formato + plataforma | Especificación de diseño |
| `email_sequence` | Secuencia de emails automatizados | Trigger + segmento + duración | N emails con timing |
| `lead_magnet_flow` | Funnel de lead magnet (landing → email → CTA) | Segmento + oferta | Landing copy + secuencia |

## Categoría 2 — Segmentación y Públicos (colaboración con Ariadne)

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `audience_from_crm` | Crea públicos desde datos CRM | Etapa pipeline + filtros | Lista de phones/emails para Meta |
| `audience_from_interactions` | Públicos por interacciones (WhatsApp, IG) | Tipo interacción + período | Segmento con criterios |
| `lookalike_builder` | Lookalike desde mejores clientes | % top clientes + plataforma | Custom audience → lookalike |
| `retargeting_stages` | Retargeting por etapa del embudo | Etapa + tiempo inactivo | Públicos + mensaje por etapa |

## Categoría 3 — Activación de Campañas ⭐ NUEVAS

| Skill | Descripción | Trigger | Output |
|-------|-------------|---------|--------|
| `ad_trigger_from_pipeline` ⭐ | Activa/pausa ads según etapa CRM | Lead cambia de etapa | Ad activado/pausado + log |
| `ads_platform_sync` ⭐ | Sincroniza públicos con Meta/Google | Segmento validado | Custom audience creada/actualizada |
| `campaign_launcher` | Lanza campaña completa | Brief aprobado | Campaña activa en Meta/Google |
| `campaign_pauser` | Pausa campaña por condición | ROAS bajo / budget agotado | Campaña pausada + alerta |

### ⭐ ad_trigger_from_pipeline — Detalle

```
Trigger: lead stage change in crm_leads
  ↓
Ariadne detecta cambio → evento en n8n
  ↓
Hermes Marketing recibe:
  {
    "lead_id": "uuid",
    "phone": "+1809XXXXXXX",
    "old_stage": "cotizacion_enviada",
    "new_stage": "en_pagos",
    "segment": "familia_premium"
  }
  ↓
Acción:
  - "cotizacion_enviada" → Activar ad de retargeting "Completa tu reserva"
  - "en_pagos" → Pausar ad de retargeting → Activar ad de cross-sell
  - "cerrado" → Pausar retargeting → Agregar a audience "viajeros_confirmados"
  - "perdido" → Activar ad de win-back con descuento
  ↓
Resultado: Ad activado/pausado en Meta Ads + log en crm_activities
```

### ⭐ ads_platform_sync — Detalle

```
Ariadne genera segmento → Hermes Marketing recibe:
  {
    "segment_name": "familia_premium_punta_cana",
    "phones": ["+1809XXXXXXX", ...],
    "emails": ["maria@...", ...],
    "criteria": "adults=2+children, budget=high, destination=punta_cana"
  }
  ↓
Hermes Marketing:
  1. Crea Custom Audience en Meta Ads API
  2. Sube lista de usuarios (phone + email matching)
  3. Genera Lookalike 1% si segmento >100
  4. Confirma sincronización → log en crm_activities
  ↓
Resultado: Audiencia disponible en Meta Ads Manager
```

## Categoría 4 — Medición y Optimización

| Skill | Descripción | Input | Output |
|-------|-------------|-------|--------|
| `campaign_report` | Reporte de rendimiento por campaña | Campaña + rango | ROAS, CPL, CTR, gasto |
| `creative_ab_test` | A/B test de creatividades | Variantes + duración | Ganador + significancia |
| `budget_optimizer` | Redistribuye presupuesto entre campañas | Rendimiento actual | Nueva asignación propuesta |

## Categoría 5 — Approval Workflow

| Skill | Descripción | Flujo |
|-------|-------------|-------|
| `request_approval` | Envía contenido al Director para approval | Contenido → Telegram → ✅/❌ |
| `schedule_publish` | Programa publicación post-approval | Horario + plataforma → cola |
| `alert_overspend` | Alerta si gasto >90% del presupuesto | Alerta inmediata → Director |

---

## Dependencias

| Variable | Uso |
|----------|-----|
| `META_ACCESS_TOKEN` | Meta Marketing API (Graph API v23.0) |
| `META_AD_ACCOUNT_ID` | Cuenta publicitaria |
| `META_PIXEL_ID` | Tracking de conversiones |
| `GOOGLE_ADS_TOKEN` | Google Ads API (futuro) |
| `SUPABASE_URL` | Lectura de segmentos y leads |
| `SUPABASE_ANON_KEY` | Acceso lectura CRM |
| `OPENROUTER_API_KEY` | Modelo para copywriting |
| `TELEGRAM_BOT_TOKEN` | Delivery de approvals |

---

*Hermes Marketing · Swarm Atlas Travel Solutions · v1.0*
