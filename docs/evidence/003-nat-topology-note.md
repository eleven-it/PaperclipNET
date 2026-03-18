# Evidence — Topología NAT externa para dominio final

## Fecha

2026-03-18

## Contexto confirmado

El dominio público no entra directamente a este host por `:443`.

Topología informada:

- dominio / proxy externo en otro equipo
- upstream externo hacia `190.3.87.108:33341`
- NAT hacia `192.168.0.187:3002`

## Implicación técnica

Para que Paperclip funcione en esta topología, el servicio local no puede quedar bind en `127.0.0.1:3002`.

Debe escuchar en:

- `0.0.0.0:3002` o
- `192.168.0.187:3002`

## Conclusión

La configuración local debe priorizar compatibilidad con NAT externo hacia `3002`, no solo reverse proxy local en loopback.
