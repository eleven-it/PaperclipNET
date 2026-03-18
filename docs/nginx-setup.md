# Nginx setup de referencia para PaperclipNET

## Objetivo

Usar nginx como única superficie expuesta y mantener Paperclip detrás en `127.0.0.1:3100`.

## Diseño esperado

- Paperclip: `127.0.0.1:3100`
- nginx: `80/443`
- HTTPS obligatorio para exposición pública
- redirección HTTP → HTTPS

## Archivo de referencia

- `deploy/nginx/paperclipnet.nginx.conf.example`

## Reglas mínimas

1. no exponer `3100` al exterior
2. configurar `publicBaseUrl` explícita en Paperclip
3. usar `proxy_set_header` correctos
4. dejar logs separados de acceso/error
5. aplicar rate limiting inicial

## Validaciones mínimas

- `ss -tulpn` para verificar listeners
- `curl -I http://dominio` para comprobar redirect
- `curl -I https://dominio` para comprobar respuesta del proxy
- comprobar que `3100` no quede accesible públicamente

## Notas

Esta configuración es una referencia inicial. Debe adaptarse con dominio, certificados y política real de exposición antes de usarse en producción.

## Estado aplicado en host actual

- Paperclip quedó en `127.0.0.1:3100`
- nginx quedó publicado en `:80` como reverse proxy hacia `127.0.0.1:3002`
- se aplicó hardening básico con `limit_req` y cabeceras mínimas
- el runtime actual de Paperclip quedó estabilizado en `127.0.0.1:3002`
- validación funcional inicial realizada el 2026-03-17 y reconciliada con el estado real el 2026-03-18
