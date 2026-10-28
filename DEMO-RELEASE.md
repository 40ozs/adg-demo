# ADG demo release `genesee-press-2.1.0-1d585649e6cb`

This repository is a **one-way release mirror**. It is generated from a verified application
integration commit and the Genesee Press synthetic world; it is not a development repository.
Changes are made upstream and arrive here only through a new release export.

| | |
|---|---|
| Application source | `40ozs/adg` `integration/SYNTH-CROSSAPP-01` @ `1d585649e6cb103cb079dc40387dab9f1f613db2` |
| Synthetic world | `40ozs/synthetic-enterprise` @ `ce7c0c7d9fbc82c67e596dde95cf5e2432acf450` |
| Dataset / contract | `synthetic-enterprise-world@2.1.0` / `0.2.0` |
| Projection | `adg@0.3.0` (lock `backend/vendor/synthetic-enterprise/SYNTHETIC_ENTERPRISE.lock`, commit `ce7c0c7d9fbc82c67e596dde95cf5e2432acf450`) |
| Integration record | `docs/demo/reports/SYNTH-CROSSAPP-01-report.md` @ `296b528e5927f579f2513b6c43b750f50f1de8e8` |
| Release generated | 2026-10-28T23:56:37Z by `tools/cutover/demo_release.py` (SYNTH-CUTOVER-01) |

Machine-readable provenance: [`demo-release.json`](demo-release.json). Every file's digest:
[`demo-release/files.sha256`](demo-release/files.sha256).

## Verify

```sh
python3 demo-release/verify_release.py
```

checks that the tree is exactly the recorded release (no file added, removed or edited) and
that no prohibited file type is present. The release is reproducible: in
`40ozs/synthetic-enterprise`,

```sh
python3 tools/cutover/demo_release.py compare --app adg --source <adg checkout> --se . --demo <this checkout>
```

re-exports from the recorded commits and requires a byte-identical tree.

## What this release contains

The ADG application at the verified integration commit, with the vendored Genesee Press projection
(`adg@0.3.0`, 206-group catalogue, `geneseepress.example`, `sec-*` naming) and its lock. Left out on
purpose: the historical run reports and evidence (`docs/demo/reports/`, `docs/handoffs/`; they stay in the
source repository), the source repository's development CI, and the real-workstation Windows capture
(SYNTH-DISCOVERY-01 U-02) together with the one test and the one probe script that use it. No source
history is included.

## Hosted demo

The public demo staging (Cloudflare Worker `adg-demo-staging` → Render `adg-demo-web` → Supabase `adg_demo`)
deploys **from this repository** with **Actions → Free staging (ADG demo) → Run workflow** on `main`
([docs/deployment/cloudflare-demo.md](docs/deployment/cloudflare-demo.md)). The first deploy of this release
runs with `bootstrap: true` and `confirm_reset: reset adg_demo`, because the hosted database still holds
the previous dataset. Expected after the reset: Demo Mode fingerprint `4667d3cf…9b270f08`, logical
fingerprint `b4b93b65…e59445d0`, probes 23/23, 9,386 open findings, 2,440 employees, 206 groups, 4,273
membership edges.

Owner prerequisites (one time, outside Git): the GitHub environment `cloudflare-staging` in this
repository with the secrets and variables listed in the deployment guide §4; the Render service
`adg-demo-web` connected to `40ozs/adg-demo`, branch `main`, auto-deploy off, `ADG_DEMO_DATASET=genesee-press-v1`.
