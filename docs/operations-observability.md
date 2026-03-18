# Operations & Observability

## Objetivo

Definir cómo observar y operar la instancia PaperclipNET en su estado actual.

## Runtime actual

- Paperclip: `0.0.0.0:3002`
- PostgreSQL embebido: `127.0.0.1:54329`
- Publicación externa: dominio `https://busone.estrategiasdenegocios.ar` mediante NAT/proxy externo

## Healthchecks

### Local app
```bash
curl http://127.0.0.1:3002/api/health
```

### Público
```bash
curl https://busone.estrategiasdenegocios.ar/api/health
```

## Logs relevantes

### Nginx local
- `/var/log/nginx/paperclipnet.access.log`
- `/var/log/nginx/paperclipnet.error.log`

### Paperclip
- `/home/ultron/.openclaw/workspace/paperclip-data/instances/default/logs/server.log`
- `/home/ultron/.openclaw/workspace/paperclip-data/instances/default/logs/embedded-postgres-runtime.log`
- `/home/ultron/.openclaw/workspace/paperclip-data/instances/default/logs/embedded-postgres-bootstrap.log`

## Señales operativas útiles

- `ss -tulpn | grep -E '(:3002|:54329|:80)\\b'`
- respuestas `200` en `/api/health`
- presencia de requests públicas con `host=busone.estrategiasdenegocios.ar` en `server.log`
- errores `401/403` esperables para endpoints protegidos sin sesión

## Troubleshooting rápido

### Si cae la app
- verificar listener en `3002`
- revisar `server.log`
- revisar si PostgreSQL sigue vivo en `54329`

### Si falla el dominio
- verificar primero `https://busone.estrategiasdenegocios.ar/api/health`
- si el local responde y el dominio no, revisar proxy/NAT externo

### Si falla auth
- comprobar `auth.publicBaseUrl`
- comprobar host/origin/trusted origins en logs
