# Evidence — Dominio final definido para PaperclipNET

## Fecha

2026-03-18

## Fase / Spec

- Spec 003 — HTTPS, dominio y base URL definitiva

## Cambio evaluado

Se definió como dominio final de servicio:

- `https://busone.estrategiasdenegocios.ar`

## Resultado esperado

- `auth.baseUrlMode` debe quedar en `explicit`
- `auth.publicBaseUrl` debe quedar en `https://busone.estrategiasdenegocios.ar`
- la validación posterior debe comprobar coherencia entre despliegue real, proxy y dominio final

## Observaciones

La terminación TLS parece existir aguas arriba o en otra capa ya operativa, dado que el dominio responde por HTTPS aunque el host local no expone `:443` directamente.
