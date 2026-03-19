# AGENTS.md — taptap/terraform-provider-volcenginecc

This file documents how to maintain the TapTap fork of
[volcengine/terraform-provider-volcenginecc](https://github.com/volcengine/terraform-provider-volcenginecc).

## Versioning convention

We do **not** bump the minor/patch version. Instead we append a patch suffix:

```
v0.0.<N>-patch.<M>
```

where `<N>` matches the upstream tag we branched from and `<M>` increments
for each fix we release. Example: `v0.0.33-patch.2`.

## Syncing from upstream

```bash
git remote add upstream https://github.com/volcengine/terraform-provider-volcenginecc.git
git fetch upstream
git merge upstream/main   # resolve conflicts if any
```

## Releasing a new version

1. Commit all changes to `main`.
2. Create and push a new tag:
   ```bash
   git tag v0.0.<N>-patch.<M>
   git push taptap v0.0.<N>-patch.<M>
   ```
3. If the tag push does not trigger the Release workflow automatically, trigger it manually:
   ```bash
   gh workflow run Release --repo taptap/terraform-provider-volcenginecc \
     --ref v0.0.<N>-patch.<M> --field tag=v0.0.<N>-patch.<M>
   ```
4. Wait for the workflow to complete and verify on the Terraform Registry:
   ```
   https://registry.terraform.io/providers/taptap/volcenginecc
   ```
