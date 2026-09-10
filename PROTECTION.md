# Preservation and controlled updates

After the site is deployed, the `main` branch is protected by an active ruleset with no bypass actors. It restricts updates, branch deletion and force-pushes. A separate active tag ruleset prevents updating or deleting release tags. This makes the published version read-only until the repository owner intentionally changes the rules.

These protections do **not** prevent a personal-account owner or repository administrator from changing the rules, changing Pages settings, or deleting the entire repository. GitHub does not provide an owner-proof deletion lock for a personal repository. See [GitHub: deleting a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/deleting-a-repository).

## Make a deliberate correction

1. Keep an independent backup and record the current commit before changing protection.
2. Prepare and review the correction on a separate branch.
3. In Settings > Rules > Rulesets, temporarily permit updates to `main` while retaining the deletion and force-push restrictions.
4. Merge the reviewed correction, check the Pages deployment, and re-enable the update lock.
5. Create a new version tag. Do not move or delete the old release tag.
6. Refresh the independent backup.

## Restore from the independent Git bundle

The local `positional-chess-v1.0.0.bundle` contains the complete initial repository history and release tag. To restore it into a new directory:

```sh
git clone positional-chess-v1.0.0.bundle positional-chess-restored
```

If restoration to GitHub is needed, create or select the intended repository, configure its remote, push the restored branches and tags, enable Pages from `main` at `/`, and recreate the protection rules. Check `SHA256SUMS.txt` before publishing restored PDF files. A Git bundle does not itself contain hosted repository settings or protection rules; their JSON exports accompany the local backup.
