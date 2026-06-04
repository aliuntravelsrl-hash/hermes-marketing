# 🔗 Cross-Repo Notice — Hermes Marketing

## Aviso para los otros pilares del enjambre

---

**Repo:** `aliuntravelsrl-hash/hermes-marketing`
**Agente:** Hermes Marketing — Generación de demanda y campañas
**Tipo:** Backend + Telegram (approval), sin interacción directa con clientes

---

## Para Ariadne Data (`aliuntravelsrl-hash/Ariadne-Data`)

**Lo que necesito de ustedes:**
- Segmentos validados (`audience_segmentation`) → SIN segmento, NO lanzo campaña
- Lead scores para targeting
- Lookalike base (top 20% clientes)
- Atribución de campaña (ROAS por segmento)
- Anomalías en métricas de ads

**Lo que les doy:**
- Datos de campaña (CTR, CPL, ROAS, gasto)
- Custom audience IDs creados
- Logs de ad_trigger_from_pipeline
- Resultados de A/B tests

---

## Para Hermes Commercial (`aliuntravelsrl-hash/hermes-commercial`)

**Lo que necesito de ustedes:**
- Feedback de ventas (qué copy funciona en conversación)
- Deals cerrados → para audience "viajeros_confirmados"
- Leads perdidos → para win-back campaigns

**Lo que les doy:**
- Leads calificados desde ads (Meta → Supabase)
- Contenido de conversión (copy que testeo en ads)
- Retargeting activo por etapa del lead

---

## Para el Director (Aldo)

**Lo que les doy:**
- Propuestas de contenido → Telegram (✅/❌)
- Weekly marketing report (ROAS, CPL, top campaigns)
- Alertas de overspend (>90% budget)
- Recomendaciones de budget optimizer

**Lo que necesito de usted:**
- Aprobación de contenido (✅ o ❌ con feedback)
- Budget mensual definido
- Dirección creativa (tone, temas, prioridades)

---

## Tablas compartidas (contrato de datos)

| Tabla | Quién escribe | Quién lee |
|-------|---------------|-----------|
| `crm_leads` | Commercial | Marketing (READ) + Ariadne (READ) |
| `crm_deals` | Commercial | Marketing (READ) + Ariadne (READ) |
| `crm_activities` | Commercial + Marketing + Ariadne | Todos (READ) |
| `client_profiles` | Commercial | Marketing (READ) + Ariadne (READ) |
| `custom_audiences` ⭐ NEW | Marketing | Ariadne (READ) |
| `campaign_logs` ⭐ NEW | Marketing | Ariadne (READ) |

⭐ = Tablas nuevas a crear en Supabase cuando Meta API esté disponible

---

*Hermes Marketing · Swarm Atlas Travel Solutions · v1.0*