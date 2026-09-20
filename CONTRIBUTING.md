# Contributing to COBOL Cookbook

Welcome! This repo is the hands-on lab for the SRM FOSS Club COBOL workshop. Every folder under `programs/` is a self-contained task — pick one, write the code, open a PR, get it reviewed, and merge.

## How to Participate

1. **Claim an issue** — Comment "I'm on this" on any open issue with the `good first issue` label. A volunteer will add the `assigned` label.
2. **Fork & clone** — Fork this repo, clone your fork locally.
3. **Create a branch** — `git checkout -b feat/001-bizzbuzz` (use the issue number).
4. **Write your program** — Add a `.cbl` file in the issue's folder (e.g., `programs/001-bizzbuzz/bizzbuzz.cbl`). Use the starter skeleton from the issue.
5. **Test locally** — `cobc -x -free yourfile.cbl -o prog && ./prog` (or use the online compiler link in the issue).
6. **Add test input** — If your program reads from stdin, include a `test-input.txt` in the same folder.
7. **Commit & push** — `git add . && git commit -m "feat: solve #001 bizzbuzz" && git push origin feat/001-bizzbuzz`
8. **Open a PR** — Use the PR template. CI will compile and run your code.
9. **Respond to review** — A reviewer may ask for changes. Push more commits to the same branch.
10. **Merge!** — Once approved, your PR gets merged. 🎉

## Rules

- **One person = one issue at a time**. Finish your current PR before claiming another.
- **Claim timeout**: If you don't push a PR within 45 minutes of claiming, the issue is released back to the pool.
- **No conflicts by design** — Each program lives in its own folder. You never edit someone else's files.
- **CI must pass** — Your PR won't be merged until the GitHub Action shows green.

## COBOL Quick Reference

See `CHEATSHEET.md` (printed at the event) for one-page syntax reminders:
- `DISPLAY` / `ACCEPT`
- `MOVE` / `COMPUTE`
- `IF` / `ELSE` / `EVALUATE`
- `PERFORM UNTIL` / `PERFORM VARYING`
- `PIC 9` / `PIC X` / `PIC 99V99`

## Need Help?

- **During the event**: Find a Table Captain (desk signs) or the Reviewer Desk.
- **After the event**: Open a GitHub Discussion or ping @fossclubsrmktr on GitHub.

## License

Code: MIT — do whatever you want.
Documentation: CC BY-SA 4.0 — share with attribution.