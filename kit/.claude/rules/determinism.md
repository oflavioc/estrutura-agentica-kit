# R7 — Determinismo por construção

Severidade: **bloqueante** (stage `build` + `.gitattributes`).

"Determinismo comprovado apenas numa plataforma" é determinismo por plataforma —
frágil. Determinismo aqui é **por construção**:

1. **LF em todo texto** — `.gitattributes` com `* text=auto eol=lf`; arquivo
   binário ou com CRLF interno pinado byte a byte é marcado `-text`.
2. **Geradores escrevem com `newline="\n"` e stdout UTF-8 explícitos** — mesmo
   byte em qualquer SO.
3. **Verificação nunca escreve na árvore**: o stage `build` constrói em
   diretório efêmero e compara; geradores oferecem `--check`; todo stage prova
   `git status` inalterado ao final. Gerador testado escreve em tmp, nunca sobre
   arquivo versionado.
4. **Dependência de ambiente é declarada, nunca implícita** — o `env-doctor`
   (stage 0) valida a toolchain declarada em `toolchain.json` ANTES das suítes;
   ausência vira WARN nomeado ou FAIL, jamais SKIP silencioso. Oráculo que
   invoca processo usa caminhos **entre aspas** (path com espaço é o caso que
   sempre volta).
5. **A plataforma canônica é o CI** ({{CI_WORKFLOW — ex.: .github/workflows/verify.yml}})
   — prova contínua em cada PR; o desenvolvimento local tem paridade real via
   `.gitattributes`.
6. **Aleatoriedade e relógio não entram em artefato verificado** — saída de
   builder e de gerador é função pura dos fontes.

> Lição de origem: um gerador sem `newline="\n"` corrompeu a árvore em CRLF num
> checkout Windows e três suítes "quebraram" sem defeito algum no produto.
