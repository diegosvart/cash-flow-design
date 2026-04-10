# Contributing

## Flujo oficial

1. Crear branch desde `main` usando:
   - `plan/prj-2026-001/<tema-kebab>-v<N>`
2. Implementar cambios en commits pequeños y descriptivos.
3. Abrir PR a `main` usando el template obligatorio.
4. Obtener al menos 1 aprobacion antes de merge.
5. Verificar workflows en verde.

## Convenciones

- No hacer push directo a `main`.
- No reutilizar ramas cerradas.
- Mantener trazabilidad del plan en el cuerpo del PR.

## Commits

Se recomienda formato convencional:

- `feat(scope): ...`
- `fix(scope): ...`
- `docs(scope): ...`
- `chore(scope): ...`

## Calidad minima

- PR template completo
- CODEOWNERS aplicando reviewers
- Checks de CI en verde
