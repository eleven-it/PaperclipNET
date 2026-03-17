# Staging Runbook

## Objetivo

Definir cómo usar la rama/entorno `Staging` como paso intermedio de validación antes de consolidar cambios.

## Precondiciones

- cambios existentes en `Desarrollo`
- specs y test plans asociados disponibles
- checklist de promoción revisada

## Uso esperado

1. seleccionar el cambio o conjunto de cambios
2. verificar trazabilidad con spec/test plan
3. promover a `Staging`
4. validar comportamiento esperado
5. decidir promoción posterior o rollback

## Qué validar en staging

- coherencia documental
- configuración prevista
- topología de red esperada
- comportamiento del proxy cuando aplique
- no ruptura de invariantes de seguridad

## Resultado esperado

`Staging` debe funcionar como zona de validación controlada, no como simple copia sin criterio.
