# Evidence — Spec 002 / Test Plan 002

## Fecha

2026-03-17

## Fase / Spec

- Spec 002 — Nginx reverse proxy endurecido para PaperclipNET

## Test Plan

- Test Plan 002 — Nginx reverse proxy endurecido

## Cambio evaluado

- Paperclip reconfigurado para escuchar en `127.0.0.1:3100`
- nginx configurado como reverse proxy en el sitio por defecto sobre `:80`

## Evidencias

### Listeners verificados

- `0.0.0.0:80` → nginx
- `[::]:80` → nginx
- `127.0.0.1:3100` → Paperclip

### Proxy check

`curl -I http://127.0.0.1/` → `HTTP/1.1 200 OK`

Respuesta servida por nginx y reenviada a Paperclip.

### Direct internal check

`curl -I http://127.0.0.1:3100/` → `HTTP/1.1 200 OK`

### Validación relevante

- `nginx -t` exitoso
- nginx recargado correctamente
- Paperclip ya no escucha en la IP LAN

## Resultado

- [x] aprobado

## Observaciones

- Aún no se ha implementado HTTPS
- Aún no se aplicó rate limiting real en la configuración activa del host
- La configuración aplicada en nginx es mínima y funcional para la fase actual

## Siguiente paso

Continuar con Spec 003 (HTTPS/base URL) y endurecimiento adicional del proxy.
