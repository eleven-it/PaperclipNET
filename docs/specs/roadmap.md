# Roadmap SDD del proyecto

## Estado actual

- Spec 000 — Alcance global
- Spec 001 — Despliegue seguro y endurecimiento inicial
- Spec 002 — Nginx reverse proxy endurecido

## Siguientes specs previstas

### Spec 003 — HTTPS, dominio y base URL definitiva
Definir cómo se publicará el servicio con URL estable, TLS y redirecciones correctas.

### Spec 004 — Gestión de configuración y secretos
Definir estructura local, archivos de entorno, plantillas, variables y exclusiones.

### Spec 005 — Observabilidad, logs y validación operativa
Definir logs, healthchecks, checklist operativa y evidencias mínimas.

### Spec 006 — Staging, promoción y estrategia de ramas
Definir cómo se promueve desde `Desarrollo` a `Staging` y luego a línea base estable.

### Spec 007 — Hardening extendido y mitigación de abuso
Definir limitación de tasa ampliada, criterios para fail2ban, exposición controlada y posture de seguridad.

## Regla de avance

No se debe saltar a implementación significativa sin tener, como mínimo:

- spec redactada
- test plan asociado
- criterios de aceptación
- alcance y exclusiones
