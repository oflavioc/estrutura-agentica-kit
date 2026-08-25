---
name: baseline
description: Valida rapidamente a integridade do baseline (pins × HEAD, boundary) e orienta o que fazer em divergência. Use antes de começar trabalho e sempre que o state-eval acusar divergência.
---

# Baseline

```bash
bash .claude/verify/run.sh --stage=baseline   # pins × blobs de HEAD
bash .claude/verify/run.sh --stage=boundary   # protegidos coerentes
# {{quando o produto tiver build determinístico:}}
# bash .claude/verify/run.sh --stage=build    # rebuild byte-idêntico
```

## Leitura dos resultados

- **Tudo verde** → o repositório é ele mesmo; trabalhe.
- **baseline FAIL "pin diverge"** → alguém alterou arquivo pinado sem repin.
  Mudança sua e legítima → `python .claude/verify/gen_pins.py` + commit próprio
  com motivo (R8). Não é sua → **não toque**: reporte ao usuário com o diff.
- **baseline FAIL "sem pin"** → arquivo novo rastreado; regenerar o registry no
  mesmo PR que o introduziu.
- **boundary FAIL** → protegido divergiu SEM rito: isso é incidente, não tarefa.
  Parar e reportar ao usuário com a classe e o rito exigido.
- **build FAIL** → decidir a direção ANTES de agir: fonte mudou de propósito
  (rebuild consciente + repin) ou o gerado foi editado à mão (reverter o gerado).

## Âncoras (fonte: pins.json, nunca prosa)

- `declared.{{ANCORA_DE_GOVERNANCA}}` — {{ex.: a régua objetiva da superfície
  congelada (R1)}}.
- Hash medido só vale sobre blob/árvore LF (R2 §2).
