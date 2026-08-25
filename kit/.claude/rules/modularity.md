# R9 — Modularização (pré-condição da equipe multi-agente)

Severidade: **bloqueante** para módulo NOVO (stage `lint-arch`, quando o produto
o instalar); estado herdado é legado documentado, não licença.

"Um módulo por delegação" só funciona com "um dono por símbolo".

> Lição de origem: 115 declarações top-level em escopo compartilhado, uma função
> de render monkey-patcheada 4×, CSS estilizando 178 seletores alheios e módulos
> conversando por regex sobre texto renderizado — cada delegação paralela virava
> colisão.

Para todo módulo novo (adapte os mecanismos à linguagem do produto — os itens
marcados (*) vêm de um produto JavaScript de página única; o princípio por trás
de cada um é o que importa):

1. **Escopo próprio e instalação única** (*IIFE + guarda `__installed`; em
   Python: módulo/pacote com API explícita, sem efeito colateral de import).
2. **Um ponto de contato público por módulo, registrado em manifesto**
   (`.claude/verify/bridges.json` ou equivalente: nome, owner, nota). Símbolo
   global fora do registro = FAIL de lint.
3. **Contrato inter-módulo só pela API registrada.** Proibido: regex sobre
   saída renderizada; ler estado interno alheio como canal de decisão.
4. **Proibido monkey-patch de função alheia.** Extensão só via API de registro
   (padrão registry/plugin). Ponto de extensão novo = entrada aprovada pelo TL
   no `plan.md`.
5. **Estado canônico nunca nasce em módulo decorador.** Dono do estado é tarefa
   do `core-engineer`, exposto por getters/setters da API; apresentação só
   consome. Campo obrigatório "owner do estado" na spec para todo dado novo.
6. **Namespace visual/CSS com prefixo do próprio módulo** (*); seletor alheio
   exige allowlist de exceções revisada.
7. **Orçamento de tamanho: ~600 linhas** ou justificativa registrada no
   plan.md; uma responsabilidade por módulo.
8. **Helper único por semântica de invariante** — estados tri-state, limiares e
   afins vivem num helper exposto pela API do dono; comparação literal duplicada
   fora do dono é candidata a FAIL de lint.
9. **Proibições de superfície insegura da linguagem** (*no origem: zero
   `innerHTML =`; defina o equivalente do seu stack — ex.: SQL por string,
   `eval`, shell sem aspas) — verificadas pelo `lint-arch`.
