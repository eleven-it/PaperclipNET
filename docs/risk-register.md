# Risk Register

## Objetivo

Registrar riesgos relevantes del proyecto de forma continua.

## Riesgos iniciales

### R-001 — Exposición directa del puerto 3100
- Impacto: alto
- Probabilidad: media
- Mitigación: nginx delante, bind loopback, validación de puertos

### R-002 — Secretos versionados accidentalmente
- Impacto: alto
- Probabilidad: media
- Mitigación: `.gitignore`, plantillas saneadas, revisión previa a commit

### R-003 — Configuración incoherente entre proxy y auth
- Impacto: medio-alto
- Probabilidad: media
- Mitigación: spec 003, validación de `publicBaseUrl`, pruebas de redirección

### R-004 — Rate limiting insuficiente
- Impacto: medio-alto
- Probabilidad: media
- Mitigación: spec 002 y 007, endurecimiento progresivo

### R-005 — Despliegue difícil de reproducir
- Impacto: medio
- Probabilidad: media
- Mitigación: runbooks, config ejemplo, checklist de promoción
