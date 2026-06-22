# Toolkit north-star — design

> **Status:** `[TARGET]` · **Altitude:** SOLUÇÃO · **Eixo:** estrutura
> **Pergunta-foco:** Como o toolkit north-star organiza skills de desenho conceitual de software?

Este é o design do próprio toolkit — o north-star do north-star. Ele "come a própria
comida": é escrito na forma que prescreve (a anatomia comum, §4), na camada Solução.

---

## 1. Propósito

O **north-star** é um toolkit de skills do Claude Code para **desenho conceitual** de
software — o sistema que se *pretende* construir, e por quê. Todo artefato do toolkit
passa por quatro critérios (o DNA):

1. **Alvo, não as-is** — desenha o pretendido, não documenta o existente.
2. **Acima do spec/ADR/implementação** — conceitual.
3. **Tech-agnóstico** — papéis, significado e contratos-como-significado; não APIs, schemas ou stacks.
4. **Enxuto e vivo** — lê-se como contexto no início de uma sessão de trabalho.

**Quem lê este doc:** quem desenvolve ou estende o toolkit. **Quando:** ao criar uma
skill/template novo, ou ao decidir se um tipo de documento "cabe".

## 2. Premissas / entrada

- **Origem:** pesquisa das famílias de notação — C4, arc42, ArchiMate, ISO/IEC 42010,
  ARCADIA/Capella, SysML, UML (perspectiva conceitual de Fowler), DDD (estratégico e
  tático), Event Storming, Domain Storytelling, Wardley Mapping, Impact Mapping,
  Capability Mapping, Journey/Service Blueprint, design docs (Google), PR-FAQ (Amazon).
  O catálogo (§5) destila o veredito de altitude de cada uma.
- A skill `designing-by-altitude` (v0.1.0) já existe e será **reposicionada** (§7).
- **Lê acima:** — (este doc é o topo do design do toolkit; sua "altitude acima" é a
  pesquisa e a intenção do autor.)

## 3. A espinha — altitude (abstração)

**Altitude** = distância do problema à forma. O toolkit se organiza em **três camadas**,
fechadas por uma **linha de corte**:

```
NEED      o problema, antes de qualquer forma        (= ARCADIA Operational + System Analysis)
  ↓ lê
CONCEITO  o modelo mental do domínio, ainda não a forma
  ↓ lê
SOLUÇÃO   a forma conceitual, tech-neutra            (= ARCADIA Logical Architecture)
═════════ altitude-stop (a linha dura) ═════════
[FORA]    spec · ADR · physical/deployment · schema/API · números   → delegado
```

A lição que dá nome ao toolkit (de ARCADIA, Fowler e 42010): **o erro nunca é misturar
diagramas — é misturar a pergunta "que problema?" com "que forma?", e "que forma?" com
"que tecnologia?".** Cada camada mantém uma dessas perguntas em sua própria página.

### Eixos (tags transversais)

O *que* um documento expressa corta as camadas em quatro eixos: **estrutura** ·
**conceito** · **fluxo** · **estratégia**. O eixo é uma etiqueta; a camada é que manda.

### Zoom / escopo (dentro de SOLUÇÃO)

Na camada Solução existe uma sub-dimensão de **zoom**: **sistema ↔ bloco**. O North Star
descreve o sistema inteiro; um Subsystem design descreve um bloco. Zoom **não** é
altitude — um Subsystem não é "menos abstrato" que o North Star, é menor em escopo.

### Regra de leitura

**Cada documento lê a(s) altitude(s) acima como input.** NEED é o topo (não lê nada);
CONCEITO lê NEED; SOLUÇÃO lê CONCEITO + NEED. Dentro de Solução, o Subsystem lê o
North Star.

## 4. A anatomia comum (meta-template)

Toda skill/documento do toolkit herda esta forma. É o primeiro artefato a construir —
ele vira o molde de todos os demais.

```
─── cabeçalho ───
Título · Altitude (NEED | CONCEITO | SOLUÇÃO) · Eixo · Status global
Pergunta-foco — a pergunta única que este documento responde

─── corpo ───
1. Propósito              — o que é, quem lê, quando (1–2 frases)
2. Premissas / entrada    — o que toma como dado; lê a altitude acima
3. Corpo do eixo          — o conteúdo específico do template
4. Alternativas + trade-offs — os caminhos não tomados, e por quê
5. Limitações / riscos / questões em aberto
6. PARE AQUI (altitude-stop) — a linha dura deste documento: o que NÃO descrever
7. Ponteiros para baixo   — specs/ADRs/docs-filhos com o detalhe

marcadores inline: [TARGET] [DECIDED] [FRONTIER] [LEGACY]
```

