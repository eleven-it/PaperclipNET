# Traceability Matrix

## Objetivo

Mantener trazabilidad entre alcance, specs, test plans y entregables del proyecto.

## Matriz

| ID | Tema | Spec | Test Plan | Entregables esperados | Estado |
|---|---|---|---|---|---|
| 000 | Alcance global | `docs/specs/000-product-scope.md` | `docs/tests/000-master-test-strategy.md` | marco global del proyecto | Draft |
| 001 | Despliegue seguro base | `docs/specs/001-secure-deployment.md` | `docs/tests/001-secure-deployment-test-plan.md` | arquitectura base, criterios iniciales | Draft |
| 002 | Nginx endurecido | `docs/specs/002-nginx-reverse-proxy-hardening.md` | `docs/tests/002-nginx-reverse-proxy-hardening-test-plan.md` | config nginx de referencia, guía proxy | Draft |
| 003 | HTTPS / dominio / base URL | `docs/specs/003-https-domain-baseurl.md` | `docs/tests/003-https-domain-baseurl-test-plan.md` | estrategia TLS y URL estable | Draft |
| 004 | Configuración y secretos | `docs/specs/004-config-and-secrets-management.md` | `docs/tests/004-config-and-secrets-management-test-plan.md` | convención de config y secretos | Draft |
| 005 | Observabilidad y operación | `docs/specs/005-observability-and-operations.md` | `docs/tests/005-observability-and-operations-test-plan.md` | logs, healthchecks, checklist operativa | Draft |
| 006 | Ramas y promoción | `docs/specs/006-branching-staging-promotion.md` | `docs/tests/006-branching-staging-promotion-test-plan.md` | estrategia de ramas, staging y promoción | Draft |
| 007 | Hardening extendido | `docs/specs/007-extended-hardening-and-abuse-mitigation.md` | `docs/tests/007-extended-hardening-and-abuse-mitigation-test-plan.md` | mitigación ampliada de abuso | Draft |

## Regla de uso

Ningún entregable importante debería aparecer sin estar vinculado a:

- una spec
- un test plan
- criterios de aceptación

## Próximo uso esperado

Esta matriz debe actualizarse cuando un artefacto pase de `Draft` a una fase más madura y cuando aparezcan entregables implementados reales.
