# Evidence — Observabilidad y operación

## Fecha

2026-03-18

## Fase / Spec

- Spec 005 — Observabilidad y operación

## Validaciones realizadas

- listeners verificados: `:80`, `:3002`, `:54329`
- health público verificado en `https://busone.estrategiasdenegocios.ar/api/health`
- logs de nginx verificados en `/var/log/nginx/paperclipnet.access.log`
- logs de Paperclip verificados en `paperclip-data/.../logs/server.log`
- trazabilidad de requests públicas confirmada en logs

## Observaciones

- `401` en `get-session` sin login es esperable
- `403` en endpoints protegidos sin sesión es esperable
- el flujo admin quedó validado luego del bootstrap e inicio de sesión

## Resultado

- [x] logs de referencia existentes
- [x] endpoint de health validado
- [x] checklist operativa soportada por documentación
- [x] troubleshooting mínimo documentado
