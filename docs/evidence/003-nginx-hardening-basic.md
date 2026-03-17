# Evidence — Hardening básico de nginx

## Fecha

2026-03-17

## Fase / Spec

- Spec 002 — Nginx reverse proxy endurecido para PaperclipNET
- preparación parcial hacia Spec 003

## Cambio evaluado

- se añadió hardening básico real en nginx
- se añadieron zonas de `limit_req`
- se añadieron cabeceras de respuesta mínimas

## Evidencias

### Configuración aplicada

- `/etc/nginx/conf.d/paperclipnet-hardening.conf`
- `/etc/nginx/sites-available/default`

### Validación

- `nginx -t` exitoso
- nginx recargado correctamente
- listeners:
  - `:80` en nginx
  - `127.0.0.1:3100` en Paperclip

### Respuesta por proxy

`curl -I http://127.0.0.1/` devolvió `HTTP/1.1 200 OK` con cabeceras:

- `X-Frame-Options: SAMEORIGIN`
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`

## Resultado

- [x] aprobado

## Observaciones

- sigue pendiente HTTPS real
- sigue pendiente dominio/subdominio final
- `X-Powered-By: Express` aún aparece al pasar por proxy; podrá mitigarse más adelante si conviene

## Siguiente paso

Definir dominio final y completar Spec 003 para pasar a HTTPS/base URL explícita.
