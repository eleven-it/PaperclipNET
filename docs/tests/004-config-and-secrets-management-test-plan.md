# Test Plan 004 — Gestión de configuración y secretos

## Estado

Draft

## Casos mínimos

- validar que no se versionen `.env`, keys, dumps, runtime
- validar existencia de config de ejemplo
- validar que las rutas de ejemplo sean portables
- validar separación entre documentación y estado local

## Negativas

- no aceptar secretos en repo
- no aceptar rutas absolutas sensibles en plantillas finales
