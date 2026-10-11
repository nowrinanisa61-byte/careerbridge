# Contributing

Use a focused branch, explain the problem and behavior change, and include relevant validation. Run `pnpm typecheck`, `pnpm test` and `pnpm build` before requesting review. Add a regression test when fixing a state, permissions or financial bug.

Use new migrations for schema changes; do not rewrite applied migrations. Do not commit secrets, local database files, provider logs, real CVs or user records. External-provider tests must be deliberate and isolated from production funds and recipients.

This export does not grant an open-source license. The maintainer must decide licensing and contribution terms before accepting third-party contributions.
