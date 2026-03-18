# Evidence — Revisión de configuración y secretos

## Fecha

2026-03-18

## Fase / Spec

- Spec 004 — Gestión de configuración y secretos

## Validaciones realizadas

- existe `.gitignore` con exclusión de `.env`, keys, dumps, runtime y logs
- existe `config/paperclip.config.example.json` sin secretos reales
- se añadió `config/.env.example` con placeholders
- se documentó política de secretos y configuración
- el runtime real está separado del repo bajo `paperclip-data/instances/default/`

## Hallazgos

- el repo no contiene `master.key` real de Paperclip
- el repo no contiene `.env` real del runtime
- la base de datos embebida y backups permanecen fuera del repo del proyecto

## Resultado

- [x] separación repo/runtime validada
- [x] plantilla de config validada
- [x] exclusiones de git validadas
- [x] política documental de secretos definida
