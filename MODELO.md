# Modelo para documentar uma tabela

Copie o bloco abaixo para o arquivo do assunto em `tabelas/` (ou crie um arquivo novo) e atualize o índice do `SKILL.md`.

```markdown
## `nome_da_tabela`

- **Onde:** Lakehouse `NomeDoLakehouse` → `dbo.nome_da_tabela`  (ou "outro workspace do Fabric (link a confirmar)")
- **Objetivo:** Traz ... (uma frase: para que serve)
- **Atualização:** diária / mensal / manual / desatualizada
- ⚠️ Avisos: preenchimento manual, unidades (segundos, centavos), colunas duplicadas de outra tabela etc.

**Colunas:**

| coluna | tipo | significado |
|---|---|---|
| `coluna_1` | varchar | ... |
| `dt_ref` | date | data de referência; use para filtrar período |

**Como filtrar / regras de negócio:**
- Para X, use `WHERE ...`
```

Regras:
- Use os nomes **exatamente** como estão no Fabric (confira com `describe` na skill fabric-readonly).
- Não escreva dados reais de clientes (CPF, nomes, contas), senhas ou links de conexão: o repositório é público.
- Se não souber o significado de uma coluna, deixe em branco em vez de chutar.