**Sobre cada parte:**

- **Pergunta-foco** (de 42010 *concern* + Novak *focus question*): força o documento a ter
  um propósito único. Se ele responde duas perguntas, são dois documentos.
- **PARE AQUI** é a parte que define a identidade do toolkit. Cada template **instancia a
  própria linha** — o ponto onde o conteúdo cairia para a camada de baixo. Ex.: um Modelo
  de Estados para em "estados ≠ enum/coluna `status`; transições ≠ chamadas de método".
- **Status markers:** `[TARGET]` (quer, não construído) · `[DECIDED]` (firmado em ADR) ·
  `[FRONTIER]` (aposta em pesquisa) · `[LEGACY]` (existe, sendo superado).

### 4.1 Notação — prosa estruturada com diagramas Mermaid

**Regra-mãe:** a **prosa** é a espinha de todo documento (carrega a alma — propósito,
princípios, contratos-como-significado, alternativas, riscos); os **diagramas Mermaid**
entram só no **Corpo do eixo** (item 3), dando esqueleto e movimento. *Diagrama embeleza o
que muda; prosa guarda o que permanece.*

**Notação primária: Mermaid** — cobre estrutura, fluxo e estado num só ecossistema,
renderiza nativo em markdown/GitHub (design-as-context vivo, sem ferramenta) e é a de maior
fidelidade na geração/manutenção. **Upgrade path** (quando o zoom crescer para dezenas de
componentes e o layout do Mermaid sufocar): D2 (escala visual) ou C4-PlantUML/Structurizr
(modelo único multi-vista).

| Seção do meta-template | Forma |
|---|---|
| 1 Propósito · 2 Premissas · 4 Alternativas · 5 Limitações · 6 PARE AQUI · 7 Ponteiros | **prosa** |
| 3 Corpo do eixo | **diagrama(s) Mermaid + prosa de apoio** |

| Eixo | Diagrama Mermaid |
|---|---|
| estrutura | `flowchart` + `subgraph` (blocos + contratos, C4-conceitual) |
| fluxo | `sequenceDiagram` (interação/tick) e/ou `flowchart` (processo) |
| estado | `stateDiagram-v2` (ciclo de vida de uma entidade) |
| conceito | `flowchart` / `classDiagram` conceitual (conceitos + relações rotuladas) |
| estratégia | sem diagrama de prateleira → prosa + tabela (opcional `quadrantChart`) |

Cada diagrama vem com 1–2 linhas de prosa que dão o significado que o desenho não carrega.
Nos diagramas, **caixas são papéis** (não serviços/classes) e **setas são intenções** (não
chamadas/assinaturas) — o altitude-stop vale também para o desenho.

## 5. O catálogo por altitude (roadmap)

Veredito: ✓ cabe · ⚠ cabe com altitude-stop forte · *existe* já no toolkit.

### NEED — o problema, antes da forma

| Template | Eixo | Veredito | Destilado de |
|---|---|---|---|
| PR-FAQ de visão | estratégia | ✓ | Amazon Working Backwards (o porquê / para quem) |
| Impact Map | estratégia | ✓ | Gojko Adzic (Why→Who→How→What) |
| Wardley Map | estratégia | ✓ | Simon Wardley (cadeia de valor × evolução; o movimento) |
| Capability Map | estratégia | ✓ apoio | "o quê" estável + heatmap north-star-crítico |
| Capacidades + contratos de fronteira | estrutura | ✓ | ARCADIA System Analysis (o sistema como caixa-preta) |

### CONCEITO — o modelo mental, ainda não a forma

| Template | Eixo | Veredito | Destilado de |
|---|---|---|---|
| Linguagem Ubíqua | conceito | ✓ fundacional | DDD (significado, não formato) |
| Mapa de Conceitos | conceito | ✓ | Novak (proposições sob uma pergunta-foco) |
| Modelo Conceitual de Domínio | conceito | ⚠ | UML class-conceitual + DDD tático (invariantes, não campos) + ontologia leve |
| Context Map | conceito/estratégia | ✓ | DDD (fronteiras e relações intencionais entre contextos) |

### SOLUÇÃO — a forma conceitual, tech-neutra

