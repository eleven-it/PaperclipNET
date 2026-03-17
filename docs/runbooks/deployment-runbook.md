# Deployment Runbook

## Objetivo

Describir el procedimiento esperado para desplegar una versión controlada de PaperclipNET siguiendo las specs vigentes.

## Precondiciones

- specs y test plans aplicables revisados
- rama de trabajo identificada
- configuración ejemplo disponible
- secretos fuera del repositorio
- estrategia de rollback definida

## Pasos de alto nivel

1. revisar spec aplicable
2. revisar test plan aplicable
3. validar que la configuración ejemplo sigue alineada con la spec
4. preparar valores locales de entorno/secrets
5. validar bind interno de Paperclip
6. validar configuración de nginx
7. verificar puertos expuestos
8. ejecutar pruebas de reachability mínimas
9. documentar evidencias
10. decidir promoción o rollback

## Checks mínimos previos

- `3100` no debe publicarse al exterior
- nginx debe ser el punto de entrada
- `publicBaseUrl` debe ser coherente con el entorno si hay exposición pública
- runtime y secrets no deben tocar el repositorio

## Evidencias a guardar

- salida de listeners
- resultado de healthcheck
- resultado de acceso vía proxy
- validación de redirect HTTPS si aplica
- fecha y responsable del despliegue

## Criterio de éxito

El despliegue es válido si cumple la spec de la fase y no rompe invariantes globales de seguridad.
