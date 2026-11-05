# CT-SER-008 — Exportar a lista em CSV e PDF

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Verificar que CSV e PDF contêm toda a consulta filtrada e ordenada, inclusive linhas fora da página visível, com os campos e nomes definidos.

## Requisitos relacionados

DOCX, 1.1.7.1 / backlog 24304: CA01–CA11, US01, US02. 1.1.2.2 / 24147: CA01–CA03, US01, US02, no uso da ordenação por nome. 1.1.6.1 / 24232: CA01, CA06, CA07, CA09, US05, no uso conjunto de status e periodicidade. Regras de dados: Exportações, Datas e próxima execução, Resultados vazios e falhas.

## Ator e permissões

U08 autenticado com SERVICO_LISTAR, suficiente para consulta e exportação da lista.

## Pré-condições e dados fictícios

Todos já cadastrados; sem OS. T01 = Preventiva, A01 = Motor e A02 = Bancada, existentes e não excluídos. Última realização ausente será apresentada como Não informado. Capacidade preparada de duas linhas por página.

| ID | Nome | Descrição | Tipo | Dias | Status | Início | Última realização | Ativos |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| E01 | Delta | Revisar motor | T01 | 7 | Ativo | 01/11/2026 | ausente | A01 — Motor |
| E02 | Alfa | Revisar bancada | T01 | 7 | Ativo | 02/11/2026 | 05/11/2026 | A02 — Bancada |
| E03 | Charlie | Conferir conjunto | T01 | 7 | Ativo | 03/11/2026 | ausente | nenhum |
| E04 | Bravo | Conferir apoio | T01 | 7 | Ativo | 04/11/2026 | ausente | A01 — Motor |
| E05 | Eco | Fora por status | T01 | 7 | Inativo | 01/11/2026 | ausente | nenhum |
| E06 | Foxtrot | Fora por período | T01 | 14 | Ativo | 01/11/2026 | ausente | nenhum |
| E07 | Golf | Fora por exclusão | T01 | 7 | Ativo | 01/11/2026 | ausente | nenhum |

E07 está excluído logicamente; os demais não. Consulta preparada: status Ativo E periodicidade 7 dias, nome crescente. Página 1: E02,E04; página 2: E03,E01. O instante controlado de geração é 05/11/2026 14:30:45 UTC, usado apenas para exemplificar nomes; em execução real deve corresponder ao instante efetivo.

## Fluxo principal

1. U08 confere os filtros e a ordenação, navega até a página 2 e solicita exportação. Espera-se escolha entre CSV e PDF antes da geração.
2. U08 escolhe CSV. Espera-se arquivo completo somente após geração confirmada, sucesso após a resposta bem-sucedida, nome `exportacao_servicos_20261105_143045.csv` no instante controlado e delimitador ponto e vírgula.
3. U08 abre o CSV e confere as quatro linhas de dados da tabela abaixo, nesta ordem: E02,E04,E03,E01. Os IDs servem para rastrear a massa, sem exigir coluna de ID no arquivo. Esperam-se os nove campos do CA05, periodicidade em dias e datas DD/MM/AAAA.
4. Em tentativa independente com a mesma consulta e instante controlado, U08 escolhe PDF. Espera-se `exportacao_servicos_20261105_143045.pdf`, com as mesmas quatro linhas, sequência e valores, sem depender de qual página estava visível.
5. U08 compara ambos os formatos. Espera-se ausência de E05,E06,E07, sem omitir E02 ou E04 por estarem na primeira página da consulta.

## Fluxos alternativos

| Início | Condição | Resultado e término |
| --- | --- | --- |
| Passo 1 | Consulta válida com período 99 dias e nenhuma linha | Informar que não há dados para exportar. Nenhum arquivo de dados é disponibilizado e nenhum sucesso de geração é informado. Terminar com consulta vazia. |
| Passo 2 ou 4 | Falha preparada de geração, repetida separadamente para CSV e PDF | Informar falha sem detalhes internos, não informar sucesso e impedir download de arquivo incompleto. Terminar sem arquivo válido dessa tentativa. |

## Regras de negócio

Exportar o conjunto filtrado completo, ordenado antes da paginação. CSV usa `;`. Ambos os formatos usam os campos do CA05; não exigir OS na lista exportada. Data/hora UTC no nome identifica geração, sem mudar o fuso das datas de serviço.

## Dados e resultados esperados

Esta tabela descreve as linhas de dados dos dois formatos; a ordem física das colunas e seus rótulos não são impostos além da presença e identificação dos campos exigidos.

| Nome | Descrição | Tipo | Periodicidade em dias | Status | Início | Última realização | Próxima execução | Ativos |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Alfa | Revisar bancada | Preventiva | 7 | Ativo | 02/11/2026 | 05/11/2026 | 12/11/2026 | A02 — Bancada |
| Bravo | Conferir apoio | Preventiva | 7 | Ativo | 04/11/2026 | Não informado | 11/11/2026 | A01 — Motor |
| Charlie | Conferir conjunto | Preventiva | 7 | Ativo | 03/11/2026 | Não informado | 10/11/2026 | nenhum vínculo |
| Delta | Revisar motor | Preventiva | 7 | Ativo | 01/11/2026 | Não informado | 08/11/2026 | A01 — Motor |

“Nenhum vínculo” descreve ausência de ativos, sem exigir mensagem literal. Inverter a ordenação para nome decrescente em repetição independente dos passos 1–5 deve produzir E01,E03,E04,E02 nos dois formatos. Cada tentativa usa o seu instante efetivo; o mesmo nome de exemplo não exige relógios iguais em exportações reais distintas.

## Pós-condição

Dados e filtros preservados. Nas tentativas bem-sucedidas há um arquivo completo do formato solicitado; nas alternativas não há arquivo de dados válido disponível.
