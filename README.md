# 🌐 Reusable PHP Login CI / CI PHP Login Reutilizável

| 🇺🇸 English | 🇧🇷 Português |
|-------------|--------------|
| This repository contains a **reusable GitHub Actions workflow** designed for **PHP 8.2** projects.<br>It was built to **automate continuous integration (CI) tasks**, such as syntax validation and environment setup, and can be easily called from other repositories. | Este repositório contém um **workflow reutilizável** do GitHub Actions voltado para projetos em **PHP 8.2**.<br>Ele foi pensado para **automatizar tarefas de integração contínua (CI)**, como validação de sintaxe e configuração de ambiente, podendo ser facilmente chamado a partir de outros repositórios. |

---

## 🚀 What it does / O que ele faz

| 🇺🇸 English | 🇧🇷 Português |
|-------------|--------------|
| - Performs **checkout** of the source code.<br>- Sets up **PHP 8.2** using the official [`shivammathur/setup-php`](https://github.com/shivammathur/setup-php) action.<br>- Installs essential dependencies (`php-cli` and `php-mbstring`).<br>- Runs syntax check with `php -l index.php`.<br>- Finishes with a build success message. | - Faz **checkout** do código fonte.<br>- Configura o **PHP 8.2** usando a action oficial [`shivammathur/setup-php`](https://github.com/shivammathur/setup-php).<br>- Instala dependências essenciais (`php-cli` e `php-mbstring`).<br>- Executa a checagem de sintaxe com `php -l index.php`.<br>- Finaliza com a mensagem de sucesso da build. |

---

## 📂 Structure / Estrutura

| 🇺🇸 English | 🇧🇷 Português |
|-------------|--------------|
| `.github/workflows/login.yml` → reusable workflow (this repository). | `.github/workflows/login.yml` → workflow reutilizável (este repositório). |

---

## 🔗 How to use this workflow / Como usar este workflow

| 🇺🇸 English | 🇧🇷 Português |
|-------------|--------------|
| In another repository, you can call it as follows:<br><br>```yaml<br>name: Example CI<br><br>on: [push]<br><br>jobs:<br>  call-workflow:<br>    uses: user/example-repo/.github/workflows/login.yml@main<br>``` | Em outro repositório, você pode chamá-lo da seguinte forma:<br><br>```yaml<br>name: CI Exemplo<br><br>on: [push]<br><br>jobs:<br>  call-workflow:<br>    uses: usuario/exemplo-repo/.github/workflows/login.yml@main<br>``` |
