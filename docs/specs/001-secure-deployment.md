# Spec 001 — Despliegue seguro y endurecimiento inicial de PaperclipNET

## Estado

Draft

## Objetivo

Definir la arquitectura, restricciones y criterios de aceptación para desplegar PaperclipNET de forma segura, evitando exposición directa insegura del servicio y preparando una base mantenible para futuras iteraciones.

## Contexto

La instalación actual de Paperclip funciona, pero presenta varias limitaciones para exposición a Internet:

- Paperclip no debe exponerse directamente en `:3100`
- la autenticación existe, pero no se considera suficiente por sí sola para Internet hostil
- no hay evidencia clara de protección interna robusta frente a brute force o DDoS
- falta configuración explícita de `publicBaseUrl`
- la instancia actual fue adaptada para escucha LAN, lo cual sirve para pruebas pero no como estado final recomendado

## Problema

Se necesita transformar una instalación funcional pero de laboratorio en una base de despliegue segura y repetible, separando claramente:

- aplicación
- proxy reverso
- configuración
- secretos
- criterios de validación

## Alcance

Incluye:

- definición de topología de despliegue recomendada
- configuración objetivo de PaperclipNET
- uso de nginx como reverse proxy
- obligatoriedad de HTTPS para exposición pública
- requisitos mínimos de endurecimiento
- estrategia de configuración portable
- checklist de aceptación técnica

No incluye todavía:

- implementación completa de automatización
- migración a base de datos externa
- integración con proveedor LLM
- alta disponibilidad
- protección DDoS avanzada a nivel proveedor/CDN

## Arquitectura objetivo

### Modo recomendado

- Paperclip escuchando solo en `127.0.0.1:3100`
- Nginx expuesto en `80/443`
- TLS terminado en nginx
- autenticación de Paperclip en modo `authenticated`
- `publicBaseUrl` explícita
- secretos fuera del repositorio

### Flujo de red

1. Cliente accede por HTTPS
2. nginx recibe la conexión
3. nginx aplica controles perimetrales
4. nginx reenvía a `127.0.0.1:3100`
5. Paperclip responde sin exposición directa del puerto interno

## Restricciones

1. No se expondrá directamente `3100` a Internet
2. No se subirán secretos al repositorio
3. No se implementará código antes de aprobar spec y plan de test
4. La configuración deberá poder reproducirse sin depender de rutas absolutas sensibles
5. Toda exposición pública requerirá `publicBaseUrl` explícita y HTTPS

## Requisitos funcionales

### RF-001
La aplicación deberá poder ejecutarse en modo autenticado con configuración portable basada en archivos de ejemplo.

### RF-002
El despliegue objetivo deberá usar nginx como único punto de entrada público.

### RF-003
La configuración deberá separar claramente runtime, secretos y documentación.

### RF-004
Debe existir documentación suficiente para reconstruir el despliegue desde cero.

### RF-005
Deben definirse rutas y controles mínimos para reducir riesgo de abuso y fuerza bruta.

## Requisitos no funcionales

### RNF-001 — Seguridad
No exponer Paperclip directamente al exterior.

### RNF-002 — Reproducibilidad
La configuración base debe poder replicarse en otro host similar con cambios mínimos.

### RNF-003 — Mantenibilidad
La documentación y estructura del repo deben dejar claro qué es plantilla y qué es estado runtime.

### RNF-004 — Observabilidad mínima
Debe contemplarse logging suficiente para troubleshooting y futura integración con herramientas defensivas.

## Decisiones iniciales

1. La rama de trabajo activo será `Desarrollo`
2. La rama `Staging` se usará para validación previa
3. La rama `1.0` mantiene la línea base documental
4. Se trabajará con SDD + TDD obligatoriamente

## Riesgos

- exponer Paperclip sin proxy endurecido
- confiar en autenticación interna sin controles perimetrales
- mezclar secretos con configuración versionada
- dejar la configuración ligada a la IP LAN en lugar de loopback
- considerar la instalación actual como producción cuando aún es de laboratorio

## Supuestos

- nginx ya está disponible en el host
- el despliegue inicial se hará sobre la máquina actual
- GitHub seguirá siendo el repositorio fuente del proyecto
- el usuario decidirá posteriormente si el acceso será privado, público o híbrido

## Entregables esperados

1. plantilla de configuración segura
2. documentación de despliegue
3. documentación de reverse proxy
4. plan de endurecimiento mínimo
5. checklist de validación
6. tests/documentación de verificación

## Criterios de aceptación

### CA-001
Existe una configuración ejemplo con bind en loopback y `publicBaseUrl` explícita.

### CA-002
Existe una guía de despliegue con nginx como reverse proxy.

### CA-003
El repositorio distingue claramente entre archivos versionables y secretos/runtime.

### CA-004
Existe un plan de validación para comprobar que `3100` no queda publicado externamente.

### CA-005
Existe un plan de validación para HTTPS, healthcheck y encaminamiento por proxy.

### CA-006
Las tareas futuras quedan organizadas en iteraciones posteriores, sin mezclar implementación prematura.

## Fuera de alcance por ahora

- MFA si la plataforma no la soporta de forma madura
- protección DDoS enterprise
- clúster multiinstancia
- SSO corporativo
- automatización CI/CD completa

## Próxima iteración propuesta

Spec 002 debería cubrir:

- reverse proxy nginx endurecido
- rate limiting inicial
- cabeceras seguras
- estrategia de logs para fail2ban
