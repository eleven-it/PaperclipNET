# Spec 002 — Nginx reverse proxy endurecido para PaperclipNET

## Estado

Draft

## Objetivo

Definir la configuración objetivo de nginx como reverse proxy endurecido para PaperclipNET, de modo que nginx sea la única superficie expuesta y Paperclip permanezca aislado detrás del proxy.

## Relación con specs previas

Esta spec implementa la siguiente fase de la `Spec 001 — Despliegue seguro y endurecimiento inicial de PaperclipNET`.

## Problema

La instancia actual de Paperclip fue llevada a escucha LAN para pruebas. Ese estado no es válido como despliegue seguro final. Se necesita una capa perimetral que:

- oculte el puerto interno
- permita HTTPS
- aplique controles básicos de abuso
- prepare registro y observabilidad

## Alcance

Incluye:

- topología nginx → Paperclip
- bind interno de Paperclip
- proxy de `80/443` hacia `127.0.0.1:3100`
- cabeceras proxy necesarias
- límites iniciales de tasa
- reglas mínimas de exposición
- separación de config versionable vs config local

No incluye todavía:

- certificados reales finales
- CDN/WAF externo
- automatización completa del provisioning
- fail2ban productivo completo
- balanceo o clustering

## Arquitectura objetivo

### Aplicación
- Paperclip escuchará en `127.0.0.1:3100`
- no se expondrá directamente en interfaces públicas

### Proxy
- nginx escuchará en `80/443`
- nginx será el único punto de entrada público
- nginx reenviará tráfico a `127.0.0.1:3100`

### Flujo
1. Cliente accede a nginx
2. nginx aplica políticas mínimas
3. nginx reenvía a Paperclip interno
4. Paperclip responde sin exposición directa del puerto 3100

## Restricciones

1. `3100` no debe quedar accesible desde el exterior
2. la configuración de nginx debe ser reproducible y documentada
3. debe existir al menos un nivel básico de rate limiting
4. deben definirse cabeceras proxy coherentes
5. el diseño debe permitir HTTPS obligatorio para exposición pública

## Requisitos funcionales

### RF-002-001
Debe existir una configuración nginx de referencia para PaperclipNET.

### RF-002-002
La configuración deberá enviar tráfico al upstream `127.0.0.1:3100`.

### RF-002-003
La configuración deberá contemplar soporte para WebSocket/upgrade si Paperclip lo necesitara.

### RF-002-004
La configuración deberá incluir redirección o preparación para HTTPS en despliegue público.

### RF-002-005
Debe contemplarse un endpoint o ruta verificable para health/proxy test.

## Requisitos no funcionales

### RNF-002-001 — Seguridad
La app no debe exponerse directamente al exterior.

### RNF-002-002 — Trazabilidad
Debe existir documentación de qué hace cada bloque principal del proxy.

### RNF-002-003 — Mantenibilidad
La configuración debe ser entendible y adaptable por entornos.

### RNF-002-004 — Defensa básica
Debe haber al menos controles básicos contra abuso automatizado.

## Controles mínimos esperados

1. `proxy_set_header Host`
2. `proxy_set_header X-Forwarded-For`
3. `proxy_set_header X-Forwarded-Proto`
4. `proxy_http_version 1.1`
5. soporte `Upgrade` / `Connection`
6. timeouts razonables
7. rate limit inicial en zonas sensibles o a nivel general
8. posibilidad de registrar eventos de acceso en logs de nginx

## Decisiones de diseño iniciales

1. mantener Paperclip en loopback
2. no usar NAT directo al puerto de app
3. exponer solo el proxy
4. dejar preparada la futura integración con HTTPS real
5. permitir evolución posterior hacia fail2ban y/o CDN

## Riesgos

- rate limiting demasiado agresivo puede romper uso legítimo
- cabeceras proxy mal configuradas pueden afectar auth/callbacks
- dejar HTTP abierto sin redirección a HTTPS en público
- asumir que nginx sustituye por completo controles de aplicación

## Supuestos

- nginx está disponible en el host
- el puerto 80 ya está bajo nginx
- se podrá adaptar la configuración por dominio cuando se defina

## Entregables esperados

1. archivo de ejemplo/configuración nginx de referencia
2. documentación operativa del proxy
3. checklist de validación de bind y puertos
4. directrices mínimas de rate limiting

## Criterios de aceptación

### CA-002-001
Existe una configuración nginx de referencia para PaperclipNET.

### CA-002-002
La configuración referencia `127.0.0.1:3100` como upstream.

### CA-002-003
Existe documentación de cabeceras y comportamiento esperado.

### CA-002-004
Existe al menos una política inicial de rate limiting documentada.

### CA-002-005
Existe una estrategia clara para validar que `3100` no queda expuesto públicamente.

### CA-002-006
La spec deja listo el camino para una iteración posterior de HTTPS y endurecimiento avanzado.

## Fuera de alcance por ahora

- certificados Let’s Encrypt reales
- gestión automática de renovación
- WAF avanzado
- fail2ban ajustado a producción
- protección DDoS de capa proveedor

## Próxima iteración propuesta

Spec 003 debería cubrir:

- HTTPS real
- dominio/baseUrl definitiva
- cabeceras seguras adicionales
- política de exposición pública controlada
