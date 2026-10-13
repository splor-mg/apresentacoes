---
slides:
  title: Relacionamento de Bases de Dados - Linktable
  theme: dracula
revealjs:
  width: 1920
  height: 1080
---

<style>
.reveal pre code { max-height: 900px; white-space: pre-wrap !important; overflow-wrap: anywhere; }
</style>

<div class="r-hstack" style="align-items:flex-start; gap:80px">
<div style="flex:1">

#  Relacionamento de Bases de Dados

## método _Linktable_

<!--s-->

## Contexto

👉 [ETL é o caminho que o dado percorre até se tornar informação útil](https://splor-mg.github.io/apresentacoes/20260701_etl.html?showNotes=true#/1).

- _O óbvio precisa ser dito_.
- Integrar dados de diferentes fontes para aprimorar a _tomada de decisão_.
- Um processo mecânico (automatizado ou não).
- Não envolve análise de dados.
- [Acrónimo](https://pt.wikipedia.org/wiki/Acr%C3%B3nimo):
  - _Extract (Extrair)_:
    - Tirar os dados de onde eles vivem.
    - Os dados são lidos, não alterados.
    - Se a extração falhar, todo o ETL falha.
  - _Transform (Transformar)_: Tratar, padronizar e enriquecer os dados.
  - _Load (Carregar)_: Armazenar os dados prontos em um destino final (análise de dados e tomada de decisão).

<!--s-->
## Proposta

<div class="r-hstack" style="align-items:flex-start; gap:80px">
<div style="flex:1">

- Repositório [dados-orcamentarios](https://github.com/splor-mg/dados-orcamentarios):
  - schemas
  - scripts
  - workflow

- Repositório do datapackage:
  - dados processados
  - descriptor (datapackage.json)

</div>
<div style="flex:1">

- [dpetl](https://github.com/splor-mg/dpetl)
  - dpetl_extract
  - dpetl_transform
  - dpetl_load

- Datamart
  - Banco de dados único com todos os dados orçamentários.

</div>
</div>

<!--s-->

## Relatório Operacional

- Painel de Dados
- Agrega dados hisóricos e atualizados
- Universo SIAFI, SIAD e da reestimativa de receitas e despesas.


<!--v-->


![](assets/dpetl_linktable/roperacional.png)
