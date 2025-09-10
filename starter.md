# Instructions: Use GitHub to Save and Manage Markdown

## 1) Create the repository
- **On GitHub**: New repository → Name it (e.g., `docs`), choose Public/Private, add a `README.md` and a license.
- **Locally**:
```bash
git clone https://github.com/<you>/<repo>.git
cd <repo>
```

## 2) Establish structure
- **Suggested layout**:
```
├── docs/
│   ├── getting-started/
│   ├── guides/
│   ├── reference/
│   └── assets/
│       ├── images/
│       └── diagrams/
├── .github/
│   ├── workflows/
│   └── ISSUE_TEMPLATE/
├── .markdownlint.json
├── .gitignore
├── README.md
└── CONTRIBUTING.md
```
- **Naming**: Use kebab-case (`getting-started.md`), one H1 per file, descriptive titles.

## 3) Authoring conventions
- Prefer short lines (≤ 100 chars), meaningful headings, and descriptive link text.
- Always add alt text to images and specify code block languages.
- Cross-link related docs; keep a Table of Contents in `README.md`.

## 4) Ignore and lint
- `.gitignore` basics:
```gitignore
.DS_Store
node_modules/
dist/
_site/
```
- Markdown lint config `.markdownlint.json` (example):
```json
{
  "MD013": { "line_length": 100 },
  "MD033": false,
  "MD041": true
}
```
- Optional local linting:
```bash
npm i -D markdownlint-cli
npx markdownlint "**/*.md" --ignore node_modules
```

## 5) Automate checks with GitHub Actions
- Create `.github/workflows/markdown.yml`:
```yaml
name: Markdown CI
on:
  pull_request:
  push:
    branches: [ main ]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm i -g markdownlint-cli markdown-link-check
      - name: Lint Markdown
        run: markdownlint "**/*.md" --ignore node_modules
      - name: Check Links
        run: |
          git ls-files "*.md" | xargs -n1 -I{} sh -c 'markdown-link-check -q {} || exit 1'
```

## 6) PR quality gates and templates
- Protect `main` branch: Require PRs, 1+ review, status checks (Actions) to pass, up-to-date branches.
- Add `.github/pull_request_template.md` with a checklist (headings, links, images alt text, lint passes).
- Add issue templates in `.github/ISSUE_TEMPLATE/` (bug, content request).

## 7) Writing and committing workflow
```bash
git checkout -b docs/add-getting-started
# create/edit files under docs/
git add .
git commit -m "docs: add getting started guide"
git push -u origin docs/add-getting-started
```
- Open a Pull Request; ensure checks pass; address review comments; merge via Squash and merge.

## 8) Publishing (optional)
- Enable GitHub Pages: Settings → Pages → Build from branch → select `main` and `/docs`.
- Use a simple static site generator (optional): MkDocs or Docsify.
  - MkDocs quick start:
  ```bash
  pip install mkdocs mkdocs-material
  mkdocs new .
  mkdocs serve
  ```
  - Add an Action to deploy (e.g., `mkdocs gh-deploy --force`).

## 9) Assets and links
- Store images under `docs/assets/images/`; reference with relative paths: `![Alt text](../assets/images/example.png)`.
- Prefer reference-style links for reuse; verify external links with CI.

## 10) Versioning and releases
- Use tags/releases for major documentation milestones.
- Keep a `CHANGELOG.md` summarizing notable documentation updates.

## 11) Collaboration and maintenance
- Define contribution rules in `CONTRIBUTING.md` (style, headings, link policy, review process).
- Periodically run link checks and lint locally; keep Actions green.
- Review open issues/PRs weekly; archive or prune stale content.

## 12) Backup and portability
- Clone to a second location or mirror the repo.
- Export site builds (if using a generator) to `dist/` for offline backup.

You now have a repeatable, CI-enforced workflow to create, review, and publish Markdown using GitHub.


