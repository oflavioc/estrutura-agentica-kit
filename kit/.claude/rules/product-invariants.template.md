# R1 — Invariantes de produto (TEMPLATE)

> **Instruções de preenchimento** (apague este bloco ao instanciar):
> 1. Renomeie para `product-invariants.md`.
> 2. Liste de 5 a 12 proposições que SÃO o produto — o que, violado, faz o
>    produto deixar de ser ele mesmo. Não liste desejos nem qualidades ("rápido",
>    "bonito"): liste proposições falsificáveis.
> 3. Para CADA invariante, nomeie o gate executável que a verifica e registre o
>    mapa em `.claude/verify/invariants.json` (o `compliance-audit`, seção
>    `invariantes`, falha se o mapa quebrar ou se o gate não existir).
> 4. Invariante nova ou alterada: o `product-owner` propõe, **só o proprietário
>    humano ratifica**. Até a ratificação, marque `PROPOSTA`.
> 5. Se existir uma superfície congelada cuja mudança exige rito especial,
>    defina aqui a régua OBJETIVA que separa mudança de equivalência de mudança
>    de comportamento (no projeto de origem: o SHA-256 de um payload funcional
>    canonicalizado — payload idêntico = porta leve; diferente = porta pesada).

Severidade: **bloqueante**. Dono: `product-owner`. Só o PO propõe mudança de
invariante, e só o proprietário humano a ratifica.

**A regra-mãe: invariante sem gate é prosa.** Cada linha da tabela tem um gate
executável mapeado em `.claude/verify/invariants.json`.

| # | Invariante | Gate |
|---|---|---|
| INV-1 | {{PROPOSICAO_CENTRAL_DO_PRODUTO}} | {{GATE_EXECUTAVEL}} |
| INV-2 | {{...}} | {{...}} |

## Régua de mudança da superfície congelada (se houver)

{{REGUA_OBJETIVA — o critério mecânico, nunca opinião, que decide qual rito
uma mudança na superfície congelada exige. Apague a seção se não se aplicar.}}
