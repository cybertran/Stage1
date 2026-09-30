# Stage1 — Roadbreak public build bridge

This public repository contains **only the build/release workflow** for Roadbreak '75. The game source remains private in `cybertran/Roadbreak-75`.

The workflow uses GitHub-hosted public-repository runners for QA and Android export, then publishes the APK directly to a Stage1 GitHub Release. It intentionally does **not** use `actions/upload-artifact`.

## One required secret

In Stage1, create the repository Actions secret:

`ROADBREAK_SOURCE_TOKEN`

Use a fine-grained GitHub personal access token restricted to **only** `cybertran/Roadbreak-75`, with repository **Contents: Read-only**. Do not grant write/admin access and do not grant access to other repositories.

Path in GitHub UI:

`Stage1 → Settings → Secrets and variables → Actions → New repository secret`

After the secret exists, run:

`Actions → Roadbreak Public Builder → Run workflow`

The default source ref is now `refine/hardsurface-quality-pass`, the validated development branch.

## Security boundary

Stage1 must never contain:
- Roadbreak private source code;
- professional Sonniss/source WAV libraries whose licenses restrict isolated redistribution;
- personal tokens in YAML or commits.

The secret is consumed only by `actions/checkout` to read the private source. The APK and SHA-256 file are the only persistent build outputs published by this repository.
