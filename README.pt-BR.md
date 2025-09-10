# 🌐 CI PHP Login Reutilizável
**2025-09-10**

**Idiomas:** [English](README.md) • [Português (pt-BR)](README.pt-BR.md) • [中文（简体）](README.zh-CN.md)

---

## 📌 Visão Geral

Este repositório fornece um **workflow reutilizável do GitHub Actions** para projetos em PHP 8.2, focado em automatizar verificações básicas de CI como configuração de ambiente e validação de sintaxe. O workflow pode ser chamado por outros repositórios via `workflow_call` e é fácil de travar (pin) para uso estável.

---

## 🚀 Funcionalidades

- Faz checkout do código-fonte.  
- Configura PHP (versão configurável; padrão 8.2) com `shivammathur/setup-php`.  
- Instala extensões comuns (`mbstring`).  
- Realiza checagem de sintaxe (`php -l`) no arquivo configurável (padrão `index.php`).  
- Gera logs claros e códigos de saída adequados para gates de CI automatizados.

---

## 📂 Estrutura

```
.github/
  workflows/
    login.yml         # <- Workflow reutilizável (este repositório)
README.md
README.pt-BR.md
README.zh-CN.md
```

---

## 🔗 Como usar (repositório que consome o workflow)

Exemplo de workflow no repositório que chama este workflow:

```yaml
# .github/workflows/consume-login.yml
name: PHP Login CI (consumir reusável)
on:
  push:
    branches: [ "main", "master" ]
  pull_request:

jobs:
  call-login:
    uses: SEU-USUARIO/Reusable-PHP-Login-CI/.github/workflows/login.yml@main
    with:
      php-version: '8.2'
      target-file: 'index.php'
```

Substitua `SEU-USUARIO/Reusable-PHP-Login-CI` pelo owner/repo reais e prefira usar uma tag ou SHA.

---

## 🧩 Exemplo completo do workflow reutilizável (login.yml)

Copie este arquivo para `.github/workflows/login.yml` no repositório deste projeto:

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

## ✅ Inputs / Saídas

- Inputs:
  - `php-version` — opcional, padrão `8.2`.
  - `target-file` — opcional, padrão `index.php`.
- Saídas:
  - `file-checked` — caminho do arquivo verificado.

---

## 🔐 Segurança & Boas práticas

- **Trave** a referência ao usar (`uses: owner/repo/.github/workflows/login.yml@v1.0.0`).  
- Não comite segredos; use GitHub Secrets e passe-os do repositório consumidor quando necessário.  
- Restrinja permissões do runner se o job não precisar de acesso amplo.  
- Para pipelines reais, acrescente testes automatizados e verificadores estáticos (PHPStan/PSalm).

---

## 🧪 Testes & Debug

- Teste localmente com `php -l index.php`.  
- Use `workflow_dispatch` em um workflow consumidor para testes rápidos.  
- Os passos de debug mostram `php -v` e `php -m` para inspecionar runtime.

---

## 🛠️ Solução de problemas

- Erros de sintaxe: verifique a linha apontada pelo `php -l` e corrija.  
- Extensões: adicione o nome da extensão no campo `extensions` do `setup-php`.  
- Arquivo não encontrado: ajuste `target-file` para o caminho correto no repositório consumidor.

---

## 🔁 Manutenção & versionamento

- Faça releases/ tags (v1.0.0) e atualize repositórios consumidores para referenciar tags.  
- Atualize o README em inglês como fonte principal e repita traduções conforme necessário.

---

## 🧭 Fluxo Git sugerido

```bash
git checkout -b add/reusable-workflow-readme
git add README*.md .github/workflows/login.yml
git commit -m "Add README and reusable login workflow"
git push origin add/reusable-workflow-readme
```

---

## 📜 Licença

Uso acadêmico / educacional. Cite o autor ao reutilizar.
