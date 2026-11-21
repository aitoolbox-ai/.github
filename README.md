# aitoolbox-ai/.github

Repositorio **público** de la organización `aitoolbox-ai` con:

- **Workflows de CI reutilizables** (`.github/workflows/*.yml`, todos `on: workflow_call`).
- **Plantillas de issues y PRs** por defecto para todos los repos de la organización
  (`.github/ISSUE_TEMPLATE/`, `.github/pull_request_template.md`).
- **Perfil de la organización** (`profile/README.md`).

> Es público porque GitHub solo aplica las plantillas de toda la organización desde un repo
> `.github` público. **No contiene secretos ni código de producto.**

## Workflows reutilizables

| Workflow | Para qué | Inputs principales |
|---|---|---|
| `go.yml` | gofmt + go vet + test + build de un módulo Go | `working-directory`, `go-version-file` |
| `node.yml` | `npm ci` + lint + test + build (Node, Vite, Astro) | `working-directory`, `node-version`, `run-lint`, `run-test`, `run-build` |
| `gradle-kmp.yml` | Tareas Gradle de un proyecto Kotlin Multiplatform | `working-directory`, `tasks`, `java-version`, `github-packages` (expone el token como `NODE_AUTH_TOKEN` solo al paso de Gradle) |
| `plans.yml` | Valida `plans.yaml` contra su JSON Schema (ajv) | `plans-file`, `schema-file` |

### Uso

```yaml
# .github/workflows/ci.yml en cualquier repo de la organización
name: ci
on:
  push: { branches: [main] }
  pull_request:
permissions:
  contents: read
  packages: read   # node.yml y gradle-kmp.yml lo piden (GitHub Packages); sin él, el job no arranca
jobs:
  backend:
    uses: aitoolbox-ai/.github/.github/workflows/go.yml@main
    with:
      working-directory: backend
  web:
    uses: aitoolbox-ai/.github/.github/workflows/node.yml@main
    with:
      working-directory: frontend/app
  plans:
    uses: aitoolbox-ai/.github/.github/workflows/plans.yml@main
    with:
      plans-file: contracts/plans.yaml
      schema-file: contracts/plans.schema.json
```

## Labels comunes

`area:backend`, `area:frontend`, `area:marketing`, `area:mobile`, `area:security`,
`area:contracts`, `area:infra`, `type:feature`, `type:bug`, `type:chore`.
