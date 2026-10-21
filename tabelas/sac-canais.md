# SAC, canais críticos e contact center

Reclamações dos canais críticos (RDR, Reclame Aqui, SAC), avaliações de clientes e ligações do call center.

Dados pessoais (CPF, nome, telefone, e-mail, conta) são sensíveis: em respostas, prefira agregados e amostras.

## `st_atendimento_criticos`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz informações sobre os atendimentos dos canais críticos da empresa (RDR, Reclame aqui, reclamações sac)
- Essa tabela contempla atendimentos realizados pelo sac área de canais críticos, onde o preenchimento é feito de forma manual, podendo haver erros.

**Colunas (62):** `carimbo_data_hora`, `matricula`, `nome_reclamante`, `cpf_reclamante`, `cta_reclamante`, `email_reclamante`, `motivo_de_atendimento`, `data_e_hora_reclamacao`, `relato_do_cliente`, `data_e_hora_de_retorno`, `tipo_de_retorno`, `resposta_final_ao_cliente`, `canal_de_atendimento`, `subcanal`, `status_do_atendimento`, `id_chamado`, `pedido_vtex`, `produto`, `valor`, `assunto`, `categoria`, `area_responsavel`, `responsavel_pela_entrega`, `pedido_cliqq`, `data_prometida_entrega`, `data_entrega`, `pedido_cancelado`, `filial`, `historico_de_contato`, `solucao`, `resumo_solucao`, `custo_solucao`, `procedente_e_improcedente`, `origem_do_problema`, `feeling_satisfacao`, `cpf_titular`, `cta_titular`, `reclamacao_ctt_terceiro_fone`, `reclamacao_ctt_terceiro_email`, `obs`, `tmr`, `mes`, `dia`, `dh_atu`, `cd_usu_atu`, `ip_usu_atu`, `data_e_hora_envio_area`, `data_e_hora_ultimo_retorno_area`, `avaliou`, `data_avaliacao`, `foi_resolvido`, `voltaria_a_fazer_negocio`, `nota`, `comentario_avaliacao`, `sheet_id`, `tabulacao_antiga`, `categoria_antiga`, `resumo_relato`, `justificativa_bcb`, `data_ranking`, `acao`, `ano`

## `dm_insights_clientes`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz as informações de canais de atendimento com as avaliações feitas pelos clientes.
- Essa tabela contempla canais de atendimento e de avaliações. Ela replica algumas informações da tabela st_atendimento_criticos.

**Colunas (26):** `canal_de_atendimento`, `nome_cliente`, `cpf`, `nota`, `relato`, `data_relato`, `pedido`, `pedido_vtex`, `sku`, `valor_total_pedido`, `filial`, `data_do_pedido`, `responsavel_pela_entrega`, `categoria_humano`, `motivo_humano`, `assunto_humano`, `categoria`, `motivo`, `assunto`, `key_hash`, `business_hash`, `meta_id`, `dh_atu`, `created_atu`, `cd_usu_atu`, `ip_usu_atu`

## `st_ligacoes_contact_center`

- **Onde:** outro workspace do Fabric (link a confirmar)
- **Objetivo:** Traz as informações sobre as ligações feitas no call center da empresa.

**Colunas (25):** `data_hora_ligacao`, `telefone`, `agente`, `qualificacao`, `forma_contato`, `campanha_mestre`, `campanha_escrava`, `identificador_mailing`, `discador`, `observacao`, `data_hora_agendada`, `extracao_manual`, `id_conta`, `conexao`, `ring`, `cpf_contato`, `duracao`, `status`, `aguardo_atendimento`, `nota`, `side_hungup`, `dnis`, `dh_atu`, `cd_usu_atu`, `ip_usu_atu`
