# 📝 Onboarding RRHH IA — Hermes Marketing

## Fase 0 — Inmediato (sin Meta API)

| # | Acción | Comando | Resultado |
|---|--------|---------|-----------|
| 1 | Crear profile marketing | `hermes profile create marketing` | Profile independiente |
| 2 | Configurar modelo | `hermes profile use marketing && hermes model` | gemini-2.0-flash-lite |
| 3 | Verificar Supabase acceso | curl a `crm_leads?select=id&limit=1` | 200 OK |
| 4 | Verificar Telegram | Mensaje de prueba al Director | Confirmación |
| 5 | Test copywriting skill | "Escribe copy para carrusel Punta Cana familias" | Output funcional |

## Fase 1 — Post-verificación Meta (~1 mes)

| # | Acción | Requisito | Resultado |
|---|--------|-----------|-----------|
| 1 | Generar Access Token permanente | Meta Business verificado | Token válido |
| 2 | Crear Ad Account | Business Manager aprobado | act_XXXXXX |
| 3 | Configurar Pixel | Sitio web con DNS resuelto | Pixel ID activo |
| 4 | Crear Custom Audience test | >50 contacts en CRM | Audience creada |
| 5 | Test `ads_platform_sync` | Audience + token | Sincronización OK |
| 6 | Configurar webhook n8n | n8n + Meta webhook | Pipeline→ads activo |

## Fase 2 — Automatización pipeline→ads (~2 meses)

| # | Acción | Resultado |
|---|--------|-----------|
| 1 | Configurar `ad_trigger_from_pipeline` | 4 reglas activas |
| 2 | Crear lookalike desde top clientes | Lookalike 1% DO |
| 3 | Configurar retargeting por etapa | 5 ad sets activos |
| 4 | Test E2E: lead→etapa→ad activado | <30 min respuesta |
| 5 | Reporte ROAS automatizado | Weekly report al Director |

## Fase 3 — Optimización (~3 meses)

| # | Acción | Resultado |
|---|--------|-----------|
| 1 | A/B test de creatividades | Ganador con significancia |
| 2 | Budget optimizer semanal | Reasignación automática propuesta |
| 3 | Google Ads integration | Campaña Google piloto |
| 4 | Email sequence post-cotización | 3-email sequence activa |

---

## Checklist

- [ ] Fase 0: 5/5 checks OK
- [ ] Fase 1: 6/6 OK (bloqueado por verificación Meta)
- [ ] Fase 2: 5/5 OK (bloqueado por Fase 1)
- [ ] Fase 3: 4/4 OK (bloqueado por Fase 2)

**Hermes Marketing puede operar en Fase 0 HOY.** Las skills de contenido no requieren Meta API.

---

*Hermes Marketing · Swarm Atlas Travel Solutions · v1.0*