# 🔀 Routing Logic — Hermes Marketing

## Triggers de activación

---

## Automáticos (evento-driven)

| Trigger | Fuente | Acción |
|---------|--------|--------|
| Lead cambia etapa | n8n webhook (crm_leads update) | `ad_trigger_from_pipeline` → activa/pausa ads |
| Segmento listo | Ariadne → n8n webhook | `ads_platform_sync` → sube audience a Meta |
| Gasto >90% budget | Meta webhook / cron check | `alert_overspend` → alerta Director |
| Lead estancado >48h | Ariadne stale_leads scan | `lead_magnet_flow` → secuencia win-back |
| Deal cerrado | crm_deals insert | Agregar a audience "viajeros_confirmados" |

## On-demand (por solicitud Director)

| Solicitud | Flujo | SLA |
|-----------|-------|-----|
| "Crear campaña Semana Santa" | Brief → Copy → Approval → Publicar | <4h hasta preview |
| "¿ROAS de la campaña X?" | Query Meta API → Reporte | <1h |
| "Pausar campaña Y" | Meta API pause → Confirmación | <15 min |
| "Nuevo lead magnet para familias" | Copy + Visual brief → Approval | <8h hasta preview |

## Priorización

| Prioridad | Tipo | SLA |
|-----------|------|-----|
| 🔴 P0 | Overspend, ad rechazado, error sync | <15 min |
| 🟡 P1 | Solicitud Director, campaign launcher | <4h |
| 🟢 P2 | Segmentación rutinaria, content calendar | <24h |
| ⚪ P3 | A/B tests, budget optimizer, research | <48h |

---

## Flujo pipeline → ads (automático)

```
LEAD STAGE CHANGE (Supabase trigger → n8n)
  ↓
n8n webhook: {lead_id, phone, old_stage, new_stage, segment}
  ↓
Hermes Marketing evalúa regla:
  
  nuevo_contacto → NO ad (aún sin cotización)
  conversacion_inicial → Activar awareness ads (destino + beneficios)
  descubrimiento → Retargeting "Cotiza tu viaje"
  cotizacion_enviada → Retargeting "Completa tu reserva" + urgencia
  en_pagos → Cross-sell (seguro viaje, excursiones)  
  cerrado → Pausar retargeting → Welcome journey email
  perdido → Win-back ad (descuento limitado, 7d ventana)
  ↓
Ejecuta Meta API call → Log en crm_activities
```

---

*Hermes Marketing · Swarm Atlas Travel Solutions · v1.0*
