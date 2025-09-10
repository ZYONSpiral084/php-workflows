# 可重用的 PHP 登录 CI / Reusable PHP Login CI
**2025-09-10**

**语言：** [English](README.md) • [Português (pt-BR)](README.pt-BR.md) • [中文（简体）](README.zh-CN.md)

---

## 概述

本仓库包含适用于 **PHP 8.2** 项目的**可重用 GitHub Actions 工作流**，用于自动化持续集成（CI）任务，如语法验证与环境配置，并可被其他仓库调用。

---

## 功能

- 执行源码 checkout。  
- 使用 `shivammathur/setup-php` 配置 PHP 8.2。  
- 安装必要依赖（`php-cli`、`php-mbstring`）。  
- 使用 `php -l index.php` 进行语法检查。  
- 输出构建成功信息。

---

## 结构

`.github/workflows/login.yml` → 可重用工作流（本仓库）。

---

## 使用方法

在其他仓库中调用示例：

```yaml
name: Example CI
on: [push]

jobs:
  call-workflow:
    uses: user/example-repo/.github/workflows/login.yml@main
```

---

## 备注

- 将 `user/example-repo` 替换为实际 owner/repo，并将 `@main` 替换为目标 ref/分支。  
- 确保调用仓库包含 `index.php` 等目标文件。  
- 建议固定 ref（tag/commit）以保证可重复性。
