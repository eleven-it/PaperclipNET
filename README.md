# PaperclipNET

Base de trabajo para despliegue, configuración y endurecimiento de una instancia Paperclip.

## Alcance actual

Este repositorio documenta y prepara:

- la instalación actual saneada de Paperclip
- una plantilla de configuración portable
- documentación de estado actual
- plan inicial de endurecimiento y despliegue

## Importante

Este repo **no** almacena secretos ni estado runtime.

No se suben:
- bases de datos
- backups
- claves
- `.env`
- logs
- secretos de autenticación

## Estructura

- `config/` → plantillas de configuración
- `docs/` → estado actual, endurecimiento y despliegue
- `runtime/` → excluido del repo; reservado para estado local

## Estado actual conocido

- Paperclip operativo
- modo `authenticated/private`
- bind LAN realizado para pruebas
- pendiente endurecimiento para exposición segura

## Siguiente fase

- devolver bind a loopback para publicación segura
- meter nginx delante
- fijar `publicBaseUrl`
- aplicar rate limiting
- definir estrategia de acceso: privado / público
