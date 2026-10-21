# fabric-dicionario

Skill do **Claude Code** com o **dicionário das tabelas do Microsoft Fabric** da Quero-Quero: o que cada tabela contém, onde está, colunas e regras de negócio.

Você pergunta em português (*"onde acho o TMA dos operadores?"*, *"como filtro só o SAC?"*, *"o que tem nas tabelas de monitoria?"*) e o Claude responde com base no dicionário.

- **Não precisa de conexão, login nem Python.** É só conhecimento.
- Para **consultar os dados**, instale também a skill de conexão: **[fabric-skill](https://github.com/VerdeCard-BusinessTech/fabric-skill)**. Com as duas instaladas, o Claude consulta o dicionário antes de escrever o SQL e acerta a tabela e o filtro de primeira.

## O que tem

| Assunto | Tabelas | Arquivo |
|---|---|---|
| Voll: atendimentos, TMA, TMF, TMR do robô, pausas, login/logout | `st_atendimento_voll*`, `st_pausas_voll`, `st_login_logout_voll` | [tabelas/voll.md](tabelas/voll.md) |
| SAC, canais críticos, avaliações, call center | `st_atendimento_criticos`, `dm_insights_clientes`, `st_ligacoes_contact_center` | [tabelas/sac-canais.md](tabelas/sac-canais.md) |
| Faturas | `st_faturas` | [tabelas/faturas.md](tabelas/faturas.md) |
| Base resumida de clientes | `st_bd_resumida` | [tabelas/clientes.md](tabelas/clientes.md) |
| Monitoria de ligações (PAS-0213) | `p0213_*` | [tabelas/monitoria.md](tabelas/monitoria.md) |

As regras de negócio mais usadas, como o filtro do número oficial do SAC, estão no [SKILL.md](SKILL.md#regras-de-negócio-mais-usadas).

## Instalação

Pré-requisito: o **Claude Code** (aba **Code** do app Claude no computador, ou `claude` no terminal). Veja o [Passo 0 da fabric-skill](https://github.com/VerdeCard-BusinessTech/fabric-skill#passo-0-abrir-o-claude-code) se nunca usou.

**Pedindo ao Claude** (cole no Claude Code):

```text
Instale a skill https://github.com/VerdeCard-BusinessTech/fabric-dicionario clonando em ~/.claude/skills/fabric-dicionario.
```

**Manual:**

```bash
git clone https://github.com/VerdeCard-BusinessTech/fabric-dicionario.git ~/.claude/skills/fabric-dicionario
```

No Windows (PowerShell): `git clone https://github.com/VerdeCard-BusinessTech/fabric-dicionario.git "$HOME\.claude\skills\fabric-dicionario"`

**Atualizar:** `git -C ~/.claude/skills/fabric-dicionario pull`

## Contribuindo

Para adicionar ou corrigir uma tabela, siga o [MODELO.md](MODELO.md). Você também pode pedir ao Claude: *"adicione a tabela X ao dicionário do Fabric"*.

**Este repositório é público:** registre estrutura e regras, nunca dados reais de clientes, senhas ou links de conexão.

## Origem

Baseado no documento interno *"Dicionário de Tabelas Fabric e Voll"*, conferido contra o Fabric:
- `bd_resumida` do documento é a `st_bd_resumida` no Fabric;
- a fórmula de TMA `d2/86400` foi traduzida para SQL (`/ 60.0` para minutos);
- a monitoria (`p0213_*`) foi adicionada a partir da estrutura real das tabelas.
