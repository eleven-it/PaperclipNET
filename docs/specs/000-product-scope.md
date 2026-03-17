# Spec 000 — Alcance global del producto PaperclipNET

## Estado

Draft

## Visión

PaperclipNET será una base de despliegue, configuración, endurecimiento y operación segura para una instancia Paperclip mantenible, reproducible y preparada para evolucionar desde laboratorio a servicio controlado.

## Objetivo global

Transformar la instalación actual en un proyecto con:

- arquitectura documentada
- configuración portable
- endurecimiento progresivo
- validación por etapas
- disciplina obligatoria SDD + TDD
- separación clara entre código, configuración, runtime y secretos

## Resultado esperado

Al finalizar las iteraciones principales, el proyecto deberá permitir:

1. desplegar Paperclip de forma repetible
2. ejecutarlo detrás de nginx
3. evitar exposición directa del puerto interno
4. soportar HTTPS con base URL explícita
5. operar con configuración documentada
6. validar la topología mediante pruebas definidas previamente
7. preparar futuras mejoras de seguridad y operación

## Objetivos principales por dominio

### A. Arquitectura y despliegue
- topología clara
- separación app/proxy/runtime
- rutas y convenciones reproducibles

### B. Seguridad
- no exponer el puerto interno
- hardening mínimo de proxy
- estrategia base frente a abuso y fuerza bruta
- tratamiento estricto de secretos

### C. Operación
- logs comprensibles
- healthchecks
- checklist de validación
- base para staging y promoción

### D. Desarrollo
- uso obligatorio de SDD
- uso obligatorio de TDD
- trabajo por specs trazables
- cambios versionados por ramas

## Fuera de alcance inicial

- multi-tenant avanzado
- HA/cluster
- SSO empresarial
- DDoS enterprise
- observabilidad enterprise completa
- automatización CI/CD completa desde el día uno

## Principios del proyecto

1. Seguridad antes que comodidad
2. Documentación antes que improvisación
3. Tests antes que implementación relevante
4. Configuración portable antes que dependencias frágiles del host
5. Secretos fuera del repositorio siempre

## Fases previstas

### Fase 0 — Fundación
- alcance global
- proceso de desarrollo
- roadmap de specs/tests

### Fase 1 — Despliegue seguro base
- arquitectura
- proxy nginx
- bind interno
- validación de puertos

### Fase 2 — Exposición segura
- HTTPS
- dominio/baseUrl
- hardening adicional del proxy

### Fase 3 — Operación
- scripts/checklists
- staging
- validación operativa

### Fase 4 — Endurecimiento extendido
- defensa adicional
- logging para respuesta a incidentes
- estrategia de promoción controlada

## Criterios globales de aceptación

### CGA-001
Existe un set coherente de specs y test plans que cubren el objetivo del proyecto.

### CGA-002
Existe una línea de despliegue seguro documentada de extremo a extremo.

### CGA-003
El proyecto distingue claramente entre artefactos versionables y secretos/runtime.

### CGA-004
Cada fase puede validarse mediante pruebas previamente definidas.

### CGA-005
No se introduce implementación relevante sin trazabilidad hacia una spec y un test plan.
