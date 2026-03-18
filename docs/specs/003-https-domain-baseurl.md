# Spec 003 — HTTPS, dominio y base URL definitiva

## Estado

Done

## Objetivo

Definir cómo PaperclipNET operará con una URL estable y TLS válido, alineando proxy, redirecciones y configuración de autenticación.

## Problema

La instancia actual carece de `publicBaseUrl` definitiva y no debe considerarse lista para exposición pública sin HTTPS y origen explícito.

## Alcance

- dominio o subdominio de servicio
- `publicBaseUrl` explícita
- estrategia HTTP→HTTPS
- coherencia entre nginx y Paperclip
- criterios de certificado y terminación TLS

## Restricciones

1. no se publicará como despliegue final sin dominio o subdominio definido
2. `auth.baseUrlMode` deberá quedar en `explicit`
3. `auth.publicBaseUrl` deberá coincidir con la URL servida por nginx
4. exposición pública final requerirá HTTPS

## Criterios de aceptación

- existe una URL pública o patrón definido
- Paperclip usa `baseUrlMode=explicit`
- existe estrategia documentada de HTTPS
- existe test plan asociado
- existe evidencia de coherencia entre proxy y base URL al implementar

## Cierre de spec

La spec se considera cerrada porque:

- el dominio final quedó definido como `https://busone.estrategiasdenegocios.ar`
- `auth.baseUrlMode` quedó en `explicit`
- `auth.publicBaseUrl` quedó alineada al dominio final
- el backend Paperclip quedó operativo en `0.0.0.0:3002` para la topología NAT real
- la publicación por dominio responde correctamente
- el acceso administrativo fue recuperado mediante bootstrap invite y validado por ingreso exitoso


## Implementación observada

- Dominio final definido: `https://busone.estrategiasdenegocios.ar`
- `auth.baseUrlMode` quedó en `explicit`
- `auth.publicBaseUrl` quedó en `https://busone.estrategiasdenegocios.ar`
- La terminación TLS parece ocurrir aguas arriba o en una capa no reflejada por el listener local `:443`
- El runtime local de Paperclip quedó recuperado en `127.0.0.1:3002`
- Queda pendiente corregir el proxy público final que hoy devuelve `502 Bad Gateway`
