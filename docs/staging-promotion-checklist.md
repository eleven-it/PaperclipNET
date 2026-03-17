# Staging Promotion Checklist

## Objetivo

Checklist para decidir si un cambio puede promoverse desde `Desarrollo` hacia `Staging`.

## Requisitos de promoción

### Documentación
- [ ] existe spec aplicable
- [ ] existe test plan aplicable
- [ ] criterios de aceptación revisados
- [ ] riesgos documentados

### Configuración
- [ ] configuración ejemplo actualizada
- [ ] secretos fuera del repo
- [ ] cambios documentados

### Validación
- [ ] pruebas definidas ejecutadas o revisadas
- [ ] no se detectó exposición indebida de `3100`
- [ ] proxy y ruta esperada validados cuando aplique
- [ ] checklist de validación completada

### Operación
- [ ] existe plan de rollback
- [ ] existe evidencia mínima del estado previo
- [ ] el cambio es entendible y trazable

## Regla

Si cualquiera de los puntos críticos falla, el cambio no debería promocionarse a `Staging`.
