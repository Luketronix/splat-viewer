The repository currently contains only Git metadata locally; refer to the remote at https://github.com/Luketronix/splat-viewer.git for the full source.

This file tells AI coding agents how to be immediately productive when working with this repository. If you (the agent) find the workspace empty, follow the "first steps" section below before making changes.

1. First steps when the workspace is empty
- Check the Git remote and branches: the repo remote is in `.git/config` (example: `https://github.com/Luketronix/splat-viewer.git`). If local files are missing, fetch and checkout the main branch: `git fetch --all` and `git checkout main` (or the default branch). Ask the user before performing any push.
- If network access is not available, ask the user where the source files are or whether you should create scaffolding.

2. How to discover the project type and build/test commands (do these in this order)
- Look for build manifests in the repo root: `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `setup.py`, `pom.xml`, `Makefile`, `Dockerfile`.
- If `package.json` exists: inspect `scripts` for `start`, `dev`, `build`, `test` and prefer `npm ci` (or `pnpm install`/`yarn install`) then the appropriate script (e.g. `npm run build`, `npm test`). Give exact script names in your PR/body.
- If `pyproject.toml` / `requirements.txt`: use `python -m venv .venv` + `pip install -r requirements.txt` or `pip install -e .` and run `pytest` if present.
- If no manifest is found, search for top-level folders `src/`, `app/`, `frontend/`, `backend/`, `static/`, `public/` to infer architecture.

3. Architecture / important places to check (examples you will reference in PRs)
- Top-level `src/` or `frontend/` — likely UI/viewer code (look for React/Vue/Svelte files). Example: if you find `src/index.tsx` or `src/main.jsx`, follow the framework conventions.
- `backend/`, `server/`, or `api/` — server-side code and integration points. Look for `routes`, `controllers`, `Dockerfile`, or `requirements.txt` there.
- `static/`, `public/`, `assets/` — static assets for the viewer.
- `.github/workflows/` — CI build and test commands; mirror them locally where possible so suggested changes match CI.

4. Project-specific conventions and patterns to preserve
- If you find `README.md`, use it as the authoritative source for high-level intent and local dev commands. If README is missing, ask the user what the canonical developer flow is before making assumptions.
- Preserve any custom scripts under `scripts/` or `tools/`. Mention script names explicitly when suggesting changes.
- Follow existing coding styles in the repo (indentation, TypeScript vs JavaScript, use of ESLint/Prettier). If no linters are present, do not introduce new formatting rules without the user's consent.

5. Cross-component communication and integration points
- Look for configuration files (eg. `.env`, `config/*.json`, `settings/*.yaml`) that store endpoints, keys, or feature flags. Do not expose secrets — if necessary, replace values with `<REDACTED>` and prompt the user.
- If repository uses submodules or git-lfs (presence in `.git/config`), note large assets and avoid re-adding them directly.

6. What to change in PRs (practical checklist for AI edits)
- Keep changes minimal and focused: one behavioral change or feature per PR. When adding files, include a short `README` or `USAGE` note.
- When adding or changing scripts, update `README.md` with the exact commands to run locally and the expected outputs.

7. When you can't discover key info
- Ask concise questions: e.g. "Where are the source files for this project?" or "Which package manager should I use (npm/pnpm/yarn) for this repo?" Provide 2-3 options inferred from the tree.

8. Example snippets to include in PR bodies (copy/paste friendly)
- "I checked the repository root and found a `package.json` with a `build` script — I used `npm ci && npm run build` to reproduce the build locally. Updated files: `...`"
- "Repository appears to be empty locally; I inspected `.git/config` and found remote `https://github.com/Luketronix/splat-viewer.git`. Please confirm if you want me to fetch/checkout the remote main branch or create starter scaffolding." 

If anything in this file is unclear or you want the instructions tuned to a particular language or framework (React, Vue, Python, Rust, etc.), tell me which stack to prioritize and I will update this file accordingly.

-- End of copilot-instructions for splat-viewer
