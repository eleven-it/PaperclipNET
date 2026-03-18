# Secrets and Config Policy

## Objetivo

Definir qué información puede versionarse y qué debe permanecer fuera del repositorio.

## Sí se versiona

- documentación
- specs y test plans
- plantillas de configuración
- ejemplos `.env`
- configuración nginx de referencia
- evidencia no sensible

## No se versiona

- `.env` reales
- claves privadas
- `master.key`
- dumps y backups de base de datos
- runtime local
- logs operativos
- secretos de terceros (tokens, API keys, credenciales)

## Ubicaciones esperadas

### Repo
- `config/` → plantillas y ejemplos
- `docs/` → documentación y evidencia
- `deploy/` → referencias de despliegue
- `runtime/` → reservado, no versionado

### Host / runtime real
- `paperclip-data/instances/default/.env`
- `paperclip-data/instances/default/secrets/master.key`
- `paperclip-data/instances/default/db/`
- `paperclip-data/instances/default/data/backups/`
- `paperclip-data/instances/default/logs/`

## Reglas

1. nunca subir secretos reales al repo
2. usar valores de ejemplo o placeholders en plantillas
3. mantener rutas sensibles fuera de ejemplos finales cuando sea posible
4. documentar claramente cualquier archivo local requerido para arrancar el sistema

## Observación actual

La instancia real usa un árbol runtime separado bajo `paperclip-data/instances/default/`, lo cual respeta el principio de separación entre repo y estado operativo.
