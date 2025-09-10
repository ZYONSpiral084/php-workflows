# 可重用的 PHP 登录 CI / Reusable PHP Login CI
**2025-09-10**

**语言：** [English](README.md) • [Português (pt-BR)](README.pt-BR.md) • [中文（简体）](README.zh-CN.md)

---

## 📌 概述

本仓库提供一个面向 PHP 8.2 项目的**可重用 GitHub Actions 工作流**，用于自动化基本 CI 检查（环境设置、语法验证）。工作流通过 `workflow_call` 触发，可由其他仓库调用，并可固定到特定 tag/sha 以确保稳定性。

---

## 🚀 功能

- 检出仓库代码。  
- 使用 `shivammathur/setup-php` 设置 PHP（默认 8.2，可配置）。  
- 通过 setup-action 安装常用扩展（`mbstring`）。  
- 对可配置的目标文件（默认 `index.php`）执行语法检查 `php -l`。  
- 输出清晰日志并使用恰当的退出码，适合 CI gating。

---

## 📂 结构

```
.github/
  workflows/
    login.yml         # <- 可重用工作流（本仓库）
README.md
README.pt-BR.md
README.zh-CN.md
```

---

## 🔗 使用方法（调用示例）

在其他仓库中添加 job 来调用此工作流，例如：

```yaml
# .github/workflows/consume-login.yml
name: PHP Login CI (consume reusable)
on:
  push:
    branches: [ "main", "master" ]
  pull_request:

jobs:
  call-login:
    uses: YOUR-USER/Reusable-PHP-Login-CI/.github/workflows/login.yml@main
    with:
      php-version: '8.2'
      target-file: 'index.php'
```

请将 `YOUR-USER/Reusable-PHP-Login-CI` 修改为实际 owner/repo，并建议固定到 tag/sha。

---

## 🧩 推荐的 login.yml 内容

（请参见 README.md 中的完整示例）

---

## ✅ 输入 / 输出

- 输入：`php-version`（可选，默认 `8.2`），`target-file`（可选，默认 `index.php`）。  
- 输出：`file-checked` — 被检查文件路径。

---

## 🔐 安全与最佳实践

- 在调用时建议使用 tag（如 `@v1.0.0`）以保证稳定性。  
- 不要提交秘密；使用 GitHub Secrets 传递敏感信息。  
- 如需更严格检查，可添加 PHPStan/PSalm 与单元测试。

---

## 🧭 维护建议

- 对此工作流发布版本并通知消费者更新引用。  
- 将 README.md（英文）作为事实来源，翻译做为辅助文档。

---

## 📜 许可

学术 / 教育用途。重复使用请注明作者。
