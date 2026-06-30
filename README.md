# pattern-catalog

Part of **[Anchor Migration](https://github.com/anchor-migration/migration-hub)** — documented migration patterns with linked OpenRewrite recipes and parity verification checklists.

**Status:** Alpha — first patterns for Duke's Bank CMP→JPA.

## Layout

```text
patterns/
  cmp-scalar-entity-to-jpa-account-bean.yaml
  cmp-many-to-many-to-jpa-account-bean.yaml
```

Each pattern YAML includes:

| Section | Purpose |
|---------|---------|
| `id` | Stable pattern ID referenced by `parity-verify` matrix `pattern_id` |
| `linked_recipes` | OpenRewrite recipe class names in `rewrite-recipes` |
| `detection` | AST / schema signals (documentation; detection tooling planned) |
| `verification.checks` | Checklist consumed by `parity-verify` RuleEngine |

## Usage with parity-verify

```bash
parity-verify compare \
  --before-db before.db --after-db after.db \
  --matrix-file examples/matrices/dukesbank-cmp-jpa.yaml \
  --pattern-catalog /path/to/pattern-catalog \
  --linked-after linked-after.db \
  -o report.json
```

Matrix YAML references a pattern:

```yaml
id: dukesbank-cmp-jpa
pattern_id: cmp-scalar-entity-to-jpa-account-bean
checks: []   # optional overrides merged by check id
```

Bundled patterns also ship inside `parity-verify` JAR under `src/main/resources/patterns/` for `--matrix dukesbank-cmp-jpa` without an external catalog path.

## License

MIT
