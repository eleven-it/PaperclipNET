# Test Plan 001 — Despliegue seguro y endurecimiento inicial

## Estado

Draft

## Relación

Este plan valida la `Spec 001 — Despliegue seguro y endurecimiento inicial de PaperclipNET`.

## Objetivo del plan

Definir cómo se verificará que la topología y configuración propuestas son seguras, reproducibles y coherentes antes de cualquier implementación amplia.

## Enfoque TDD

Antes de cambios de implementación relevantes, deberán definirse y ejecutarse comprobaciones que fallen si el despliegue incumple la spec.

## Tipos de prueba

### 1. Validación documental
Comprueba que la documentación requerida existe y es coherente.

### 2. Validación de configuración
Comprueba que los archivos de ejemplo reflejan el estado objetivo.

### 3. Validación de red
Comprueba que la aplicación no queda expuesta directamente.

### 4. Validación funcional mínima
Comprueba que el servicio puede responder a través del proxy esperado.

## Casos de prueba

### TP-001 — Existe spec aprobable
**Dado** el repositorio en rama `Desarrollo`
**Cuando** se revisa `docs/specs/001-secure-deployment.md`
**Entonces** deben existir objetivo, alcance, restricciones y criterios de aceptación.

### TP-002 — Existe test plan asociado
**Dado** el repositorio
**Cuando** se revisa `docs/tests/001-secure-deployment-test-plan.md`
**Entonces** debe existir trazabilidad con la spec 001.

### TP-003 — Config ejemplo segura
**Dado** `config/paperclip.config.example.json`
**Cuando** se inspecciona el archivo
**Entonces** el `host` debe ser `127.0.0.1`.

### TP-004 — Public base URL explícita
**Dado** `config/paperclip.config.example.json`
**Cuando** se inspecciona `auth`
**Entonces** debe existir `baseUrlMode = explicit` y un `publicBaseUrl` de ejemplo.

### TP-005 — Secretos fuera del repo
**Dado** el repositorio
**Cuando** se revisan archivos versionados y `.gitignore`
**Entonces** no deben estar incluidos `.env`, claves, backups ni runtime sensible.

### TP-006 — Separación runtime/config
**Dado** la estructura del repositorio
**Cuando** se inspeccionan las carpetas
**Entonces** debe distinguirse `config/`, `docs/` y `runtime/`.

### TP-007 — No exposición directa del 3100
**Dado** el despliegue objetivo implementado
**Cuando** se pruebe exposición externa
**Entonces** el puerto `3100` no debe ser accesible públicamente.

### TP-008 — Proxy operativo
**Dado** nginx configurado
**Cuando** se consulte la URL pública o interna definida
**Entonces** la respuesta debe llegar a Paperclip a través del proxy.

### TP-009 — Healthcheck alcanzable por ruta esperada
**Dado** el despliegue con proxy
**Cuando** se consulte el endpoint de health permitido
**Entonces** debe responder correctamente sin requerir acceso al puerto interno directo.

### TP-010 — HTTPS obligatorio en despliegue público
**Dado** un escenario de exposición pública
**Cuando** se intente acceso por HTTP plano
**Entonces** debe existir redirección o política definida a HTTPS.

## Pruebas negativas

### TN-001
No debe aceptarse como válido un despliegue que publique `192.168.x.x:3100` o `0.0.0.0:3100` directamente hacia Internet.

### TN-002
No debe aceptarse una configuración sin `publicBaseUrl` explícita cuando se pretenda exposición pública.

### TN-003
No debe aceptarse una propuesta que mezcle secretos reales dentro del repositorio.

## Evidencia esperada

- archivos versionados
- salidas de verificación de puertos
- comprobaciones HTTP/HTTPS
- revisión de `.gitignore`
- revisión de estructura documental

## Definición de terminado para esta iteración

La iteración podrá considerarse lista cuando:

1. la spec esté completa
2. el plan de test esté completo
3. exista configuración ejemplo coherente
4. exista documentación suficiente para implementar la siguiente iteración

## Próxima fase sugerida

Tras esta fase, la siguiente batería de pruebas deberá cubrir:

- nginx reverse proxy real
- rate limiting
- cabeceras de seguridad
- pruebas de exposición pública controlada
