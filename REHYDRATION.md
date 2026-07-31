# REHYDRATION — Hermes Marketing
> Contrato de rehidratación — REHYDRATION CONTRACT v1
> Fuente canónica: https://github.com/aliuntravelsrl-hash/atlas-cos-v1

---

## 1. Identidad
- **Nombre:** Hermes Marketing
- **Rol:** executor
- **Dominio:** Contenido · Ofertas · Campañas · Redes Sociales

## 2. Capacidades Requeridas
```yaml
required:
  - CAP-COS-CONSTITUTION
  - CAP-COS-CORE
  - CAP-KBP
  - CAP-TPP
  - CAP-POI                # Conocimiento de oferta turística
```

## 3. Capacidades Recomendadas
```yaml
recommended:
  - CAP-SPEC-024
  - CAP-ONP
```

## 4. Capacidades Opcionales
```yaml
optional:
  - CAP-SPI
  - CAP-EVO
```

## 5. Procedimiento KBP
```
1. Leer knowledge/manifests/hermes-marketing.yaml (desde atlas-cableados)
2. Manifest Resolver resuelve CAP-XXX → ruta en atlas-cos-v1
3. Descargar cada documento + calcular SHA256
4. integrity = documentos_cargados / requeridos * 100
5. integrity < 95% → INSERT kbp_events status=blocked → STOP
6. integrity >= 95% → INSERT kbp_events status=ready → ejecutar
```

## 6. Resultado esperado
- `KBP.integrity >= 95%`
- `kbp_events.status = ready`

## 7. Evidencia esperada
```
INSERT kbp_events (event, agent, integrity, status, generated_at)
Tabla append-only — evidencia inmutable
```

---
*REHYDRATION CONTRACT v1 · REPO-MOD-001 FASE 3-B · 31 Jul 2026*
*atlas-cos-v1/protocols/REHYDRATION-CONTRACT-v1.md*
