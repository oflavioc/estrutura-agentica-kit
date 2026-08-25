# CONTEXT — glossário canônico

> Mantido pelo `product-owner` na Fase 0 de cada demanda (R12). Só glossário:
> o que cada conceito É, em uma ou duas frases. Doc, spec e prompt novos usam o
> termo daqui, sem derivar para os sinônimos evitados.

## {{DOMINIO}} (produto)

**{{Termo}}**:
{{Definição em uma ou duas frases — o que o conceito É.}}
_Evitar_: {{sinônimo-a}}, {{sinônimo-b}}

## Estrutura (processo)

**Demanda**:
Unidade de trabalho que percorre as 7 fases da máquina SDD (skill new-demand),
com specs/NNN-slug/ e planning-state próprios.
_Evitar_: feature (reservado ao tipo de tarefa e ao nome de branch), pedido

**Onda**:
Etapa de implantação da Estrutura Agêntica (0–4), com critério de pronto
executável. Distinta de *wave* (grupo de tarefas paralelas dentro de uma
demanda).
_Evitar_: fase (reservado à máquina SDD e aos marcos do produto)

**Pin / repin**:
Identidade SHA-256 de um artefato no registry (pins.json). Repin = atualização
consciente, no mesmo PR, com trilha "Identidade anterior".
_Evitar_: hash solto, checksum informal

**Boundary**:
Manifesto de classes de proteção (frozen/generated/legacy/registry) com o rito
de mudança de cada uma. Fecha acumulativamente a cada selagem.
_Evitar_: escopo, lista de proibidos

**Red / green**:
Estados do ciclo TDD: gate provado FALHANDO antes da implementação (red,
commitado) e passando depois (green). Sem red provado não há green que valha.
_Evitar_: teste quebrado (red é intencional)

**Gate**:
Asserção executável com poder discriminante provado por mutante. O que decide é
o gate, nunca a leitura de quem implementou.
_Evitar_: teste (genérico), checagem manual

**Selagem**:
Ato do auditor humano que congela uma fase: release develop→main com tag
anotada; a boundary da fase fecha para sempre.
_Evitar_: entrega, conclusão de sprint

**Acervo de evidência**:
Conjunto congelado de artefatos que sustenta a selagem de uma fase; imutável
após a selagem, com identidade por manifesto de hashes.
_Evitar_: pasta de prints, anexos, evidências soltas

**Evidence store**:
Destino externo ao clone onde acervos de evidência publicados vivem
({{EVIDENCE_STORE}}). O repositório versiona o manifesto, nunca os bytes.
_Evitar_: backup, pasta externa, storage
