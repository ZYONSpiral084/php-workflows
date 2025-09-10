# 🌐 Reusable PHP Login CI / CI PHP Login Reutilizável
**2025-09-10**

**Languages:** [English](README.md) • [Português (pt-BR)](README.pt-BR.md) • [中文（简体）](README.zh-CN.md)

---

## 📌 Overview

This repository provides a **reusable GitHub Actions workflow** for PHP 8.2 projects, focused on automating basic CI checks such as environment setup and syntax validation. The workflow is designed to be called from other repositories using the `workflow_call` trigger and to be easy to pin and reuse in production or academic scenarios.

---

## 🚀 Features (what the workflow does)

- Checkout repository code.
- Setup PHP (configurable PHP version; default: 8.2) using `shivammathur/setup-php`.
- Install common PHP extensions (`mbstring`) via the setup action.
- Run a syntax check (`php -l`) against a configurable target file (default `index.php`).
- Provide clear logs and exit codes suitable for automated CI gates.

---

## 📂 Repository structure

```
.github/
  workflows/
    login.yml         # <- Reusable workflow (this repo)
README.md
README.pt-BR.md
README.zh-CN.md
```

---

## 🔗 Usage — Call the reusable workflow (consumer repo)

Add a job that calls this reusable workflow. Example consumer workflow:

```yaml
# .github/workflows/consume-login.yml in calling repository
name: PHP Login CI (consume reusable)
on:
  push:
    branches: [ "main", "master" ]
  pull_request:

jobs:
  call-login:
    uses: YOUR-USER/Reusable-PHP-Login-CI/.github/workflows/login.yml@main
    with:
      php-version: '8.2'       # optional (default 8.2)
      target-file: 'index.php' # optional
```

**Important:** Replace `YOUR-USER/Reusable-PHP-Login-CI` with the actual owner/repo and `@main` with a tag or commit SHA for stability.

---

## 🧩 Complete example of the reusable workflow (login.yml)

Below is a **recommended** implementation for `.github/workflows/login.yml`. It is ready to use and includes inputs, sensible defaults and descriptive steps. Copy it into the repository `.github/workflows/login.yml`.

```yaml
# .github/workflows/login.yml
name: Reusable PHP Login CI
on:
  workflow_call:
    inputs:
      php-version:
        description: 'PHP version to use'
        required: false
        default: '8.2'
      target-file:
        description: 'File to run syntax check on'
        required: false
        default: 'index.php'
    # No secrets required by default; calling workflow can pass secrets if needed

jobs:
  php-syntax-check:
    runs-on: ubuntu-latest
    outputs:
      file-checked: ${{ steps.check.outputs.file }}
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: ${{ inputs.php-version }}
          extensions: mbstring
          coverage: none

      - name: Show PHP info (debug)
        run: php -v && php -m

      - name: Check target file exists
        id: check
        run: |
          if [ -f "${{ inputs.target-file }}" ]; then
            echo "file_exists=true" >> $GITHUB_OUTPUT
            echo "file=${{ inputs.target-file }}" >> $GITHUB_OUTPUT
          else
            echo "file_exists=false" >> $GITHUB_OUTPUT
          fi

      - name: Syntax check
        if: steps.check.outputs.file_exists == 'true'
        run: |
          echo "Running php -l on ${{ inputs.target-file }}"
          php -l "${{ inputs.target-file }}"

      - name: Fail if file missing
        if: steps.check.outputs.file_exists == 'false'
        run: |
          echo "Target file '${{ inputs.target-file }}' not found. Failing the job."
          exit 1

      - name: Success message
        if: success()
        run: echo "PHP syntax check passed for ${{ inputs.target-file }} (PHP ${{ inputs.php-version }})"
```

---

## ✅ Inputs / Outputs (summary)

- Inputs:
  - `php-version` — optional, default `8.2`.
  - `target-file` — optional, default `index.php`.
- Outputs:
  - `file-checked` — path of the checked file (set by job output).

---

## 🔐 Security & best practices

- **Pin the workflow reference** when consuming (use tag or commit SHA) to avoid breaking changes: `uses: owner/repo/.github/workflows/login.yml@v1.0.0` or `@<sha>`.
- Do **not** commit secrets or credentials. Use GitHub Secrets and pass them securely from the calling workflow when necessary.
- Limit runner permissions if the workflow doesn't need broad access (see `permissions:` in the consumer workflow).
- For production pipelines, extend checks with unit tests and static analyzers (PHPStan, Psalm).

---

## 🧪 Testing & debugging

- Test locally by running the target PHP file through `php -l index.php`.
- Add a temporary consumer workflow that triggers on `workflow_dispatch` to iterate quickly.
- Use `echo`/`php -v` steps (as included) to collect debug info on the runner.

---

## 🛠️ Troubleshooting

- **`php -l` reports parse errors:** fix syntax in the target file; the output includes the file and line number.
- **Extensions missing:** ensure `shivammathur/setup-php` installs needed extensions (add to `extensions:`) or install via package manager if required.
- **File not found:** verify `target-file` is at the repository root or adjust the path in the consumer workflow.

---

## 🔁 Maintenance & versioning

- Tag stable releases of this reusable workflow (`v1.0.0`, `v1.1.0`, ...).
- When fixing or adding features, increment the tag and update consumer repos to reference the new tag.
- Keep `README.md` (English) as the source of truth and update translations accordingly.

---

## 🧭 Git workflow suggestion

```bash
git checkout -b add/reusable-workflow
git add .github/workflows/login.yml README*.md
git commit -m "Add reusable PHP login CI workflow and docs"
git push origin add/reusable-workflow
```

---

## 📜 License

Academic / educational use. Please cite the author if you reuse this content.

---
