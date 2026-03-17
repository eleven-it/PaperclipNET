# Master Test Strategy — PaperclipNET

## Estado

Draft

## Objetivo

Definir la estrategia global de validación del proyecto PaperclipNET bajo enfoque TDD.

## Capas de validación

### 1. Validación de documentación
Comprueba que cada fase tenga spec, test plan, criterios de aceptación y trazabilidad.

### 2. Validación de configuración
Comprueba consistencia entre archivos de ejemplo, rutas, binds y políticas.

### 3. Validación de host/red
Comprueba puertos, listeners, proxy, reachability y no exposición del puerto interno.

### 4. Validación funcional mínima
Comprueba que el servicio responda por la ruta prevista y en la topología prevista.

### 5. Validación de seguridad básica
Comprueba que no se rompan invariantes de seguridad esenciales.

## Invariantes que nunca deben romperse

1. no subir secretos al repositorio
2. no exponer directamente el puerto de app a Internet
3. no implementar cambios relevantes sin spec/test plan
4. no mezclar runtime con config versionada

## Tipos de evidencia aceptados

- archivos versionados
- salida de comandos de red
- respuestas HTTP/HTTPS
- revisión estructural del repo
- checklist operativa firmada/completada

## Criterio de avance entre fases

Una fase solo se considera lista cuando:

- sus criterios de aceptación están cubiertos
- su test plan está completo
- los riesgos conocidos se documentaron
- la siguiente fase tiene base suficiente para iniciar
