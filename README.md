# Chorus Core

The collaboration core shared by three products, so that a fix lands once instead of three times.

| Package | What it owns |
| --- | --- |
| `@mohammadtmohsen/shared` | Ids, redaction, the types every other package imports |
| `@mohammadtmohsen/agent-protocol` | The normalized `AgentEvent` union both providers project onto |
| `@mohammadtmohsen/adapter-claude` | Claude SDK to `AgentEvent`, with the mapping kept pure |
| `@mohammadtmohsen/adapter-codex` | codex app-server JSON-RPC to `AgentEvent` |
| `@mohammadtmohsen/orchestrator` | Conversation service, policy engine, catch-up, supervisor |
| `@mohammadtmohsen/event-store` | SQLite, migrations, projections, the projects registry |
| `@mohammadtmohsen/workspace` | Path helpers and `parseDiff` |
| `@mohammadtmohsen/ide-protocol` | The editor bridge contract |

## Consuming it

Add the scope to `.npmrc`, with the token read from the environment so no credential is ever
written to a file:

```
@mohammadtmohsen:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

Then depend on a version as usual:

```json
{ "dependencies": { "@mohammadtmohsen/event-store": "^1.0.0" } }
```

## Releasing

Tag `v*` and push. `.github/workflows/release.yml` builds every package, runs every package's
tests, and publishes in dependency order. A tag whose tests fail publishes nothing.

Packages are `restricted`: readable in this repository, installable only with a token that has
`read:packages`.

## Not here

The products. Chorus, Chorus Workbench and the Chorus VS Code extension each own their own
application code and their own release. This repository owns the eight packages above and nothing
else — no desktop shell, no editor surface, no engine.

## Where it came from

`chorus-extension/docs/core-provenance.md` records the revision these packages were seeded from,
file by file, with blob ids and sha256.
