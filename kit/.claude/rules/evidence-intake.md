# R11 — Entrada de evidência

Severidade: **bloqueante** (hook `guard-data`).

1. **Toda geração de evidência escreve em diretório ignorado** ({{DIRS_EVIDENCIA
   — ex.: `visual_evidence/`, tmp}}) — nunca em diretório rastreado como efeito
   colateral de rodar uma ferramenta.
2. **A entrada no repositório é um passo explícito de promoção**: `qa-engineer`
   aprova o conteúdo → `build-engineer` publica no evidence store ({{EVIDENCE_STORE
   — ex.: GitHub Releases, um release por fase}}) → `doc-writer` registra o
   manifesto de hashes. O repo versiona o manifesto, não os bytes.
3. **`guard-data` bloqueia no commit**: arquivo casando padrão sensível
   declarado no boundary.json (seção `dados`), PDF novo, padrão de segredo,
   **binário novo >200 KB** — inclusive dentro de `.claude/**`.
4. **Dados reais de clientes/usuários vivem fora do clone**
   ({{DIR_DADOS_EXTERNO}}). Nome de pessoa, documento, identificador sensível,
   teor de material de cliente: nunca em arquivo versionado, memória de agente,
   log ou mensagem.
5. Se um segredo aparecer em texto no chat: avisar que ficou no transcript e
   sugerir rotação.

> Lição de origem: ~103 MB de evidência binária commitada "de passagem" ao longo
> de três fases — sair do git sem quebrar a verificabilidade exigiu um projeto
> de migração inteiro. Mais barato nunca deixar entrar.
