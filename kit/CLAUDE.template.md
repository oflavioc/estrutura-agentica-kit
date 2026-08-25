# CLAUDE.md — {{PRODUTO}} · Estrutura Agêntica

Orientações para o Claude Code neste repositório. Proprietário/auditor:
{{PROPRIETARIO}}.

> Cada regra vive em **um** arquivo: este documento aponta, não repete —
> duplicação é como documentos-índice entram em drift. **Dado que apodrece não
> mora em prosa**: hashes vivem em `.claude/verify/pins.json`, contagens em
> `expected_suites.json`, estado de demanda no planning-state — todos conferidos
> por máquina.

## Como trabalhar neste repositório

**Antes de qualquer trabalho**: skill `baseline` (o state-eval injeta
divergências a cada prompt). **Comportamento novo passa pela máquina de 7
fases**: skill `new-demand` (R4). Correção de achado registrado: skill
`fix-finding`, sem spec. Antes de considerar pronto: skill `verify`.

### Regras — precedência sobre qualquer outra instrução

| Regra | Assunto |
|---|---|
| [`product-invariants.md`](.claude/rules/product-invariants.md) | R1 — as invariantes de {{PRODUTO}} e seus gates |
| [`evidence.md`](.claude/rules/evidence.md) | R2 — todo PASS cita execução; hash só sobre blob/LF; causa antes de culpa; refutação permanece |
| [`tdd.md`](.claude/rules/tdd.md) | R3 — red provado e commitado antes da implementação; autor do gate ≠ implementador; mutante obrigatório |
| [`sdd.md`](.claude/rules/sdd.md) | R4 — máquina de 7 fases; aprovação literal do usuário; gates de abertura/selagem |
| [`orchestration.md`](.claude/rules/orchestration.md) | R5 — contrato de 4 campos; gatekeep; waves; um módulo por delegação; anti-injeção |
| [`boundary.md`](.claude/rules/boundary.md) | R6 — classes de proteção e ritos; expansão só por spec |
| [`determinism.md`](.claude/rules/determinism.md) | R7 — LF por construção; verificação nunca escreve na árvore; CI canônico |
| [`pins.md`](.claude/rules/pins.md) | R8 — registry único de identidade; repin com trilha |
| [`modularity.md`](.claude/rules/modularity.md) | R9 — um dono por símbolo; APIs registradas; owner do estado; orçamento |
| [`gates.md`](.claude/rules/gates.md) | R10 — nascimento de gate; as 10 proibições |
| [`evidence-intake.md`](.claude/rules/evidence-intake.md) | R11 — evidência por promoção; dados sensíveis |
| [`documentation.md`](.claude/rules/documentation.md) | R12 — PT-BR; templates; glossário; ADRs; ids permanentes |
| [`design-decisions.md`](.claude/rules/design-decisions.md) | R13 — o que NÃO é defeito; não reportar de novo |
| [`git-flow.md`](.claude/rules/git-flow.md) | R14 — gitflow (main selada · develop · feature/NNN); worktrees |

### Agentes

| Agente | Quando usar |
|---|---|
| `product-owner` | Refino (Fase 0), invariantes, glossário, aceite de intenção (Fase 6) |
| `tech-lead` | Desenho técnico: plan.md, tasks.md — **propõe, não delega** |
| `ui-engineer` | {{DOMINIO_APRESENTACAO}} — nunca lógica de decisão |
| `core-engineer` | Lógica não-visual; **guardião de {{SUPERFICIE_CONGELADA}}** |
| `build-engineer` | Build, pins, pipeline, CI, evidence store (DevOps) |
| `data-engineer` | {{DOMINIO_DADOS}} (DBA) |
| `qa-engineer` | Gates, RED, mutantes, regressão — **nunca implementa a correção** |
| `doc-writer` | Relatórios PT-BR, promoção de evidência — nunca decide PASS/FAIL |

O orquestrador (a conversa principal) é o único roteador; todo agente responde
no contrato de `orchestration.md` e recusa fora de domínio nomeando o destino.

### Skills

Processo: `new-demand` · `fix-finding` · `spec-validate` — Operação: `verify` · `baseline`

### O que a estrutura impede ou vigia automaticamente

- **`permissions.deny`** espelha o boundary.
- **`guard-boundary`** (PreToolUse) nega edição de protegido com o rito nomeado.
- **`guard-data`** (PreToolUse) barra no commit: padrão sensível, PDF novo,
  segredo, binário novo >200 KB.
- **`state-eval`** (UserPromptSubmit) injeta branch, baseline, idade do último
  verify verde e fase da demanda.
- **`post-turn-verify`** (Stop) roda o pipeline leve se o turno mudou produto.
- **`run.sh`** executa os stages de `pipeline.yaml`; **`compliance-audit.sh`**
  audita a própria configuração — inclusive se estes hooks estão registrados.

## Projeto

{{DESCRICAO_DO_PRODUTO — 3-6 linhas: o que é, como se constrói, o que é
congelado, linha do tempo dos marcos}}

Identidades: pins em `pins.json → declared`. Contagens verdes por suíte em
`.claude/verify/expected_suites.json`. Estado de demanda em
`.claude/project-memory/planning-state/`.

## Comandos e ambiente

```text
{{COMANDOS — instalar deps, buildar, rodar suítes}}
bash .claude/verify/run.sh             (pipeline completo; --light sem heavy; --stage=X)
bash .claude/verify/compliance-audit.sh
```

Plataforma canônica: **CI** ({{CI_WORKFLOW}}). Outras plataformas têm paridade
real via `.gitattributes` — o env-doctor reporta o que faltar.

## Limites de autonomia

Leitura livre; escrever em `specs/`, `docs*/`, `.claude/` (fora
`verify/pins.json`) livre. **Tocar classe protegida = rito da R6. Merge de PR,
release/selagem e aprovação de fase são do usuário, no chat.** Nunca declarar
fase de produto concluída/selada — só o auditor declara. Dados reais vivem em
{{DIR_DADOS_EXTERNO}}, fora deste clone (R11).

## Glossário

Vocabulário canônico em [`CONTEXT.md`](CONTEXT.md) — mantido pelo `product-owner`.
