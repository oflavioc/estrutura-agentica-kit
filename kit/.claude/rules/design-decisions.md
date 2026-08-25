# R13 — Decisões de projeto que não são defeitos

**Não reportar como achado, não "corrigir de passagem".** Reapresentar decisão
confirmada como defeito gera ruído e desgasta a confiança nos achados reais.

> Instrução de preenchimento: este arquivo começa quase vazio e cresce com o
> projeto. Cada linha da primeira tabela nasce de uma pergunta da segunda que o
> proprietário confirmou como intencional — sempre com a fonte da confirmação
> (commit, data, registro de decisão).

## Confirmadas (com a fonte da confirmação)

| Tema | Decisão |
|---|---|
| {{TEMA}} | {{DECISAO — o que parece defeito mas é desenho, por quê, e ONDE foi confirmado}} |

## Candidatas — observadas no exame, pendentes de confirmação do PO/proprietário

Comportamentos do produto que *parecem* anomalia mas aparentam ser desenho.
Até confirmação, **não são achados nem defeitos** — são perguntas:

- {{PERGUNTA_CANDIDATA}}

Confirmada qualquer uma como intencional → sobe para a tabela acima com a fonte.
