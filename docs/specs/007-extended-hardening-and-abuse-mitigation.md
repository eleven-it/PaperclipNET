# Spec 007 — Hardening extendido y mitigación de abuso

## Estado

Done

## Objetivo

Definir una fase de seguridad posterior al despliegue base para reducir riesgo frente a abuso automatizado, fuerza bruta y exposición no controlada.

## Alcance

- rate limiting ampliado
- integración futura con fail2ban
- criterios de exposición pública controlada
- lineamientos de defensa perimetral

## Criterios de aceptación

- existe estrategia ampliada de mitigación
- existe test plan asociado
- quedan separadas las medidas básicas de las avanzadas

## Cierre de spec

La spec se considera cerrada porque:

- existe hardening básico ya aplicado en nginx (`limit_req`, cabeceras mínimas)
- existe documentación de mitigación ampliada y criterios para fases posteriores
- quedó explícita la separación entre controles básicos ya implementados y defensas avanzadas futuras (por ejemplo fail2ban/CDN/WAF)
