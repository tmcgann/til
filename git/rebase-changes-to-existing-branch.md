If you make some commits on the wrong feature or development branch and you want to move them to another branch, you can use rebase to drop them onto the appropriate branch.

```bash
gco dev
git rebase --onto dev 35172ee 1411542
git branch -f dev cb6e273
gco feature/feat-1
git reset --hard HEAD~2
```

1. Checkout the target branch where you want your commits to end up
2. Rebase (`git rebase`) onto the target branch (`--onto <target>`) providing two references (i.e. hash, branch name, etc.) that declare the range of commits to rebase where the first reference is excluded (all commits after it apply) and hte second reference is inclusive (all commits upto and including this reference apply).
3. If necessary, move the pointer of your branch to the new commit hash.
4. Checout your feature branch
5. Reset that feature branch back to commit where you wish you had stopped making changes previously.
