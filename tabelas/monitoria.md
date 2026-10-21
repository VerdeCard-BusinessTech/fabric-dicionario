# Monitoria de qualidade (projeto PAS-0213)

Monitoria de ligações com IA: gravações, transcrições, avaliações por formulário e alertas.

- **Onde:** Lakehouse `LAKE_BT` (mesmo workspace e mesmo link do `Neg_BT`), tabelas `dbo.p0213_*`.
- **Caminho principal:** `p0213_audio_recording.hash_audio` → `p0213_form_response.audio_hash` → `p0213_field_response.form_response_id` → `p0213_model_field.id` (via `model_field_id`).
- Outras ligações: `form_response.model_form_id` → `model_form.id`; `model_module.model_form_id` → `model_form.id`; `model_field.model_module_id` → `model_module.id`; `audio_recording.operator_id` → `operator.id`; `audio_recording.workgroup_id` → `workgroup.id`; `transcription.hash_audio` e `audio_metadata.hash_audio` → `audio_recording.hash_audio`; `alerts.model_alert_id` → `model_alert.id`.
- Para relatórios por operador/equipe **na data da avaliação**, use as colunas `*_snapshot` de `p0213_form_response` (guardam o operador, a equipe e o monitor como eram naquele momento).
- Descrições inferidas da estrutura das tabelas; confirme regras de negócio com o time do projeto.

## `p0213_alerts`

Alertas disparados em cada ligação.

**Colunas:** `id` (bigint), `model_alert_id` (bigint), `audio_hash` (varchar), `detail` (varchar), `dt_atu` (datetime2)

## `p0213_audio_metadata`

Resumo da ligação gerado por IA, tabulação sugerida pela IA x tabulação do operador (com justificativa) e tokens usados.

**Colunas:** `id` (bigint), `hash_audio` (varchar), `summary` (varchar), `tabulation_ai_id` (bigint), `tabulation_op_id` (bigint), `total_tokens` (bigint), `tabulation_ai_justification` (varchar), `input_tokens` (bigint), `output_tokens` (bigint), `dt_atu` (datetime2), `dt_created` (datetime2)

## `p0213_audio_metadata_kv`

Campos extras extraídos de cada ligação (chave/valor).

**Colunas:** `id` (bigint), `id_metadata` (bigint), `field_name` (varchar), `field_value` (varchar), `dt_atu` (datetime2), `dt_created` (datetime2)

## `p0213_audio_recording`

Gravações das ligações: link do áudio, duração, telefone, conta do cliente, operador, grupo e data/hora. Chave: `hash_audio`.

**Colunas:** `hash_audio` (varchar), `url_audio` (varchar), `duration` (bigint), `phone` (varchar), `workgroup_id` (bigint), `id` (bigint), `dt_atu` (datetime2), `call_timestamp` (datetime2), `dt_created` (datetime2), `client_account` (bigint), `operator_id` (bigint)

## `p0213_client`

Clientes das ligações (conta, nome, CPF/CNPJ). Sensível.

**Colunas:** `account` (bigint), `name` (varchar), `cpf_cnpj` (varchar), `id` (bigint), `dt_atu` (datetime2)

## `p0213_field_response`

Nota de cada item avaliado: motivo, se foi o robô, se o item se aplicava e se a avaliação estava correta.

**Colunas:** `id` (bigint), `model_field_id` (bigint), `form_response_id` (bigint), `score` (bigint), `reason` (varchar), `robot` (bit), `applicable` (bit), `dt_atu` (datetime2), `dt_cri` (datetime2), `matricula` (int), `is_correct` (bit)

## `p0213_form_response`

Uma avaliação (monitoria) por ligação: nota total, formulário, avaliador, origem e fotografia do operador, equipe, monitor e datas no momento da avaliação.

**Colunas:** `id` (bigint), `model_form_id` (bigint), `audio_hash` (varchar), `total_tokens` (bigint), `input_tokens` (bigint), `output_tokens` (bigint), `score` (bigint), `public_id` (varchar), `dt_atu` (datetime2), `dt_cri` (datetime2), `tabulation_id` (int), `origin` (varchar), `evaluator_id` (varchar), `operator_snapshot` (varchar), `operator_enrollment_snapshot` (varchar), `team_snapshot` (varchar), `monitor_snapshot` (varchar), `tabulation_snapshot` (varchar), `call_datetime_snapshot` (datetime2), `monitoring_datetime_snapshot` (datetime2), `suggestion` (varchar)

## `p0213_model_alert`

Regras de alerta (prompt, grupo, ativo).

**Colunas:** `id` (bigint), `name` (varchar), `description` (varchar), `prompt` (varchar), `workgroup` (bigint), `active` (bit), `dt_atu` (datetime2)

## `p0213_model_field`

Itens avaliados em cada seção, com prompt e peso da nota.

**Colunas:** `id` (bigint), `model_module_id` (bigint), `name` (varchar), `description` (varchar), `prompt` (varchar), `score` (bigint), `dt_atu` (datetime2), `dt_cri` (datetime2)

## `p0213_model_form`

Formulários de monitoria (versão, prompt, grupo, ativo).

**Colunas:** `id` (bigint), `name` (varchar), `description` (varchar), `prompt` (varchar), `version` (varchar), `workgroup_id` (bigint), `active` (bit), `dt_atu` (datetime2), `dt_cri` (datetime2)

## `p0213_model_metadata_kv`

Definição dos campos extras por grupo.

**Colunas:** `id` (bigint), `workgroup_id` (int), `name` (varchar), `description` (varchar), `active` (bit), `type` (varchar), `dt_atu` (datetime2), `dt_created` (datetime2)

## `p0213_model_module`

Seções de cada formulário.

**Colunas:** `id` (bigint), `model_form_id` (bigint), `name` (varchar), `description` (int), `prompt` (varchar), `dt_atu` (datetime2), `dt_cri` (datetime2)

## `p0213_operator`

Operadores (nome, matrícula, grupo).

**Colunas:** `id` (bigint), `name` (varchar), `matricula` (varchar), `dt_atu` (datetime2), `workgroup` (varchar)

## `p0213_tabulation`

Tabulações por grupo.

**Colunas:** `id` (bigint), `workgroup_id` (bigint), `name` (varchar), `description` (varchar), `active` (bit), `dt_atu` (datetime2), `dt_created` (datetime2)

## `p0213_transcription`

Transcrição das ligações: falas, quem falou (`is_client`) e tempo de cada trecho.

**Colunas:** `id` (bigint), `hash_audio` (varchar), `is_client` (bit), `speech` (varchar), `dt_atu` (datetime2), `dt_created` (datetime2), `start_time` (varchar), `end_time` (varchar)

## `p0213_workgroup`

Grupos/equipes (com hierarquia via `parent_id`).

**Colunas:** `id` (bigint), `name` (varchar), `description` (varchar), `company` (varchar), `dt_atu` (datetime2), `dt_created` (datetime2), `parent_id` (int)
