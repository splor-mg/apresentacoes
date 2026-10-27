---
slides:
  title: SDD assistido por IA — Semantic Versioning
  theme: dracula
revealjs:
  width: 1920
  height: 1080
---

<style>
.reveal pre code { max-height: 900px; white-space: pre-wrap !important; overflow-wrap: anywhere; }
.reveal table { font-size: 0.55em; }
.reveal h2 { text-transform: none; }
.ver-scheme { margin-top: 56px; }
.ver-row { display: flex; align-items: center; justify-content: center; gap: 28px; }
.ver-node {
  min-width: 220px;
  padding: 22px 28px;
  border-radius: 16px;
  background: #44475a;
  color: #f8f8f2;
  font-size: 0.72em;
  font-weight: 700;
  letter-spacing: 0.02em;
}
.ver-node-end { background: #ff79c6; color: #282a36; }
.ver-shaft { position: relative; width: 860px; height: 150px; }
.ver-line {
  position: absolute;
  left: 0;
  right: 22px;
  top: 72px;
  height: 8px;
  border-radius: 8px;
  background: linear-gradient(90deg, #8be9fd, #ff79c6);
}
.ver-head {
  position: absolute;
  right: 0;
  top: 56px;
  width: 0;
  height: 0;
  border-top: 20px solid transparent;
  border-bottom: 20px solid transparent;
  border-left: 28px solid #ff79c6;
}
.ver-stop {
  position: absolute;
  top: 8px;
  transform: translateX(-50%);
  color: #f8f8f2;
  font-size: 0.48em;
  font-weight: 600;
}
.ver-stop::after {
  content: "";
  position: absolute;
  left: 50%;
  top: 46px;
  width: 4px;
  height: 22px;
  background: #bd93f9;
  transform: translateX(-50%);
}
.ver-stop-a { left: 30%; }
.ver-stop-b { left: 68%; }
.reveal :not(pre) > code { white-space: nowrap; }
.reveal .norm-table table { font-size: 0.72em; }
.reveal .big-code pre { font-size: 0.62em; }
.flow { display: flex; align-items: stretch; justify-content: center; gap: 20px; margin: 48px 0 40px; }
.flow-step {
  flex: 1 1 0;
  max-width: 400px;
  padding: 28px 26px;
  border-radius: 16px;
  background: #44475a;
  color: #f8f8f2;
  font-size: 0.6em;
  line-height: 1.35;
  text-align: left;
}
.reveal .flow-step b { display: block; margin-bottom: 12px; color: #8be9fd; font-size: 1.2em; }
.flow-what { display: block; margin-bottom: 14px; font-weight: 700; }
.flow-what code { font-size: 0.92em; }
.flow-ai { box-shadow: inset 0 0 0 4px #bd93f9; }
.reveal .flow-ai b { color: #bd93f9; }
.flow-end { background: #ff79c6; color: #282a36; }
.reveal .flow-end b { color: #282a36; }
.flow-arrow { align-self: center; color: #ff79c6; font-size: 1.2em; font-weight: 700; }
.stab { margin-top: 40px; }
.stab-caption {
  margin-bottom: 16px;
  color: #8be9fd;
  font-size: 0.38em;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}
.stab-row { display: flex; align-items: center; justify-content: center; gap: 16px; }
.stab-node {
  min-width: 200px;
  padding: 18px 24px;
  border-radius: 16px;
  background: #44475a;
  color: #f8f8f2;
  font-size: 0.58em;
  font-weight: 700;
}
.stab-beta { background: #6272a4; }
.stab-rc { background: #bd93f9; color: #282a36; }
.stab-release { background: #ff79c6; color: #282a36; }
.stab-lt { color: #ff79c6; font-size: 0.7em; font-weight: 700; }
</style>

# SDD assistido por IA

## Semantic Versioning

28 de outubro de 2026

<!--s-->

## O óbvio

- Um número de versão só comunica alguma coisa quando quem publica e quem consome compartilham a regra.
- Sem essa regra, `1.7.3` é um rótulo. Com ela, é um contrato.
- SemVer é esse contrato. O número diz o _risco de atualizar_.

<!--s-->

## Quatro jeitos de numerar

| Esquema     | A pergunta que responde  | Exemplo                      |
| ----------- | ------------------------ | ---------------------------- |
| **SemVer**  | Isso quebra quem já usa? | `1.9.0` → `2.0.0`            |
| **CalVer**  | Quando isso saiu?        | `2026.10.28`, Ubuntu `24.04` |
| **ZeroVer** | Ainda estamos em `0.y`?  | `0.24.1` para sempre         |
| **Hash**    | Quais bytes são estes?   | `a8f32c1`                    |

Notes:
ZeroVer permanece na série 0.y para não prometer estabilidade. Hash identifica o conteúdo e não diz nada sobre compatibilidade. Versionamento romântico é a ausência de esquema: o número sobe por sentimento.

<!--s-->

## Quando cada um cabe

- **SemVer**, quando existe interface pública: CLI, API, config, formato de saída, esquema de dados.
- **CalVer**, quando a pergunta é a data. Um snapshot, um relatório periódico, uma distribuição.
- **ZeroVer**, enquanto o contrato ainda não existe. A série `0.y.z` _não promete_ estabilidade. Isso tem de estar escrito.
- **Hash**, como identidade do artefato. Complementa a versão. Não a substitui.

Número sem regra não é versão.

<!--s-->

## SemVer em uma frase

`MAJOR.MINOR.PATCH` diz o risco de atualizar (**compatibilidade**).

- **MAJOR** — a interface pública quebrou. `1.8.4` → `2.0.0` se uma opção documentada some.
- **MINOR** — entrou **funcionalidade** compatível, ou uma depreciação. `1.8.4` → `1.9.0` ao acrescentar `--dry-run`.
- **PATCH** — correção que preserva o contrato. `1.9.0` → `1.9.1`.

<!--s-->

## Antes do número, a fronteira

Sem a interface pública nomeada, MAJOR / MINOR / PATCH vira opinião.

- Entram no contrato: comando, opção, config, JSON documentado, esquema, integração.
- Ficam de fora, salvo aviso: texto de log humano, ordem interna, detalhe que ninguém consome.

<!--s-->

## Prévia não é tamanho

- `2.0.0-beta.1` é uma prévia da ruptura. `beta` não significa “mudança pequena”.
- A sequência `1.10.0-alpha` → `1.10.0-rc` → `1.10.0` mantém o mesmo alvo.
- `1.2.0-rc.2` vem antes de `1.2.0-rc.10`. Os dois vêm antes de `1.2.0`.
- `1.2.0+build.17` e `1.2.0+build.18` são a mesma versão. O sufixo `+` não ordena.

<div class="stab">
<div class="stab-caption">estabilidade</div>
<div class="stab-row">
<div class="stab-node">alpha</div>
<div class="stab-lt">&lt;</div>
<div class="stab-node stab-beta">beta</div>
<div class="stab-lt">&lt;</div>
<div class="stab-node stab-rc">rc</div>
<div class="stab-lt">&lt;</div>
<div class="stab-node stab-release">release</div>
</div>
</div>

<!--s-->

## O maior impacto ganha

O número olha _tudo_ o que entrou desde a versão anterior.

Três correções, duas funções novas e uma quebra de contrato não viram PATCH porque o último commit foi um fix.

Prevalece o maior impacto. Nesse caso, MAJOR.

<div class="ver-scheme">
<div class="ver-row">
<div class="ver-node">1.8.15</div>
<div class="ver-shaft">
<div class="ver-line"></div>
<div class="ver-head"></div>
<div class="ver-stop ver-stop-a">1.8.16-beta.1</div>
<div class="ver-stop ver-stop-b">1.9.0-alpha.1</div>
</div>
<div class="ver-node ver-node-end">2.0.0</div>
</div>
</div>

<!--s-->

## Um número, uma entrega

- `1.9.0` publicado com defeito não é reescrito. A correção é `1.9.1`.
- Uma linha antiga pode seguir viva. `1.8.6` pode sair depois de `2.1.0`.
- O número diz o risco. O registro da versão diz o que mudou e como migrar.

<!--s-->

## Para levar

- Onde há interface pública, o esquema é **SemVer**.
- CalVer responde _quando_. Hash responde _quais bytes_. Nenhum dos dois diz se a atualização quebra.
- Antes de escolher MAJOR, MINOR ou PATCH, nomear o que é contrato.
- O número publicado não se reaproveita.

`1.7.3` ou é um rótulo, ou é uma promessa.

<!--s-->

# Proposta

## spok — Splor Kit

A norma de versão num pacote, com o Copilot ajudando a aplicar.

<!--s-->

## O que vimos hoje já é norma

Cada regra desta apresentação pode ser escrita como norma, com um ID.

<div class="norm-table">

| Tema               | Normas                              | Onde apareceu hoje                                  |
| ------------------ | ----------------------------------- | --------------------------------------------------- |
| Esquema e contrato | `VERSION-01-01-01` e `-01-01-02`    | Quando cada um cabe · Antes do número, a fronteira  |
| Incremento         | `VERSION-01-02-01` a `-01-02-05`    | SemVer em uma frase · O maior impacto ganha         |
| Prévia e build     | `VERSION-01-03-01` a `-01-03-04`    | Prévia não é tamanho                                |
| Versão publicada   | `VERSION-01-04-01` a `-01-04-03`    | Um número, uma entrega                              |
| Decisão            | `VERSION-01-05-01` e `-01-05-02`    | O que o spok faria (a seguir)                       |

</div>

<!--s-->

## Cada norma tem um ID

<div class="big-code">

```markdown
### VERSION-01-02-02 — Incrementar MINOR por funcionalidade compatível

**Força:** MUST, sob SemVer.
**Regra:** a introdução de funcionalidade pública compatível DEVE incrementar MINOR e reiniciar PATCH em zero.
**Por quê:** sinaliza expansão do contrato sem quebra de compatibilidade.
**Exemplo/contexto:** acrescentar `--dry-run` sem modificar o comportamento anterior: `1.8.4` → `1.9.0`.
```

</div>

- `VERSION` é o domínio. Os três blocos são família, tema e sequência.
- O ID não é número de versão. É o endereço da regra, e é ele que o Copilot cita.

<!--s-->

## spok: Splor Kit

<div class="r-hstack" style="align-items:flex-start; gap:80px">
<div style="flex:1">

- Um **pacote** Python com CLI, como o `dpetl`. Usa-se pelo comando, não por `import`.
- Mora num repositório da splor-mg e entra no projeto como dependência de desenvolvimento.
- **Kit** porque junta a norma e o comando que ajuda a cumpri-la.
- Começa com um domínio: `version`.

</div>
<div style="flex:1">

```text
spok/
├── cli.py                    spok version …
└── catalog/
    └── version/
        ├── spec_version.md   norma: as regras, com ID
        ├── tmpl_version.md   template: o formato da resposta
        └── agt_version.md    agente: o papel do Copilot
```

</div>
</div>

Notes:
Pacote, e não biblioteca: biblioteca é o que se importa no código. O spok se instala e se usa pelo terminal, como o dpetl. Dentro dele, o catálogo por domínio: norma, template e agente.

<!--s-->

## Como funcionaria

<div class="flow">
<div class="flow-step">
<b>1. Prepara</b>
<span class="flow-what"><code>spok version bump</code></span>
Lê a versão atual e os commits desde ela. Junta com a norma, o template e o agente. Copia tudo.
</div>
<div class="flow-arrow">→</div>
<div class="flow-step flow-ai">
<b>2. Julga</b>
<span class="flow-what">Copilot</span>
Recebe o texto colado. Responde no template: o nível, as normas que o justificam e o comando.
</div>
<div class="flow-arrow">→</div>
<div class="flow-step">
<b>3. Calcula</b>
<span class="flow-what"><code>spok version bump minor</code></span>
Faz a conta, 1.8.4 → 1.9.0, e grava no <code>pyproject.toml</code> e no <code>CHANGELOG.md</code>.
</div>
<div class="flow-arrow">→</div>
<div class="flow-step flow-end">
<b>4. Decide</b>
<span class="flow-what">Você</span>
Revisa o que mudou e faz o commit. Publicar é outro passo.
</div>
</div>

A IA julga. O script calcula. Quem decide é você.

Notes:
O spok não chama a IA. Ele prepara o texto e aplica a resposta. Hoje o canal é copiar e colar no Copilot. Se um dia houver um agente no terminal, o mesmo agente vira uma skill, e a norma não muda.

<!--s-->

## Como seria na prática

<div class="big-code">

```console
$ spok version bump
Contexto copiado: agente, template, normas VERSION-01, versão 1.8.4 e 7 commits.
Cole no Copilot.
```

O Copilot responde preenchendo o template:

```text
Nível:   MINOR
Normas:  VERSION-01-02-02  entrou --dry-run, sem mudar o que já existia
         VERSION-01-02-04  nos 7 commits, nada pede mais que MINOR
Comando: spok version bump minor
```

```console
$ spok version bump minor
1.8.4 → 1.9.0   pyproject.toml, CHANGELOG.md
O commit fica com você.
```

</div>

<!--s-->

## O início também

<div class="big-code">

```console
$ spok dev init
Nenhum arquivo de concepção em _dev/.concep/.
Esta camada exige --epic: a issue e o épico já precisam existir.
```

```console
$ spok dev init -h
spok dev init [--concep PATH] [--epic PATH|ID] [--main-issue #N]
spok dev init status|doctor [--epic PATH|ID]
spok dev init --dry-run

1. Classifica as relações da issue
2. Cria o épico, ou anexa o que veio em --epic
3. Cria o branch, salvo quando o trabalho fica na main
4. Marca o primeiro passo e oferece o commit
```

</div>

<!--s-->

## Sincronizar é atualizar o pacote

- A norma não é copiada de projeto em projeto. Ela viaja dentro do spok.
- Cada projeto fixa a versão do spok que segue, como qualquer dependência.
- Norma nova e compatível: MINOR do spok. Norma que muda o que já valia: MAJOR.
- `poetry update spok` traz a norma nova. O spok segue o SemVer que ensina.

<!--s-->

## Próximos passos

1. Fechar as normas de `version`, a partir de `VERSION-01`.
2. Criar o repositório `spok` na splor-mg, começando em `0.1.0`.
3. Deixar escrito o que a série `0.y` promete (`VERSION-01-02-05`).
4. Testar o ciclo com o Copilot num repositório da equipe.
5. Depois de `version`, outros domínios, do mesmo jeito.

`1.7.3` é uma promessa. O spok ajuda a cumpri-la.
