# Spec 003 — HTTPS, dominio y base URL definitiva

## Estado

Draft

## Objetivo

Definir cómo PaperclipNET operará con una URL estable y TLS válido, alineando proxy, redirecciones y configuración de autenticación.

## Problema

La instancia actual carece de `publicBaseUrl` definitiva y no debe considerarse lista para exposición pública sin HTTPS y origen explícito.

## Alcance

- dominio o subdominio de servicio
- `publicBaseUrl` explícita
- estrategia HTTP→HTTPS
- coherencia entre nginx y Paperclip

## Criterios de aceptación

- existe una URL pública o patrón definido
- Paperclip usa `baseUrlMode=explicit`
- existe estrategia documentada de HTTPS
- existe test plan asociado
