# Spec 004 — Gestión de configuración y secretos

## Estado

Done

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

## Cierre de spec

La spec se considera cerrada porque:

- existe `config/paperclip.config.example.json` sin valores sensibles reales
- existe `config/.env.example` con placeholders
- `.gitignore` excluye `.env`, claves, runtime, logs y dumps
- el runtime real vive fuera del repo bajo `paperclip-data/instances/default/`
- existe política documental explícita para configuración y secretos
