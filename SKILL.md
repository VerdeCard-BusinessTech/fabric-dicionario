---
name: fabric-dicionario
description: Dicionário das tabelas do Microsoft Fabric da Quero-Quero (Voll, SAC/canais críticos, contact center, faturas, base de clientes, monitoria PAS-0213). Explica o que cada tabela contém, onde ela está, as colunas e as regras de negócio (ex.: filtro do número oficial do SAC, TMA em segundos). Use quando o usuário perguntar o que é uma tabela, qual tabela usar para um assunto (TMA, TMF, pausas, reclamações, faturas, clientes, monitoria), o significado de colunas ou como filtrar atendimentos. Não precisa de conexão nem login. Use também antes de escrever SQL com a skill fabric-readonly.
---

# Dicionário de tabelas do Fabric

Conhecimento sobre as tabelas do Fabric: **o que são, onde estão, colunas e regras de negócio**. Esta skill não conecta em nada: só responde com base nos arquivos de `tabelas/`. Para rodar consultas, use a skill **fabric-readonly**.

## Como usar

1. Ache o assunto no índice abaixo e **leia só o arquivo correspondente** em `tabelas/`. Não carregue todos de uma vez.
2. Responda em linguagem simples: para que serve a tabela, onde está, as colunas relevantes para a pergunta e os avisos (⚠️).
3. Se a pessoa quiser os dados, passe para a skill **fabric-readonly**:
   - use os nomes **exatamente** como estão aqui;
   - aplique as regras de negócio do arquivo (filtros, unidades);
   - siga o "uso consciente" daquela skill: filtro de período e batch.
4. Tabela marcada como **"outro workspace do Fabric (link a confirmar)"**: ela existe no Fabric, mas fica num workspace que talvez ainda não esteja configurado. Para consultar, peça o link de conexão desse workspace (veja o guia da fabric-readonly) e configure um perfil novo. Quando descobrir o workspace, **atualize o campo "Onde"** do arquivo.
5. Se a pergunta não estiver coberta, diga isso claramente. **Não invente** o significado de colunas. Se a fabric-readonly estiver configurada, o `describe` mostra nomes e tipos reais.

## Índice

| Assunto | Tabela | Onde | Arquivo |
|---|---|---|---|
| Atendimentos Voll (compilado diário) | `st_atendimento_voll` | outro workspace | [tabelas/voll.md](tabelas/voll.md) |
| Tempo médio de atendimento (TMA) | `st_atendimento_voll_tma` | outro workspace | [tabelas/voll.md](tabelas/voll.md) |
| Tempo de fila (TMF), SLA, abandono | `st_atendimento_voll_tmf` | outro workspace | [tabelas/voll.md](tabelas/voll.md) |
| Tempo de resposta do robô (TMR) ⚠️ desatualizada | `st_atendimento_voll_tmr_robo` | outro workspace | [tabelas/voll.md](tabelas/voll.md) |
| Pausas de operadores | `st_pausas_voll` | outro workspace | [tabelas/voll.md](tabelas/voll.md) |
| Login/logout de operadores | `st_login_logout_voll` | outro workspace | [tabelas/voll.md](tabelas/voll.md) |
| Canais críticos (RDR, Reclame Aqui, SAC) | `st_atendimento_criticos` | outro workspace | [tabelas/sac-canais.md](tabelas/sac-canais.md) |
| Avaliações e insights de clientes | `dm_insights_clientes` | outro workspace | [tabelas/sac-canais.md](tabelas/sac-canais.md) |
| Ligações do call center | `st_ligacoes_contact_center` | outro workspace | [tabelas/sac-canais.md](tabelas/sac-canais.md) |
| Faturas | `st_faturas` | outro workspace | [tabelas/faturas.md](tabelas/faturas.md) |
| Base resumida de clientes | `st_bd_resumida` | `Neg_BT` | [tabelas/clientes.md](tabelas/clientes.md) |
| Monitoria de ligações (gravação, transcrição, notas, alertas) | `p0213_*` (16 tabelas) | `LAKE_BT` | [tabelas/monitoria.md](tabelas/monitoria.md) |

## Regras de negócio mais usadas

- **Número oficial do SAC:** `numero_entrada = '51986008186'`. Inclui robô, IA, televendas, call center de empréstimo e de cobrança (receptivo) e SAC. Para uma área específica, filtre por `campanha`.
- **Só o SAC:** `operador = 'Chatbot'` e `campanha = 'ATENDIMENTO'`.
- **Atendimentos internos** (Comuniq, Workplace, ChatQQ): coluna `sistema`.
- **Tempos em segundos** (`*_seg`). Minutos = `/ 60.0`. O chatbot tem TMR = 0.
- `st_atendimento_criticos` é preenchida **manualmente** e pode ter erros. `dm_insights_clientes` replica parte dela.

## Mantendo o dicionário

Quando a pessoa pedir para **adicionar ou corrigir** uma tabela:
- edite o arquivo do assunto em `tabelas/`, ou crie um novo seguindo [MODELO.md](MODELO.md);
- atualize o índice acima.

Se a fabric-readonly estiver configurada, confira nomes e tipos com `describe` antes de registrar. **Este repositório é público:** registre estrutura e regras, nunca dados reais de clientes, senhas ou links de conexão.
