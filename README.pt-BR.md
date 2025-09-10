# CI PHP Login Reutilizável
**2025-09-10**

**Idiomas:** [English](README.md) • [Português (pt-BR)](README.pt-BR.md) • [中文（简体）](README.zh-CN.md)

---

## Visão Geral

Este repositório contém um workflow reutilizável do GitHub Actions para projetos em PHP 8.2. Automação de tarefas de CI como validação de sintaxe e configuração do ambiente.

---

## O que ele faz

- Faz checkout do código fonte.  
- Configura PHP 8.2 com `shivammathur/setup-php`.  
- Instala dependências essenciais (`php-cli`, `php-mbstring`).  
- Executa `php -l index.php` (checagem de sintaxe).  
- Exibe mensagem de sucesso ao final.

---

## Estrutura

`.github/workflows/login.yml` → workflow reutilizável (este repositório).

---

## Como usar

Exemplo de uso em outro repositório:

```yaml
name: CI Exemplo
on: [push]

jobs:
  call-workflow:
    uses: usuario/exemplo-repo/.github/workflows/login.yml@main
```

---

## Observações

- Substitua `usuario/exemplo-repo` pelo owner/repo correto e `@main` pelo branch/ref desejado.  
- Verifique se `index.php` existe no repositório que chama.  
- Prefira travar um ref (tag / commit) para estabilidade.
