# Instruções para Merge via Linha de Comando

## Pré-requisitos

Certifique-se de que você tem:
- Permissões para fazer push na branch `main`
- Git configurado corretamente

## Passo a Passo

### 1. Verificar branch atual e buscar atualizações

```bash
# Ver em qual branch você está
git branch

# Buscar atualizações do repositório remoto
git fetch origin
```

### 2. Ir para a branch main e atualizar

```bash
# Mudar para a branch main
git checkout main

# Atualizar com as últimas mudanças do remoto
git pull origin main
```

### 3. Fazer o merge da branch de feature

```bash
# Fazer merge da branch de feature na main
git merge claude/create-caio-villani-agent-011CUxiMdctpEbWQUi7oNDKX --no-ff

# A flag --no-ff cria um commit de merge mesmo que seja fast-forward
# Isso mantém o histórico mais claro
```

### 4. Resolver conflitos (se houver)

Se houver conflitos, o Git irá avisar. Você precisará:

```bash
# Ver quais arquivos têm conflitos
git status

# Editar os arquivos com conflitos manualmente
# Procure por marcadores como:
# <<<<<<< HEAD
# (seu código)
# =======
# (código da outra branch)
# >>>>>>> branch-name

# Após resolver, adicionar os arquivos
git add <arquivo-resolvido>

# Continuar o merge
git commit
```

### 5. Enviar as mudanças para o repositório remoto

```bash
# Enviar o merge para o GitHub
git push origin main
```

### 6. Deletar a branch de feature (opcional)

```bash
# Deletar localmente
git branch -d claude/create-caio-villani-agent-011CUxiMdctpEbWQUi7oNDKX

# Deletar no remoto
git push origin --delete claude/create-caio-villani-agent-011CUxiMdctpEbWQUi7oNDKX
```

## Verificação

Para confirmar que o merge foi bem-sucedido:

```bash
# Ver o log de commits
git log --oneline --graph -10

# Verificar que os arquivos estão na main
ls -la caiovillani-agent/
```

Você deve ver o commit de merge e os 5 arquivos do skill:
- SKILL.md
- README.md
- reference/frameworks-metodologicos.md
- reference/exemplos-aplicacao.md
- reference/glossario-recursos.md

## Troubleshooting

### Erro: "Permission denied" ou "403"

Isso significa que a branch main está protegida. Soluções:

1. **Use a interface do GitHub** (método recomendado)
2. **Configure branch protection rules** no GitHub para permitir push direto
3. **Peça a um administrador** do repositório para fazer o merge

### Erro: "Your branch is behind"

Você precisa atualizar sua branch local:

```bash
git pull origin main --rebase
git push origin main
```

### Erro: "Merge conflict"

Siga os passos de resolução de conflitos acima.

## Comandos Úteis

```bash
# Ver diferenças antes do merge
git diff main..claude/create-caio-villani-agent-011CUxiMdctpEbWQUi7oNDKX

# Ver estatísticas do que será mergeado
git diff --stat main..claude/create-caio-villani-agent-011CUxiMdctpEbWQUi7oNDKX

# Cancelar um merge em progresso
git merge --abort

# Ver histórico gráfico
git log --oneline --graph --all -20
```
