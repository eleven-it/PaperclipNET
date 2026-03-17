# Decision Log

## Objetivo

Registrar decisiones de arquitectura y proceso que afecten el proyecto.

## Decisiones actuales

### D-001
Se trabajará obligatoriamente con SDD y TDD antes de implementación relevante.

### D-002
Las ramas activas del proyecto son `1.0`, `Desarrollo` y `Staging`.

### D-003
Paperclip no debe exponerse directamente por `3100` a Internet.

### D-004
nginx será la capa de entrada prevista para despliegue seguro.

### D-005
Los secretos, runtime y artefactos sensibles quedan fuera del repositorio.
