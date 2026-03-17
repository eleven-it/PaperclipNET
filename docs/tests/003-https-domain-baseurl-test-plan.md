# Test Plan 003 — HTTPS, dominio y base URL

## Estado

Draft

## Casos mínimos

- validar existencia de `publicBaseUrl`
- validar coherencia entre dominio y proxy
- validar política HTTP→HTTPS
- validar que callbacks/redirecciones no dependan de autodetección ambigua

## Negativas

- no aceptar despliegue público sin `publicBaseUrl`
- no aceptar despliegue público solo por IP sin estrategia explícita
