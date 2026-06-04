# 🛠 Tools — Hermes Marketing

---

## Capa 1 — Meta Marketing API (Graph API v23.0)

| # | Tool | Endpoint | Propósito |
|---|------|----------|-----------|
| 1 | `create_custom_audience` | `POST /v23.0/{ad_account}/customaudiences` | Crea audiencia en Meta |
| 2 | `upload_audience_users` | `POST /v23.0/{audience_id}/users` | Sube phones/emails |
| 3 | `create_lookalike` | `POST /v23.0/{ad_account}/customaudiences` | Genera lookalike 1% |
| 4 | `get_campaign_status` | `GET /v23.0/{campaign_id}` | Estado de campaña |
| 5 | `pause_campaign` | `POST /v23.0/{campaign_id}` status=PAUSED | Pausa campaña |
| 6 | `activate_campaign` | `POST /v23.0/{campaign_id}` status=ACTIVE | Activa campaña |
| 7 | `get_ad_insights` | `GET /v23.0/{ad_id}/insights` | Métricas (ROAS, CPL, CTR) |
| 8 | `update_ad_set_budget` | `POST /v23.0/{adset_id}` | Cambia presupuesto diario |

### Meta API — Config requerida

```yaml
meta:
  access_token: META_ACCESS_TOKEN        # System User permanente
  ad_account_id: act_<AD_ACCOUNT_ID>     # Cuenta publicitaria
  pixel_id: META_PIXEL_ID               # Tracking conversiones
  business_id: "541406196695825"         # Business Manager
  waba_id: "1664245875019293"            # WhatsApp Business
```

---

## Capa 2 — Tools de Sincronización ⭐ NUEVAS

### ⭐ ads_platform_sync

```python
# Pseudocode — implementación en n8n workflow + MCP tool
def ads_platform_sync(segment_name, phones, emails, criteria):
    """
    1. Crea Custom Audience en Meta Ads
    2. Sube usuarios (SHA256 hashed phone + email)
    3. Si segmento >100 usuarios → genera Lookalike 1%
    4. Retorna audience_id + status
    """
    audience = meta_create_custom_audience(
        name=f"ALIUN_{segment_name}",
        subtype="CUSTOM",
        description=criteria
    )
    
    meta_upload_users(
        audience_id=audience['id'],
        users=[{"phone": hash_sha256(p), "email": hash_sha256(e)} 
               for p, e in zip(phones, emails)]
    )
    
    if len(phones) >= 100:
        meta_create_lookalike(
            origin_audience_id=audience['id'],
            name=f"ALIUN_{segment_name}_Lookalike_1pct",
            country="DO"
        )
    
    return {"audience_id": audience['id'], "users_synced": len(phones)}
```

### ⭐ ad_trigger_from_pipeline

```python
# Pseudocode — implementación en n8n workflow
PIPELINE_AD_RULES = {
    "nuevo_contacto":    {"action": "none"},
    "conversacion_inicial": {"action": "activate", "ad_set": "awareness_destination"},
    "descubrimiento":     {"action": "activate", "ad_set": "retargeting_cotiza"},
    "cotizacion_enviada": {"action": "activate", "ad_set": "retargeting_completa"},
    "en_pagos":           {"action": "activate", "ad_set": "cross_sell_extras"},
    "cerrado":            {"action": "pause_all", "then": "welcome_email"},
    "perdido":            {"action": "activate", "ad_set": "winback_descuento", "window": "7d"},
}

def ad_trigger_from_pipeline(lead_id, phone, old_stage, new_stage):
    rule = PIPELINE_AD_RULES.get(new_stage, {"action": "none"})
    
    if rule["action"] == "activate":
        meta_activate_ad_set(rule["ad_set"], user_phone=phone)
    elif rule["action"] == "pause_all":
        meta_pause_retargeting(phone)
        send_welcome_email(lead_id)
    
    crm_log_activity(lead_id, f"ad_trigger: {old_stage}→{new_stage} → {rule['action']}")
```

---

## Capa 3 — Tools de Contenido (LLM-driven)

| # | Tool | Propósito | Modelo |
|---|------|-----------|--------|
| 1 | `copywriting` | Redacción de copy | gemini-2.0-flash-lite |
| 2 | `visual_brief` | Brief para diseñador | gemini-2.0-flash-lite |
| 3 | `email_sequence` | Secuencia de emails | gemini-2.0-flash-lite |
| 4 | `lead_magnet_flow` | Funnel lead magnet | gemini-2.0-flash-lite |

---

## Capa 4 — Tools de Lectura (compartidas con Ariadne)

| # | Tool | Fuente | Uso |
|---|------|--------|-----|
| 1 | `get_segment` | Supabase `client_profiles` | Leer segmentos |
| 2 | `get_lead_stage` | Supabase `crm_leads` | Verificar etapa |
| 3 | `get_campaign_data` | Meta API insights | Métricas campaña |

---

## Capa 5 — Tools de Approval

| # | Tool | Canal | Uso |
|---|------|-------|-----|
| 1 | `request_approval` | Telegram DM Director | Enviar contenido para ✅/❌ |
| 2 | `schedule_publish` | Meta API / cola interna | Programar post-approval |

---

*Hermes Marketing · Swarm Atlas Travel Solutions · v1.0*