| Template | Eixo | Zoom | Veredito | Destilado de |
|---|---|---|---|---|
| North Star | estrutura | sistema | `[DECIDED]` *existe* | C4 Context/Container · arc42 N1 · ARCADIA Logical |
| Subsystem design | estrutura | bloco | `[DECIDED]` *existe* | arc42 blackbox · SysML bdd |
| Design Doc de visão | estrutura | sistema | ✓ podado | Google design doc (corta API/schema/storage) |
| Narrativa de Fluxo | fluxo | qualquer | ⚠ guarda-chuva | C4-dynamic + DFD-contexto + sequence-como-prosa |
| Modelo de Estados / Ciclo de Vida | fluxo | bloco | ✓ | UML state machine (de uma entidade) |
| Fluxo de Eventos de Domínio | fluxo | qualquer | ✓ | Event Storming Big-Picture/Process |

> **Bounded Context Canvas** (DDD Crew) é um *agregador* que cruza conceito + fluxo +
> estratégia de um único contexto. Candidato a template-âncora, fora das camadas puras.

## 6. A fronteira — o que fica fora

Definir o "não" é metade do valor de um north-star. Ficam **abaixo do altitude-stop**
(delegados ao fluxo `superpowers` de spec→plano→código, ou a ADRs):

- **ADR** — granular + registro do passado + concreto (viola 3 dos 4 critérios). É *filho*
  linkado, nunca conteúdo.
- **BPMN / fluxograma** — desenhados para virar processo executável.
- **DFD abaixo do nível de contexto · deployment · timing · parametric · ibd/component/
  composite/package/object · ARCADIA physical & EPBS · TOGAF** — tecnologia, wiring, números.
- **Mind map** — vira etapa de descoberta, não entregável (sem ligações rotuladas).
- **RFC/IETF** — entra como influência cultural (proposta escrita + revisão), não template.

## 7. Reconciliação da skill atual

`designing-by-altitude` (v0.1.0) usa "altitude" no sentido de **zoom** (sistema ↔ bloco).
Na espinha nova isso é re-significado: ambos os seus artefatos (North Star e Subsystem)
vivem na camada **Solução**, e o zoom passa a ser sub-dimensão dela. A skill será
reescrita para:

- adotar "altitude" = abstração (NEED → CONCEITO → SOLUÇÃO);
- posicionar-se como a skill da camada **Solução** (eixo estrutura);
- herdar a anatomia comum (§4);
- apontar para as camadas NEED e CONCEITO como input.

## 8. Alternativas + trade-offs

- **Organização por eixo de expressão** (estrutura/conceito/fluxo/estratégia como espinha;
  altitude transversal). *Rejeitada:* alinhava ao jeito intuitivo de pensar, mas perdia a
  fronteira need/solução — exatamente a lição mais forte da pesquisa (ARCADIA).
- **Escada de altitude contínua** (need → conceito → solução-sistema → solução-bloco).
  *Rejeitada:* funde abstração com zoom; impreciso (um bloco não é menos abstrato, é menor).
- **Por altitude (abstração), eixo transversal, zoom dentro de Solução.** *Escolhida:*
  honra need/conceito/solução, dá ao nome do toolkit um sentido mais forte, e acomoda os
  eixos sem misturar dimensões.

## 9. Limitações / questões em aberto

- **O North Star deixa de ser o topo absoluto** — NEED está acima dele.
  `[DECIDED 2026-06-22]` O North Star **permanece síntese ancorada**: vive na camada Solução
  e **distila o NEED** no topo (propósito, princípios, a virada), apontando para docs de NEED
  quando existirem. Validado no TDD da reescrita da `designing-by-altitude`.
- **Sobreposição no eixo fluxo** — Narrativa de Fluxo, Fluxo de Eventos e Modelo de Estados
  contam "como acontece" de ângulos diferentes. Consolidar fronteiras entre eles ao
  detalhar cada template.
- **Jornada / Camadas de Serviço** (UX) — eixo próprio ou variação opcional da Narrativa
  de Fluxo? Em aberto.
- **Empacotamento em skills** — uma skill por camada? por eixo? por template? Decidir
  depois que a anatomia comum e 2–3 templates exemplares existirem.

## 10. PARE AQUI (altitude-stop deste doc)

Este documento desenha a **forma** do toolkit. Não desce a: o conteúdo final de cada
template (isso é cada skill), o texto das `SKILL.md`, nem o plano de implementação (isso é
o spec/plano que vem a seguir).

## 11. Ponteiros para baixo

- `skills/designing-by-altitude/SKILL.md` — a reescrever (§7).
- O plano de implementação desta rodada — a criar (writing-plans).
- A pesquisa de origem — destilada no catálogo (§5) e na fronteira (§6).
