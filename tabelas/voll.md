# Voll: atendimentos, tempos e operadores

Tabelas da plataforma de atendimento Voll (chat/telefonia): atendimentos, TMA, TMF, TMR do robô, pausas e login/logout.

Dados pessoais (CPF, nome, telefone, e-mail, conta) são sensíveis: em respostas, prefira agregados e amostras.

## `st_atendimento_voll`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz o compilado de informações sobre os atendimentos diários da Voll.

**Colunas (36):** `id`, `cliente`, `sistema`, `telefone`, `cpf`, `cnpj`, `campanha`, `operador`, `tabulacao`, `inicio`, `fim`, `inicio_cliente`, `inicio_agente`, `maior_estouro_seg`, `tempo_total_seg`, `qtd_enviada`, `qtd_recebida`, `qtd_mensagens`, `observacoes`, `tipo_atendimento`, `tmr_operador_seg`, `tmr_cliente_seg`, `dh_atu`, `cd_usu_atu`, `ip_usu_atu`, `protocolo`, `numero_entrada`, `status`, `direcao`, `grupo_tabulacao`, `identificador_externo`, `pesquisa`, `pergunta_1`, `resposta_1`, `pergunta_2`, `resposta_2`

## `st_atendimento_voll_tma`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz o Tempo Médio de Atendimento dos operadores Voll.
- ⚠️ Diferente do relatório Voll do diretório, a tabela tem só uma coluna de TMA, em segundos.
- ⚠️ `tma_seg` está em segundos. Minutos: `tma_seg / 60.0` (a fórmula `d2/86400` do documento original é do Excel e converte para fração de dia).

**Colunas (8):** `operador`, `data`, `tma_seg`, `campanha`, `quantidade`, `dh_atu`, `cd_usu_atu`, `ip_usu_atu`

## `st_atendimento_voll_tmf`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz o tempo de fila sobre os atendimentos diários da Voll.

**Colunas (14):** `id`, `cliente`, `telefone`, `campanha`, `data_inicio`, `data_fim`, `espera_seg`, `sla_alerta`, `sla_limite`, `tempo_restante_seg`, `abandono`, `dh_atu`, `cd_usu_atu`, `ip_usu_atu`

## `st_atendimento_voll_tmr_robo`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz o tempo médio de resposta do robô (Chatbot).
- ⚠️ está com os dados sem atualização.

**Colunas (7):** `data`, `operador`, `tmr_seg`, `sistema`, `dh_atu`, `cd_usu_atu`, `ip_usu_atu`

## `st_pausas_voll`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz os tempos de pausa dos operadores/ campanhas da Voll.

**Colunas (9):** `nome`, `campanha`, `pausa`, `inicio`, `fim`, `duracao_pausa`, `duracao_operacao`, `dh_atu`, `cd_usu_atu`

## `st_login_logout_voll`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz o horário de login e logout dos operadores.

**Colunas (8):** `login`, `nome`, `campanha`, `supervisor`, `inicio`, `fim`, `dh_atu`, `cd_usu_atu`

## Regras de negócio para atendimentos

- **Tudo que passa pelo número oficial do SAC:** filtre `numero_entrada = '51986008186'`. Isso traz robô, IA, televendas, call center de empréstimo (receptivo), call center de cobrança (receptivo) e SAC.
  - Para uma área específica dentro desse número, filtre também por `campanha`.
- **Só o SAC:** `operador = 'Chatbot'` e `campanha = 'ATENDIMENTO'`.
- **Atendimentos internos** (Comuniq, Workplace, ChatQQ): use a coluna `sistema`.
- **Um suporte específico:** use `numero_entrada`.
- **O chatbot tem TMR = 0**, porque responde na hora. Exclua o chatbot ao calcular TMR de operadores humanos.
- Tempos estão em **segundos** (`*_seg`). Em SQL: minutos = `tma_seg / 60.0`. No Excel, `=D2/86400` formatado como hora mostra hh:mm:ss.
