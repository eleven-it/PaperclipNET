# Validation Checklist

## Documentación
- [ ] Existe spec aplicable
- [ ] Existe test plan aplicable
- [ ] Existen criterios de aceptación claros

## Configuración
- [ ] `config/paperclip.config.example.json` usa loopback
- [x] `publicBaseUrl` está definida para exposición pública
- [ ] No hay secretos en el repo

## Red y proxy
- [ ] nginx escucha en `80/443`
- [ ] Paperclip escucha en `127.0.0.1:3100`
- [ ] `3100` no está expuesto externamente
- [ ] el proxy reenvía correctamente al upstream

## Seguridad básica
- [ ] existe rate limiting inicial
- [ ] existe estrategia HTTPS
- [ ] existen logs de acceso/error del proxy

## Operación
- [ ] el healthcheck responde por la ruta esperada
- [ ] el despliegue puede explicarse/repetirse con la documentación disponible
