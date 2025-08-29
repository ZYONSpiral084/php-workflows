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
