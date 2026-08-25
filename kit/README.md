# Estrutura Agêntica — Starter Kit

Kit reutilizável de governança para projetos conduzidos com agentes de IA
(Claude Code), destilado de um projeto real que passou por duas degradações de
processo e as fechou com estrutura executável. O princípio unificador:

> **Regra que vive só em prosa apodrece. Tudo que importa vira dado conferido
> por máquina: hooks que bloqueiam, stages que falham, manifestos que declaram.**

## O que é portátil (vem pronto no kit)

| Bloco | Conteúdo |
|---|---|
| `.claude/rules/` | R2–R14: evidência, TDD estrutural, máquina SDD de 7 fases, orquestração com contrato de 4 campos, boundary, determinismo, pins, modularidade, gates, entrada de evidência, documentação, decisões de projeto, git flow |
| `.claude/rules/product-invariants.template.md` | R1 como template — as invariantes são SEMPRE do produto; o kit só traz a regra-mãe e o formato |
| `.claude/agents/` | 8 papéis (PO, TL, UI, core, build, data, QA, doc) com as restrições estruturais preservadas e a especialidade de domínio em slots |
| `.claude/skills/` | new-demand (7 fases), fix-finding, spec-validate, verify, baseline |
| `.claude/templates/` | refinement, spec, plan, tasks, adr, planning-state.schema.json |
| `.claude/hooks/` | guard-boundary, guard-tdd, guard-data, state-eval, post-turn-verify + lib comum — todos parametrizados pelos manifestos, sem caminho de produto hardcoded |
| `.claude/verify/` | run.sh, compliance-audit.sh, gen_pins.py, checks de baseline/boundary/state/tdd, env_doctor, pipeline mínimo |
| `CLAUDE.template.md` / `CONTEXT.template.md` | índice de regras e glossário, com slots |
| `BOOTSTRAP.md` | o rito de instanciação em ondas — instale cada onda quando o projeto tiver a dor que ela fecha |

## O que cada projeto preenche (slots e manifestos)

- **Slots `{{ASSIM}}`** nos textos: `{{PRODUTO}}`, `{{MODULO_EXEMPLO}}`,
  `{{BUILDER}}`, `{{SUITE_EXEMPLO}}` etc. Busque por `{{` após copiar.
- **`.claude/verify/boundary.json`** — o que é protegido NESTE produto e o rito
  de mudança de cada classe (o kit entrega vazio, com `_meta` explicando).
- **`.claude/verify/expected_suites.json`** — as suítes e contagens verdes do
  produto (vazio no kit).
- **`.claude/verify/toolchain.json`** — a toolchain que o env-doctor valida.
- **`.claude/rules/product-invariants.md`** — escrito a partir do template,
  ratificado pelo proprietário; cada invariante com gate executável.
- **`pipeline.yaml`** — os stages do produto (build, suítes, lint) entram nos
  pontos comentados.

## Notas de rodapé "lição de origem"

Regras do kit carregam notas curtas `> Lição de origem:` — o erro real, no
projeto de origem, que fez a regra existir. Elas ficam para explicar o *porquê*;
apague-as se preferir o texto seco.

## Como instanciar

Siga o [`BOOTSTRAP.md`](BOOTSTRAP.md). Não instale tudo no dia 1.
