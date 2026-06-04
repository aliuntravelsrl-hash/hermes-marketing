# 🏗 Architecture — Hermes Marketing

---

## Posición en el enjambre

```
Ariadne (DATOS)          →  Hermes Marketing (ACCIÓN)  →  Meta/Google (PLATAFORMA)
─────────────────          ─────────────────────          ──────────────────
Segmentos                  Crea audiencias                Custom audiences
Lead scores                Activa/pausa ads               Campaigns live
Atribución                 Sincroniza públicos            Lookalikes
Anomalías                  Crea contenido                Ads publicados
```

Hermes Marketing es el **brazo ejecutor** de la inteligencia de Ariadne. Sin datos, no actúa. Sin Ariadne, es ciego.

---

## Modelo

| Componente | Modelo | Costo/1M tokens |
|-----------|--------|-----------------|
| Orquestador | `google/gemini-2.0-flash-lite-001` | $0.07 / $0.30 |
| Copywriting | `google/gemini-2.0-flash-lite-001` | $0.07 / $0.30 |
| Meta API calls | Directo (sin LLM) | $0 |

**Costo mensual estimado:** ~$3-5 USD (mayoría son API calls sin LLM)

---

## Infraestructura

| Componente | URL/Propósito |
|-----------|---------------|
| VPS2 Profile | `hermes profile marketing` |
| Gateway | Telegram (approvals) — sin WhatsApp directo |
| Meta API | Graph API v23.0 (post-verificación negocio) |
| n8n | Webhooks pipeline→ads, segment→sync |
| Supabase | Lectura de CRM para segmentación |

---

## Pre-requisitos para operar

| # | Requisito | Estado | Bloqueado por |
|---|----------|--------|---------------|
| 1 | Meta Business verificado | ⏳ En proceso | Incorporación legal (~1 mes) |
| 2 | Meta Access Token permanente | 🔴 Sin generar | Depende de #1 |
| 3 | Ad Account activa | 🔴 Sin crear | Depende de #1 |
| 4 | Meta Pixel configurado | 🔴 Sin configurar | Depende de #1 |
| 5 | n8n webhook pipeline→ads | 🔴 Sin configurar | Depende de #1 |
| 6 | Profile `marketing` en VPS2 | 🟢 Listo para crear | Sin bloqueo |
| 7 | Repo documentado | ✅ Este repo | — |

**Todo lo de Meta está bloqueado por la verificación legal.** Mientras tanto:
- ✅ Profile se crea
- ✅ Skills de contenido (copywriting, visual_brief) funcionan sin Meta
- ✅ Flujo de approval funciona
- ❌ Ad trigger, platform sync, campaign launcher → esperan Meta API

---

## Fases de activación

| Fase | Qué se activa | Cuándo |
|------|---------------|--------|
| **Fase 0 (ahora)** | Profile + repo + contenido + approval | Inmediato |
| **Fase 1 (post-legal)** | Meta API + Custom Audiences + Pixel | ~1 mes |
| **Fase 2 (post-data)** | ad_trigger_from_pipeline + lookalikes | ~2 meses |
| **Fase 3 (post-optimize)** | Budget optimizer + A/B testing + Google Ads | ~3 meses |

---

*Hermes Marketing · Swarm Atlas Travel Solutions · v1.0*
