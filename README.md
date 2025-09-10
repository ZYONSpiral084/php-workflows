# 🌐 Reusable PHP Login CI / CI PHP Login Reutilizável
**2025-09-10**

**Languages:** [English](README.md) • [Português (pt-BR)](README.pt-BR.md) • [中文（简体）](README.zh-CN.md)

---

## 📌 Overview / Visão Geral / 概览

| 🇺🇸 English | 🇧🇷 Português | 🇨🇳 中文（简体） |
|---|---|---|
| This repository contains a **reusable GitHub Actions workflow** designed for **PHP 8.2** projects. It was built to **automate continuous integration (CI) tasks**, such as syntax validation and environment setup, and can be easily called from other repositories. | Este repositório contém um **workflow reutilizável** do GitHub Actions voltado para projetos em **PHP 8.2**. Ele foi pensado para **automatizar tarefas de integração contínua (CI)**, como validação de sintaxe e configuração de ambiente, podendo ser facilmente chamado a partir de outros repositórios. | 本仓库包含一个面向 **PHP 8.2** 项目的**可重用 GitHub Actions 工作流**。它用于自动化持续集成（CI）任务，例如语法验证与环境配置，并可被其他仓库方便地调用。 |

---

## 🚀 What it does / O que ele faz / 功能

| 🇺🇸 English | 🇧🇷 Português | 🇨🇳 中文（简体） |
|---|---|---|
| - Performs **checkout** of the source code.<br>- Sets up **PHP 8.2** using the official `shivammathur/setup-php` action.<br>- Installs essential dependencies (`php-cli` and `php-mbstring`).<br>- Runs syntax check with `php -l index.php`.<br>- Finishes with a build success message. | - Faz **checkout** do código fonte.<br>- Configura o **PHP 8.2** usando a action oficial `shivammathur/setup-php`.<br>- Instala dependências essenciais (`php-cli` e `php-mbstring`).<br>- Executa a checagem de sintaxe com `php -l index.php`.<br>- Finaliza com a mensagem de sucesso da build. | - 执行源码 **checkout**。<br>- 使用官方 `shivammathur/setup-php` action 配置 **PHP 8.2**。<br>- 安装必要依赖（`php-cli` 与 `php-mbstring`）。<br>- 使用 `php -l index.php` 进行语法检查。<br>- 最终输出构建成功信息。 |

---

## 📂 Structure / Estrutura / 结构

| 🇺🇸 English | 🇧🇷 Português | 🇨🇳 中文（简体） |
|---|---|---|
| `.github/workflows/login.yml` → reusable workflow (this repository). | `.github/workflows/login.yml` → workflow reutilizável (este repositório). | `.github/workflows/login.yml` → 可重用工作流（本仓库）。 |

---

## 🔗 How to use this workflow / Como usar este workflow / 如何使用此工作流

| 🇺🇸 English | 🇧🇷 Português | 🇨🇳 中文（简体） |
|---|---|---|
| In another repository, you can call it as follows:<br><br>```yaml
name: Example CI

on: [push]

jobs:
  call-workflow:
    uses: user/example-repo/.github/workflows/login.yml@main
``` | Em outro repositório, você pode chamá-lo da seguinte forma:<br><br>```yaml
name: CI Exemplo

on: [push]

jobs:
  call-workflow:
    uses: usuario/exemplo-repo/.github/workflows/login.yml@main
``` | 在其他仓库中，您可以如下调用：<br><br>```yaml
name: Example CI

on: [push]

jobs:
  call-workflow:
    uses: user/example-repo/.github/workflows/login.yml@main
``` |

---

## ✅ Notes / Observações / 备注

| 🇺🇸 English | 🇧🇷 Português | 🇨🇳 中文（简体） |
|---|---|---|
| - Replace `user/example-repo` with the actual owner/repo and `@main` with the intended ref/branch.<br>- Ensure `index.php` or target files exist in the calling repository; otherwise the syntax check will fail.<br>- Prefer to pin to a ref (tag / commit) for reproducibility. | - Substitua `user/example-repo` pelo owner/repo correto e `@main` pelo ref/branch desejado.<br>- Garanta que `index.php` ou os arquivos alvo existam no repositório que chama; caso contrário a checagem de sintaxe falhará.<br>- Prefira travar um ref (tag / commit) para reprodutibilidade. | - 将 `user/example-repo` 替换为实际的 owner/repo，并将 `@main` 替换为目标 ref/分支。<br>- 确保调用仓库中存在 `index.php` 或目标文件，否则语法检查将失败。<br>- 推荐固定到某个 ref（tag/commit）以保证可重复性。 |

---

## 🔁 Git workflow suggestion / Sugestão de fluxo Git / Git 工作流建议

```bash
git checkout -b add/reusable-workflow-readme
git add README.md README.pt-BR.md README.zh-CN.md .github/workflows/login.yml
git commit -m "Add README for reusable PHP login CI workflow"
git push origin add/reusable-workflow-readme
# open PR and request review
```

---

## 📜 License / Licença / 许可证

| 🇺🇸 English | 🇧🇷 Português | 🇨🇳 中文（简体） |
|---|---|---|
| Academic / educational use. Please cite the author when reusing. | Uso acadêmico / educacional. Cite o autor ao reutilizar. | 学术 / 教育用途。重复使用请注明作者。 |
