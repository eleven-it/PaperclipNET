# Test Plan 002 — Nginx reverse proxy endurecido

## Estado

Draft

## Relación

Este plan valida la `Spec 002 — Nginx reverse proxy endurecido para PaperclipNET`.

## Objetivo del plan

Definir cómo verificar que nginx protege correctamente a PaperclipNET y que la aplicación deja de ser el punto directamente expuesto.

## Enfoque TDD

Antes de aplicar una configuración final, deberán existir comprobaciones que permitan detectar:

- binds inseguros
- upstream incorrecto
- ausencia de proxy
- ausencia de rate limiting inicial
- configuración inconsistente para HTTP/HTTPS

## Tipos de prueba

### 1. Validación de configuración
Revisión estática de archivos de nginx y de la config objetivo de Paperclip.

### 2. Validación de puertos
Comprobación de qué servicio escucha en qué puerto.

### 3. Validación de proxy
Comprobación de que nginx sirve como punto de entrada hacia Paperclip.

### 4. Validación negativa
Comprobación de que el puerto 3100 no sea accesible externamente.

## Casos de prueba

### TP-002-001 — Existe configuración nginx de referencia
**Dado** el repositorio
**Cuando** se revisa la documentación/config de proxy
**Entonces** debe existir una configuración nginx de referencia para PaperclipNET.

### TP-002-002 — Upstream en loopback
**Dado** la configuración nginx de referencia
**Cuando** se revisa el upstream
**Entonces** debe apuntar a `127.0.0.1:3100`.

### TP-002-003 — Paperclip en loopback
**Dado** la configuración objetivo de Paperclip
**Cuando** se revisa el `host`
**Entonces** debe ser `127.0.0.1`.

### TP-002-004 — Proxy headers presentes
**Dado** la configuración nginx
**Cuando** se revisan directivas proxy
**Entonces** deben existir cabeceras `Host`, `X-Forwarded-For` y `X-Forwarded-Proto`.

### TP-002-005 — HTTP/1.1 y upgrade
**Dado** la configuración nginx
**Cuando** se revisan directivas de proxy
**Entonces** debe contemplarse `proxy_http_version 1.1` y soporte de upgrade.

### TP-002-006 — Rate limiting inicial presente
**Dado** la configuración nginx
**Cuando** se revisa el archivo de referencia
**Entonces** debe existir al menos una política inicial de limitación de tasa.

### TP-002-007 — Puerto 80/443 en nginx
**Dado** la configuración implementada
**Cuando** se inspeccionan puertos
**Entonces** nginx debe escuchar en `80` y/o `443`.

### TP-002-008 — Puerto 3100 no público
**Dado** la configuración implementada
**Cuando** se inspecciona la exposición del host
**Entonces** `3100` no debe quedar expuesto externamente.

### TP-002-009 — Respuesta por proxy
**Dado** nginx configurado
**Cuando** se solicita la URL de entrada
**Entonces** debe recibirse respuesta de Paperclip a través del proxy.

### TP-002-010 — Healthcheck encaminado
**Dado** nginx configurado
**Cuando** se consulta el healthcheck por la ruta definida
**Entonces** la respuesta debe ser válida sin uso directo del puerto interno público.

## Pruebas negativas

### TN-002-001
No es válido un despliegue donde nginx exista pero Paperclip siga publicado en `0.0.0.0:3100` o IP LAN expuesta a Internet.

### TN-002-002
No es válida una configuración de proxy sin cabeceras forward básicas.

### TN-002-003
No es válida una configuración pública sin una estrategia definida para HTTPS.

### TN-002-004
No es válida una configuración endurecida que no contemple ni siquiera limitación básica de tasa.

## Evidencia esperada

- archivos de configuración nginx
- resultado de `ss -tulpn`
- pruebas `curl` a proxy
- comprobaciones de reachability al `3100`
- revisión documental de cabeceras y límites

## Definición de terminado para esta iteración

La iteración se considerará completa cuando:

1. exista configuración nginx de referencia
2. exista documentación operativa mínima
3. el bind interno quede definido
4. exista un plan claro para validar que el proxy es el único punto de entrada

## Próxima fase sugerida

La siguiente fase debería cubrir:

- HTTPS real
- certificados
- redirect HTTP→HTTPS
- headers de seguridad ampliadas
- política de exposición pública por dominio
