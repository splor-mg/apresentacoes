---
slides:
  title: Servidor Qlik.
---

# Servidor Qlik

<!--s-->

## Pauta

- Apresentações
- Contexto Histórico
- Quem Utiliza
- Processos e Alternativas

<!--s-->

## Apresentações

<!--s-->

## Contexto Histórico

- Licenças Qlik.
- Servidor.

Note:

- Licença Qlik:
  - Licitação realizada em 2013.
  - Comprado Licenças para áreas logadas e abertas.
  - Para consultar a licitação basta pesquisar por "Qlik" no [Objeto de licitação](https://www1.compras.mg.gov.br/processocompra/pregao/consulta/consultaPregoes.html#).
  - [Consultar edital](https://www1.compras.mg.gov.br/processocompra/pregao/consulta/dados/abaDadosPregao.html?metodo=abrirArquivoEdital&idPregao=46408).
  - Qlik não vende mais este tipo de licença. Agora somente serviços Cloud.
- Servidor:
  - Windows Server 2008 R2 Standard.
  - Sem [suporte Microsoft](https://learn.microsoft.com/pt-br/troubleshoot/windows-server/windows-server-eos-faq/end-of-support-windows-server-2008-2008r2) a partir de 2020.
  - Disco com 80% de utilização (storage).
  - Memória RAM no seu limite de processamento.

<!--s-->

## Quem Utiliza

- Seplag:
  - SPLOR.
  - SCAP.
  - COFIN.
  - SUGES.
- Casa Civil.

<!--s-->

## Processos e Alternativas

- Processos ETL.
- Paineis Qlik.

Note:

- Estes são processos conhecidos pela AID.
- Gabriel (SCC) informou em 14/04/2025, [de maneira resumida](https://teams.microsoft.com/l/message/19:302739e5-013a-4388-987d-f726008fa3d0_ed7857d7-ef2d-4911-b321-cb2a443bec03@unq.gbl.spaces/1744639317776?context=%7B%22contextType%22%3A%22chat%22%7D), quais são os processos de extração de dados realizados pela SCC.
- ETL SPLOR sabe como transferir.
  - GitHub.
  - GitHub Actions.
  - Python.
  - [Datapackages](https://datapackage.org/overview/introduction/).
- Qlik:
  - Splor ainda não sabe qual ferramenta irá utilizar.
  - PowerBi é uma ótima alternativa para outras áreas.

<!--v-->

## Processos e Alternativas

Capacitações

Note:

- [Trilhadev](https://trilhadev.planejamento.mg.gov.br/main/).
- [Encontros com equipe](https://splor-mg.github.io/handbook/blog/category/etl/) para melhoria de nossos processos ETL.

<!--v-->

## Processos e Alternativas

- Power BI.
- Ferramentas de BI Open Source.
- Máquinas virtuais Azure (contrato intendência).

Note:

- PowerBi:
	- Não penso em migrar para nenhuma versão paga de PowerBi.
	- Sou muito a favor de projetos open source.
- [Metabase](https://www.metabase.com/):
  - Necessário ter uma base SQL.
	- Quais os principais desafios técnicos do Metabase que vocês identificaram?
		- Depender de uma base SQL (curva de aprendizado).
		- Instalação e manutenção (administração de servidor).
		- Pequena curva de aprendizado para montar as consultas/visualizações.
- [Streamlit](https://streamlit.io/):
  - Ferramenta Python.
  - Exige mais configuração para criar áreas logadas.
	- Como configurar para rodar 24h/dia em servidor? Precisa de algum gerenciador de processos?
		- Precisa ser instalado em um servidor, tipo Azure.
		- Existem algumas opções gratuitas que funcionariam, a depender do tamanho da aplicação.
	- Como funciona a atualização automática das bases de dados conectadas ao Streamlit?
		- Um GitHub actions poderia ser acionado periodicamente (diariamente ou até a cada hora).
		- Conectado automaticamente em um banco de dados (sem necessidade de atualização manual).
	- Quais os principais desafios ou limitações do Streamlit para ambientes corporativos?
		- Do ponto de vista de segurança não vejo nenhum.
		- Curva de aprendizado.
	- Rodar pelo GitHub/servidor elimina a necessidade dos usuários terem Python instalado localmente? Não queremos depender de scripts rodando apenas em computadores específicos.
		- Sim, esta responsabilidade fica a cargo do Action (GitHub) e/ou do servidor.
- [django](https://www.djangoproject.com/):
  - Ferramenta Python.
  - Exige um pouco mais conhecimento.
- Infraestrutura de dados
	- Vocês possuem um data lake estruturado?
		- Ainda não, mas está em nosso radar. Atualmente nossa base de dados são arquivos `.csv` no GitHub.
	- Se sim, qual a estrutura geral (softwares utilizados, arquitetura de tratamento, camadas de dados)?
		- Banco de dados SQL (PostgreSql).
		- Aplicação web para facilitar modificações nos schemas do banco (django).
		- Servidor Azure.
		- ELT em Python (padrão frictionless e AID)

- Azure:
  - Conhecimento mínimo de administração de servidores.
  - [easypanel](https://easypanel.io/) pode ajudar e dar autonomia em relação à PRODEMGE e consultores Microsoft.
