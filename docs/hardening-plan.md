# Plan inicial de configuración y endurecimiento

## Objetivo

Publicar Paperclip de forma controlada, evitando exposición directa del puerto de aplicación y reduciendo riesgo frente a:

- fuerza bruta
- escaneo automatizado
- abuso de sesiones
- denegación de servicio básica

## Recomendación de arquitectura

1. Paperclip escuchando solo en loopback (`127.0.0.1:3100`)
2. Nginx como reverse proxy delante
3. HTTPS obligatorio
4. rate limiting en rutas sensibles
5. fail2ban o control equivalente en logs de nginx
6. opcional: Cloudflare o proxy perimetral
7. nunca exponer directamente el puerto 3100 a Internet

## Estado deseado

- `deploymentMode: authenticated`
- `exposure: private` si acceso restringido por VPN/LAN/reverse proxy interno
- `exposure: public` solo cuando exista:
  - `publicBaseUrl` explícita
  - HTTPS válido
  - control de origen/hostnames
  - reverse proxy endurecido

## Medidas mínimas

- `auth.baseUrlMode = explicit`
- `auth.publicBaseUrl = https://paperclip.tudominio`
- bind local o interno controlado
- protección perimetral en nginx
- ocultar `X-Powered-By` cuando sea posible desde proxy
- registrar y vigilar intentos de acceso

## Riesgos detectados

- Paperclip no demuestra por sí solo protección robusta anti-DDoS
- no hay evidencia clara de MFA madura por defecto
- no hay evidencia fuerte de lockout/rate limiting interno suficiente para Internet hostil
- PostgreSQL embebido es cómodo para local, pero no es la opción más robusta para exposición pública seria

## Próximos pasos de trabajo

1. documentar despliegue recomendado
2. preparar config limpia y portable
3. preparar nginx reverse proxy
4. preparar rate limiting
5. preparar checklist de exposición pública
6. evaluar migración a base de datos gestionada si escala el uso
