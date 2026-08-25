# R6 — Change boundary

Severidade: **bloqueante** (hook `guard-boundary` + stage `boundary` +
`permissions.deny`).

A boundary é **dado, não prosa**: `.claude/verify/boundary.json` declara as
classes de proteção e o rito que autoriza mudança em cada uma.

> Lição de origem: uma seção de spec em prosa "proibia" editar superfícies
> congeladas — e elas foram editadas em duas fases seguidas. Regra em prosa não
> segurou; o hook segura.

| Classe | Conteúdo típico | Rito de mudança |
|---|---|---|
| `frozen` | {{SUPERFICIE_CONGELADA — ex.: o núcleo validado de {{PRODUTO}}, snapshots funcionais}} | a porta definida na R1 (régua objetiva) |
| `generated` | {{ARTEFATOS_GERADOS — saída de {{BUILDER}}}} | só via gerador; o stage `build` prova identidade |
| `legacy` | {{ARTEFATOS_APOSENTADOS}} | congelado até reconciliação formal |
| `registry` | `pins.json` | só via `gen_pins.py`, no mesmo PR, com motivo no commit |

## Regras

1. Edição direta de path protegido é **negada pelo hook** com o rito nomeado.
2. `permissions.deny` espelha o boundary (Edit+Write) — o `compliance-audit`
   (seção `deny`) falha se divergirem.
3. **Expansão de boundary só por spec commitada ANTES do código** — nunca por
   autorização registrada só em prosa de relatório.
4. Quando uma fase é **selada**, sua boundary fecha para sempre: os módulos da
   fase entram no conjunto protegido da fase seguinte (freeze acumulativo).
5. Correção que exigir arquivo protegido: **PARAR, explicar o rito, aguardar**
   a autorização do usuário no chat.
