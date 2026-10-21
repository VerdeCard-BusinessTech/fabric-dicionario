# Clientes (base resumida)

Cadastro resumido de clientes: dados pessoais, endereço, contato, limites, bloqueios e datas de compra.

Dados pessoais (CPF, nome, telefone, e-mail, conta) são sensíveis: em respostas, prefira agregados e amostras.

## `st_bd_resumida`

- **Onde:** Lakehouse `Neg_BT` → `dbo.st_bd_resumida`
- **Objetivo:** Traz as informações sobre clientes da empresa.
- ⚠️ No documento original aparece como `bd_resumida`; no Fabric o nome é **`st_bd_resumida`**.
- ⚠️ Os nomes de coluna são abreviados e alguns têm grafia própria (ex.: `cpfcnjp`). Use exatamente como na lista abaixo.
- ⚠️ Colunas `blcta*` parecem ser marcações de bloqueio de conta por tipo, mas o significado de cada sigla ainda não está documentado. Confirme antes de usar.

<details><summary>123 colunas (nomes e tipos conferidos no Fabric)</summary>

| # | coluna | tipo |
|---|---|---|
| 1 | `cta` | bigint |
| 2 | `cpfcnjp` | varchar |
| 3 | `fisjur` | varchar |
| 4 | `nomerazao` | varchar |
| 5 | `dtnascdtfund` | date |
| 6 | `nac` | varchar |
| 7 | `sexo` | varchar |
| 8 | `atpri` | varchar |
| 9 | `escolaridade` | int |
| 10 | `ufres` | varchar |
| 11 | `cidres` | varchar |
| 12 | `cepres` | int |
| 13 | `baires` | varchar |
| 14 | `tplogres` | varchar |
| 15 | `logres` | varchar |
| 16 | `nlogres` | varchar |
| 17 | `clogres` | varchar |
| 18 | `ufcom` | varchar |
| 19 | `cidcom` | varchar |
| 20 | `cepcom` | int |
| 21 | `baicom` | varchar |
| 22 | `tplogcom` | varchar |
| 23 | `nmlogcom` | varchar |
| 24 | `nlogcom` | varchar |
| 25 | `clogcom` | varchar |
| 26 | `dffix` | int |
| 27 | `ffix` | bigint |
| 28 | `dfcel` | int |
| 29 | `fcel` | bigint |
| 30 | `dcom` | int |
| 31 | `fcom` | bigint |
| 32 | `ljcta` | int |
| 33 | `ljcad` | int |
| 34 | `id_tp_cap` | varchar |
| 35 | `id_aca_cap` | varchar |
| 36 | `dt_ger_cd_cc` | date |
| 37 | `dt_abe_cd_cc` | date |
| 38 | `status` | varchar |
| 39 | `rcli` | decimal |
| 40 | `dt_re` | date |
| 41 | `lim_gbl` | decimal |
| 42 | `lim_disp` | decimal |
| 43 | `lim_ep` | decimal |
| 44 | `lim_disp_ep` | decimal |
| 45 | `cd_mda` | int |
| 46 | `cd_mda_ant` | int |
| 47 | `vr_hist_cmp_ant` | decimal |
| 48 | `vr_hist_cmp` | decimal |
| 49 | `bloq_rel` | varchar |
| 50 | `bloq_crm` | varchar |
| 51 | `blctabg` | varchar |
| 52 | `blctabb` | varchar |
| 53 | `blctaba` | varchar |
| 54 | `blctabm` | varchar |
| 55 | `blctabs` | varchar |
| 56 | `blctabc` | varchar |
| 57 | `blctabp` | varchar |
| 58 | `blctabj` | varchar |
| 59 | `blctacp` | varchar |
| 60 | `blctalp` | varchar |
| 61 | `blctabd` | varchar |
| 62 | `blctadg` | varchar |
| 63 | `blctaac` | varchar |
| 64 | `blctaca` | varchar |
| 65 | `blctacc` | varchar |
| 66 | `blctacf` | varchar |
| 67 | `blctaci` | varchar |
| 68 | `blctacn` | varchar |
| 69 | `blctacr` | varchar |
| 70 | `blctacs` | varchar |
| 71 | `blctabl` | varchar |
| 72 | `blctarc` | varchar |
| 73 | `blctada` | varchar |
| 74 | `blctamf` | varchar |
| 75 | `blctarl` | varchar |
| 76 | `blctabk` | varchar |
| 77 | `blctaap` | varchar |
| 78 | `hab_qqpag` | varchar |
| 79 | `blctasc` | varchar |
| 80 | `dt_ult_com_merc` | date |
| 81 | `dt_ult_com_multi` | date |
| 82 | `dt_ult_com_ep` | date |
| 83 | `matricula_colab` | int |
| 84 | `cartao_ativo` | int |
| 85 | `sg_med` | varchar |
| 86 | `rkg1` | decimal |
| 87 | `rkg5` | decimal |
| 88 | `email` | varchar |
| 89 | `cd_emp` | int |
| 90 | `nr_cic_eg` | int |
| 91 | `dt_pri_cmp_qq` | date |
| 92 | `dt_pri_cmp_af` | date |
| 93 | `dt_pri_ep` | date |
| 94 | `dt_pri_rn` | date |
| 95 | `dt_ult_ep` | date |
| 96 | `dt_ult_cmp_qq` | date |
| 97 | `dt_ult_cmp_af` | date |
| 98 | `dt_ult_rn` | date |
| 99 | `blctact` | varchar |
| 100 | `blctami` | varchar |
| 101 | `blctavt` | varchar |
| 102 | `blctabn` | varchar |
| 103 | `catpro` | varchar |
| 104 | `func_cartao` | varchar |
| 105 | `sg_sco` | varchar |
| 106 | `dt_ult_mod_renda` | date |
| 107 | `dt_ult_cad_compl` | date |
| 108 | `diafat` | int |
| 109 | `id_verdecob` | int |
| 110 | `saldo_conta_digital` | varchar |
| 111 | `dt_ult_mov` | date |
| 112 | `blctafd` | varchar |
| 113 | `dt_ult_acesso_app` | date |
| 114 | `id_rcb_fat_email` | varchar |
| 115 | `id_rcb_fat_cel` | varchar |
| 116 | `vr_glb_ext` | decimal |
| 117 | `vr_glb_ext_disp` | decimal |
| 118 | `apto_compra` | varchar |
| 119 | `apto_ep` | varchar |
| 120 | `dh_atu` | datetime2 |
| 121 | `lim_sug` | bigint |
| 122 | `ren_res` | bigint |
| 123 | `grupo_ep` | varchar |

</details>
