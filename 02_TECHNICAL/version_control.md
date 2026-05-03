# Version Control Guidelines

## 1. Branch Structure
- `main`: always holds the latest stable build for deployment or release-ready code.
- `dev`: active integration branch for work in progress and feature completion.
- `feature/*`: create a branch for each task or small scope, e.g. `feature/player-movement`, `feature/ui-fix`.
- Workflow: branch off `dev`, finish the feature, then merge back into `dev`.
- Only merge `dev` into `main` when the project is stable and tested.

## 2. Commit Message Conventions
- Keep commits small and focused.
- Use present-tense, imperative style: `Add`, `Fix`, `Update`, `Remove`.
- Format: `type(scope): short summary`
  - Example: `fix(player): correct jump height`
- Optional body for details if needed, but keep it concise.
- Avoid vague messages like `stuff`, `update`, or `changes`.

## 3. Merge Procedure
- Push branch to GitHub and create a pull request into `dev`.
- Review with your teammate before merging.
- Confirm the branch is up to date with `dev` and resolve conflicts locally.
- Use fast-forward or squash merges for feature branches to keep history clean.
- After review, merge into `dev`. Optionally delete the feature branch after merge.
- When `dev` is stable, create a pull request into `main` and merge after final validation.

## 4. Repo vs External Storage
- Store source code, scripts, configuration files, and small text assets in GitHub.
- Keep large generated builds, video captures, raw audio, and art source files out of the repo.
- Use external cloud storage for backups, large archives, and files that change rarely but are heavy.
- In the repo, include instructions or links in `README` to access external assets if needed.

## 5. Large Binary Assets and Git LFS
- Use Git LFS for large binary files that must stay in the repo, such as final textures, sound effects, or models.
- Track only specific large file types: `git lfs track "*.png"`, `"*.wav"`, `"*.fbx"`, etc.
- Commit the `.gitattributes` file so the team shares the same LFS rules.
- Keep binary assets as small as practical and avoid frequently changing large files.
- If a file becomes too large or changes too often, move it to external storage instead of forcing it through Git.

## Practical Notes
- Keep branches short-lived and merge often.
- Use issues or a shared task list to decide who owns each feature branch.
- Keep the repo clean: no generated builds, no build artifacts, no OS files.
- Communicate on GitHub PR comments or your team chat for merge timing and conflict resolution.
