# Spec 004 — Gestión de configuración y secretos

## Estado

Draft

## Objetivo

Definir el modelo de configuración del proyecto y la separación estricta entre artefactos versionados, runtime local y secretos.

## Alcance

- plantillas de config
- estructura `config/`, `runtime/`, `docs/`
- convenciones para `.env`
- exclusiones de git
- ubicaciones permitidas de secretos

## Criterios de aceptación

- existe convención documental de secretos
- existen plantillas sin valores sensibles
- `.gitignore` cubre artefactos críticos
- existe test plan asociado
