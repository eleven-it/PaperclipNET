# Rollback Runbook

## Objetivo

Definir cómo revertir cambios de despliegue/configuración cuando una iteración no cumpla criterios de aceptación o genere regresiones.

## Cuándo aplicar rollback

- el proxy no enruta correctamente
- el servicio deja de responder
- `3100` queda expuesto de forma indebida
- la autenticación o redirecciones fallan gravemente
- el cambio incumple tests críticos de la fase

## Principios

1. priorizar restaurar disponibilidad controlada
2. volver al último estado conocido válido
3. no improvisar cambios adicionales durante el rollback
4. dejar evidencia de causa y resultado

## Pasos de alto nivel

1. identificar el cambio introducido
2. contrastar contra la spec y el test plan
3. restaurar configuración previa conocida
4. reiniciar o recargar solo los servicios necesarios
5. verificar healthcheck
6. verificar listeners
7. verificar acceso por proxy
8. registrar incidente y hallazgos

## Evidencias de rollback

- qué se revirtió
- por qué se revirtió
- hora de inicio y fin
- estado final del servicio
- próximos pasos correctivos

## Resultado esperado

El sistema vuelve a un estado conocido, documentado y verificable, aunque no sea el estado final deseado.
