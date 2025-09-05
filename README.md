# 🌐 Reusable PHP Login CI

This repository contains a **reusable GitHub Actions workflow** designed for **PHP 8.2** projects.  
It was built to **automate continuous integration (CI) tasks**, such as syntax validation and environment setup, and can be easily called from other repositories.

---

## 🚀 What it does
- Performs **checkout** of the source code.  
- Sets up **PHP 8.2** using the official [`shivammathur/setup-php`](https://github.com/shivammathur/setup-php) action.  
- Installs essential dependencies (`php-cli` and `php-mbstring`).  
- Runs syntax check with `php -l index.php`.  
- Finishes with a build success message.  

---

## 📂 Structure
- `.github/workflows/login.yml` → reusable workflow (this repository).

---

## 🔗 How to use this workflow
In another repository, you can call it as follows:

```yaml
name: Example CI

on: [push]

jobs:
  call-workflow:
    uses: user/example-repo/.github/workflows/login.yml@main

---

# 🌐 CI PHP Login Reutilizável

Este repositório contém um **workflow reutilizável** do GitHub Actions voltado para projetos em **PHP 8.2**.  
Ele foi pensado para **automatizar tarefas de integração contínua (CI)**, como validação de sintaxe e configuração de ambiente, podendo ser facilmente chamado a partir de outros repositórios.

---

## 🚀 O que ele faz
- Faz **checkout** do código fonte.  
- Configura o **PHP 8.2** usando a action oficial [`shivammathur/setup-php`](https://github.com/shivammathur/setup-php).  
- Instala dependências essenciais (`php-cli` e `php-mbstring`).  
- Executa a checagem de sintaxe com `php -l index.php`.  
- Finaliza com a mensagem de sucesso da build.  

---

## 📂 Estrutura
- `.github/workflows/login.yml` → workflow reutilizável (este repositório).

---

## 🔗 Como usar este workflow
Em outro repositório, você pode chamá-lo da seguinte forma:

```yaml
name: CI Exemplo

on: [push]

jobs:
  call-workflow:
    uses: usuario/exemplo-repo/.github/workflows/login.yml@main
