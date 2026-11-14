# .github (aitoolbox-ai) — CLAUDE.md

## Alcance
Solo workflows de CI **reutilizables** (`on: workflow_call`), plantillas de issues/PR y el perfil
de la organización. Nada de código de producto. **Repo público: nunca secretos, nombres de
clientes ni URLs internas.**

## Reglas
- Cada workflow declara `permissions` mínimas (`contents: read` por defecto).
- Cambios en inputs = cambio de contrato: añadir inputs con valor por defecto, no renombrar ni
  borrar sin actualizar antes todos los repos que lo llaman.
- Versiones de acciones fijadas a major (`actions/checkout@v7`, etc.).

## Comandos
- Lint de workflows: `npx -y @action-validator/cli .github/workflows/*.yml` (opcional) o
  `actionlint` si está instalado.
- No hay build ni tests: la validación real es que el CI de los repos consumidores pase.
