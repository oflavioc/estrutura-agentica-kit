# BOOTSTRAP — o rito de instanciação em ondas

O kit não se instala inteiro no dia 1. **Cada onda entra QUANDO o projeto tem a
dor que ela fecha** — instalar governança antes da dor produz burocracia sem
adesão; instalar depois demais produz as degradações que o projeto de origem
viveu (fases sem spec, selagens inauditáveis, hooks soltos e desligados).
A sequência abaixo é fiel à história real do projeto de origem.

## Onda 0 — Determinismo e identidade (dia 1, sempre)

*Dor que fecha: "o repositório não é ele mesmo" — hashes que divergem por
plataforma, arquivos protegidos editados sem ninguém ver, contexto de sessão
sem estado real.*

1. **`.gitattributes`** com `* text=auto eol=lf` (e `-text` para binários/CRLF
   pinado byte a byte). Renormalizar: `git add --renormalize .` + commit.
2. Copiar `kit/.claude/` para o projeto; preencher os slots `{{...}}` de
   `boundary.json` (classes + `produto.globs` vazio + `dados`), `toolchain.json`.
3. **Semear os pins**: `python .claude/verify/gen_pins.py` (árvore limpa!) +
   commit próprio.
4. **CLAUDE.md índice** a partir de `CLAUDE.template.md` (aponta, não repete) +
   `CONTEXT.md` a partir do template, com os primeiros termos do domínio.
5. `settings.json` com os hooks registrados; espelhar o boundary em
   `permissions.deny`.
6. Prova de pronto: `bash .claude/verify/run.sh --stage=baseline` verde e
   `bash .claude/verify/compliance-audit.sh` sem FAIL inesperado.

## Onda 1 — Pipeline e CI

*Dor que fecha: verificação manual, esquecível e não-agregada; "funciona na
minha máquina".*

1. `pipeline.yaml`: manter os 5 stages mínimos e adicionar os stages do
   produto (build determinístico, suítes) nos pontos comentados.
2. `expected_suites.json`: registrar as suítes existentes com contagens reais.
3. CI ({{ex.: GitHub Actions}}) rodando `run.sh` em cada PR — a plataforma do
   CI é a canônica (R7 §5).
4. Prova de pronto: pipeline completo verde local E no CI.

## Onda 2 — Agentes e SDD (na primeira demanda real)

*Dor que fecha: demandas que começam pela implementação; critérios de aceite
implícitos; um só "agente faz-tudo" sem separação de poderes.*

1. Instanciar os 8 agentes (preencher os slots de domínio de cada um).
2. Conduzir a PRIMEIRA demanda nova inteira pela skill `new-demand` — as 7
   fases, com aprovação literal do usuário em cada portão. Não instale a
   máquina "no vazio": instale-a resolvendo uma demanda de verdade.
3. planning-state + stage `state` ativos (já vêm no pipeline mínimo).
4. Prova de pronto: primeira demanda com refinement/spec/plan/tasks/red
   commitados e PR aberto.

## Onda 3 — TDD endurecido

*Dor que fecha: red "de mentira" (nunca executado), gates sem poder
discriminante, disciplina que depende de lembrar.*

1. Ativar o `guard-tdd`: preencher `boundary.json → produto.globs` com os
   padrões dos módulos de produto. A partir daqui, editar produto sem red
   provado É bloqueado.
2. Instalar a matriz gate↔mutante (`mutation-matrix.json`) e a campanha de
   mutação por trigger de path no pipeline (stage `mutation`, heavy).
3. Prova de pronto: stage `tdd` validando red.commit real; um mutante morto
   por gate novo.

## Onda 4 — Boundary acumulativa e reconciliações

*Dor que fecha: superfícies "prontas" que continuam mudando; legado ambíguo
(manifestos velhos, evidência binária no git, docs fora de versão).*

1. A cada selagem, **fechar a boundary da fase**: módulos selados entram em
   `frozen`/`generated` no boundary.json + `permissions.deny`.
2. Reconciliar legados: aposentar manifestos antigos (classe `legacy`), migrar
   evidência binária para o evidence store com manifesto-ponte (R11), pinar
   docs de governança que estavam fora do git.
3. Prova de pronto: `compliance-audit.sh` inteiro verde, incluindo deny ×
   boundary; nenhum artefato de identidade fora do registry.

## Regra de ouro

Se uma onda não tem dor correspondente ainda, **não a instale** — registre no
CLAUDE.md que ela está pendente e qual sinal dispara a instalação. Estrutura
sem dor vira teatro; a auditoria (`compliance-audit.sh`) só protege o que o
projeto de fato usa.
