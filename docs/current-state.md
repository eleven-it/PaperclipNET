# Estado actual de la instalación Paperclip

## Estado operativo

- Servicio Paperclip levantado y operativo
- Modo actual: `authenticated/private`
- Bind actual en la máquina: `192.168.0.187:3100`
- Health API verificado
- PostgreSQL embebido funcional

## Observaciones

- La instalación inicial requirió corrección manual del arranque del PostgreSQL embebido.
- La instancia fue migrada desde `local_trusted` a `authenticated/private` para permitir bind en LAN.
- Existe un flujo de `board claim` pendiente/mostrado al pasar a modo autenticado.
- Falta fijar `baseUrl` de autenticación para un despliegue público limpio.
- No hay proveedor LLM configurado todavía.

## No incluido en este repo

Por seguridad, este repositorio NO incluye:

- base de datos embebida
- backups SQL
- `master.key`
- `.env`
- logs
- secretos de autenticación

## Ruta local original

- Data dir local: `/home/ultron/.openclaw/workspace/paperclip-data`
