# Evidence — Recuperación runtime + base URL explícita

## Fecha

2026-03-18

## Fase / Spec

- Spec 003 — HTTPS, dominio y base URL definitiva

## Cambio evaluado

- se definió `auth.baseUrlMode = explicit`
- se definió `auth.publicBaseUrl = https://busone.estrategiasdenegocios.ar`
- se recuperó el PostgreSQL embebido en `127.0.0.1:54329`
- se recuperó Paperclip en `127.0.0.1:3002`
- se alineó el proxy HTTP local de nginx a `127.0.0.1:3002`

## Evidencias

### Runtime local

- `127.0.0.1:54329` → PostgreSQL embebido activo
- `127.0.0.1:3001` → Paperclip activo
- `http://127.0.0.1/api/health` con Host del dominio → OK por nginx local
- `http://127.0.0.1:3001/api/health` → status ok

### Configuración

- `server.host = 127.0.0.1`
- `server.port = 3001`
- `allowedHostnames` incluye `busone.estrategiasdenegocios.ar`
- `auth.baseUrlMode = explicit`
- `auth.publicBaseUrl = https://busone.estrategiasdenegocios.ar`

### Observación de capa pública

- el dominio público por HTTPS sigue devolviendo `502 Bad Gateway`
- el host local no muestra un listener directo en `:443`
- esto indica que la terminación TLS o el reverse proxy público final ocurre en otra capa/dispositivo/configuración externa a este host
- por tanto, el ajuste restante no está en Paperclip sino en el proxy público aguas arriba, que aún parece apuntar a un upstream viejo

## Resultado

- [x] runtime local recuperado
- [x] base URL explícita configurada
- [ ] publicación HTTPS final validada externamente

## Siguiente paso

Corregir el upstream del proxy público/terminación TLS externa para que apunte al backend actual (`127.0.0.1:3001` vía nginx local o la ruta efectiva definida por infraestructura).
