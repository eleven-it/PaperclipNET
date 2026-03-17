# Proceso de desarrollo obligatorio

## Norma de trabajo

A partir de este punto, el proyecto se trabajará obligatoriamente bajo:

- **SDD** — Spec-Driven Development
- **TDD** — Test-Driven Development

## Regla principal

**No se genera código de implementación hasta que exista una especificación suficiente y una estrategia de pruebas definida.**

## Flujo obligatorio

1. Definir la necesidad o cambio
2. Redactar especificación funcional/técnica
3. Acordar criterios de aceptación
4. Diseñar estrategia de pruebas
5. Escribir pruebas primero cuando aplique
6. Implementar el mínimo código necesario para satisfacer la especificación y las pruebas
7. Refactorizar sin romper contratos
8. Documentar decisiones y riesgos

## Requisitos mínimos antes de codificar

Antes de cualquier implementación debe existir:

- objetivo claro
- alcance
- restricciones
- criterios de aceptación
- casos de prueba esperados
- riesgos o supuestos relevantes

## Política del repositorio

- `1.0` → línea base
- `Desarrollo` → trabajo activo
- `Staging` → validación previa

## Aplicación práctica en PaperclipNET

Para cada cambio importante se deberá crear primero:

- una spec en `docs/specs/`
- una estrategia de test en `docs/tests/`

Y solo después avanzar a implementación.
