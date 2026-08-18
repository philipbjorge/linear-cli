# This is a fork

Upstream is [nesszer/linear-cli](https://github.com/nesszer/linear-cli), MIT licensed.

It exists because upstream's release pipeline has been failing since v0.3.7, so
fixes that are already merged upstream never reach an installable macOS or Linux
binary. We carry a small delta and cut our own releases.

## Delta against upstream master

| change | upstream status |
| --- | --- |
| `initiatives list`: `progress` → `health` (Linear removed the field) | proposed in nesszer/linear-cli#46 |
| `issues get --history`: drop `slaBreachesAt`/`slaStartedAt` from the history fragment | proposed in nesszer/linear-cli#46 |
| release workflow: `fail-fast: false`, resilient upload, explicit tag input, GitHub-hosted runners | proposed in nesszer/linear-cli#47 |
| `issues create --project` cherry-picked from the orphaned v0.3.27 tag | tagged upstream but never merged to master |
| crates.io publish job removed | fork-only, and must stay fork-only — we do not own the crate |

Keep this delta small. When upstream merges #46 and #47, rebase and drop what
landed. If upstream ever ships working release assets again, retire this fork and
point `mise.toml` back at `github:nesszer/linear-cli`.

## Cutting a release

```
git tag vX.Y.Z && git push origin vX.Y.Z
gh workflow run release.yml --repo philipbjorge/linear-cli -f tag=vX.Y.Z
```

Then confirm the run attached `linear-cli-aarch64-apple-darwin.tar.gz`, which is
the asset `mise` needs, and bump the pin in 87group-hq's `mise.toml`.
