# Rastreabilidade — Gestão de Serviços

**Responsável:** Luca Lopes Marques. **Situação:** cenários documentais, não executados.

## Fonte e escopo

A fonte normativa é o DOCX BVapp_Gestao_Servicos_Ajustada, seções 1.1.1 a 1.1.7 e regras transversais. Os RF locais reorganizam as funções para leitura, sem substituir CA, US ou IDs do backlog. CA01/US01 são locais a cada feature. Os requisitos do exemplo de produtos e garantias foram usados apenas como modelo de redação.

A feature de PDF individual foi criada no OpenProject como #36153 na atualização registrada em 06/11/2026. Esse número substitui nesta documentação a indicação histórica de ausência de ID; não se usa NOVO-3.1.10 como ID definitivo. O número não é o ID de um serviço da aplicação.

## Responsabilidade dos casos de uso

| UC | Verificação concentrada | Referência anterior consolidada |
| --- | --- | --- |
| [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | Cadastro, edição, status, auditoria, vínculos e remoção | CT-SER-001; complementação do antigo CA11 de edição |
| [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | Lista, atualização da resposta, cinco colunas nos dois sentidos e paginação | CT-SER-002 e CT-SER-003 |
| [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | Busca, filtros isolados/combinados, datas e limpeza | CT-SER-004 e CT-SER-005 |
| [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | Detalhes, próxima execução, ativos, OS e navegação | CT-SER-006 e CT-SER-007 |
| [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | Exportação de lista em PDF/CSV | CT-SER-008 |
| [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | PDF individual | CT-SER-009 |
| [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | Autenticação e permissão por rota | CT-SER-010 e negativas antes dispersas |

Abrir uma consulta para alcançar uma edição não repete o teste da listagem. Conferir que uma exportação preservou filtros não repete os controles de filtro. Arquivos que dependem de cálculo ou autorização referenciam seu responsável, sem criar outro caso equivalente. PDF e CSV são alternativas do mesmo caso de exportação.

## Cobertura dos 76 CA

Cada critério tem um responsável primário na tabela; referências transversais não criam cópias de cenários. A cobertura é documental: comportamentos positivos, negativos e caminhos alternativos previstos. Não equivale a teste executado nem exaure combinações arbitrárias de entradas.

| Feature / backlog | RF | CA | UC responsável | Fluxos ou regras |
| --- | --- | --- | --- | --- |
| 1.1.1.1 / 24078 | RF001 | CA01 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP |
| 1.1.1.1 / 24078 | RF001 | CA02 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP, A2, RN1 |
| 1.1.1.1 / 24078 | RF001 | CA03 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A4, RN2 |
| 1.1.1.1 / 24078 | RF001 | CA04 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A2 |
| 1.1.1.1 / 24078 | RF001 | CA05 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP |
| 1.1.1.1 / 24078 | RF001 | CA06 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP, A5 |
| 1.1.1.1 / 24078 | RF001 | CA07 | [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | A1, A2, A3 |
| 1.1.1.1 / 24078 | RF001 | CA08 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP |
| 1.1.1.1 / 24078 | RF001 | CA09 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A5 |
| 1.1.1.1 / 24078 | RF001 | CA10 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A3 |
| 1.1.1.1 / 24078 | RF001 | CA11 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A2 |
| 1.1.1.1 / 24078 | RF001 | CA12 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP |
| 1.1.1.1 / 24078 | RF001 | CA13 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A2, A3, RN1, RN2, RN3 |
| 1.1.1.1 / 24078 | RF001 | CA14 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A4, RN3 |
| 1.1.2.1 / 24115 | RF002 | CA01 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP, A2, A4 |
| 1.1.2.1 / 24115 | RF002 | CA02 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP |
| 1.1.2.1 / 24115 | RF002 | CA03 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP |
| 1.1.2.1 / 24115 | RF002 | CA04 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP |
| 1.1.2.1 / 24115 | RF002 | CA05 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | A2, A3 |
| 1.1.2.2 / 24147 | RF003 | CA01 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP, A1 |
| 1.1.2.2 / 24147 | RF003 | CA02 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | A1 |
| 1.1.2.2 / 24147 | RF003 | CA03 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | A1 |
| 1.1.2.2 / 24147 | RF003 | CA04 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP, A1 |
| 1.1.3.1 / 24170 | RF004 | CA01 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP |
| 1.1.3.1 / 24170 | RF004 | CA02 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A1, RN2 |
| 1.1.3.1 / 24170 | RF004 | CA03 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A2 |
| 1.1.3.1 / 24170 | RF004 | CA04 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP |
| 1.1.3.1 / 24170 | RF004 | CA05 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A2 |
| 1.1.3.1 / 24170 | RF004 | CA06 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A2 |
| 1.1.3.1 / 24170 | RF004 | CA07 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | A2, A4 |
| 1.1.4.1 / 24186 | RF005 | CA01 | [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | A1, A2, A3 |
| 1.1.4.1 / 24186 | RF005 | CA02 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6, A7, A9 |
| 1.1.4.1 / 24186 | RF005 | CA03 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6 |
| 1.1.4.1 / 24186 | RF005 | CA04 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6, A7 |
| 1.1.4.1 / 24186 | RF005 | CA05 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6, A9 |
| 1.1.4.1 / 24186 | RF005 | CA06 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A10 |
| 1.1.4.1 / 24186 | RF005 | CA07 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6, A7, A9, A10, RN4 |
| 1.1.4.1 / 24186 | RF005 | CA08 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A9 |
| 1.1.4.1 / 24186 | RF005 | CA09 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A7 |
| 1.1.4.1 / 24186 | RF005 | CA10 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A7 |
| 1.1.4.1 / 24186 | RF005 | CA11 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A8 |
| 1.1.4.1 / 24186 | RF005 | CA12 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A10 |
| 1.1.5.1 / 24211 | RF006 | CA01 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11 |
| 1.1.5.1 / 24211 | RF006 | CA02 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11 |
| 1.1.5.1 / 24211 | RF006 | CA03 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11 |
| 1.1.5.1 / 24211 | RF006 | CA04 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A12 |
| 1.1.5.1 / 24211 | RF006 | CA05 | [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | A1, A2, A3 |
| 1.1.5.1 / 24211 | RF006 | CA06 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11 |
| 1.1.5.1 / 24211 | RF006 | CA07 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11 |
| 1.1.5.1 / 24211 | RF006 | CA08 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A12 |
| 1.1.6.1 / 24232 | RF007 | CA01 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP |
| 1.1.6.1 / 24232 | RF007 | CA02 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | A1 |
| 1.1.6.1 / 24232 | RF007 | CA03 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | A2 |
| 1.1.6.1 / 24232 | RF007 | CA04 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | A2, A3 |
| 1.1.6.1 / 24232 | RF007 | CA05 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP |
| 1.1.6.1 / 24232 | RF007 | CA06 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP, A1, A2 |
| 1.1.6.1 / 24232 | RF007 | CA07 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP, A2 |
| 1.1.6.1 / 24232 | RF007 | CA08 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP |
| 1.1.6.1 / 24232 | RF007 | CA09 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | A1, A2, RN1, RN2 |
| 1.1.7.1 / 24304 | RF008 | CA01 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP |
| 1.1.7.1 / 24304 | RF008 | CA02 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP |
| 1.1.7.1 / 24304 | RF008 | CA03 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP |
| 1.1.7.1 / 24304 | RF008 | CA04 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP, A1 |
| 1.1.7.1 / 24304 | RF008 | CA05 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP, A2 |
| 1.1.7.1 / 24304 | RF008 | CA06 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP |
| 1.1.7.1 / 24304 | RF008 | CA07 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP |
| 1.1.7.1 / 24304 | RF008 | CA08 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | A3 |
| 1.1.7.1 / 24304 | RF008 | CA09 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP, RN1 |
| 1.1.7.1 / 24304 | RF008 | CA10 | [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | FP, A2, A3 |
| 1.1.7.1 / 24304 | RF008 | CA11 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | A4 |
| 1.1.7.2 / 36153 | RF009 | CA01 | [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | FP, A2, A3 |
| 1.1.7.2 / 36153 | RF009 | CA02 | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | A2 |
| 1.1.7.2 / 36153 | RF009 | CA03 | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | FP |
| 1.1.7.2 / 36153 | RF009 | CA04 | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | FP, A1 |
| 1.1.7.2 / 36153 | RF009 | CA05 | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | A2, A3 |
| 1.1.7.2 / 36153 | RF009 | CA06 | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | FP, A1, RN1 |

RF010 é transversal às nove features; sua verificação é concentrada no UC007.

## Cobertura das 24 US

| Feature | US local | UC | Fluxos |
| --- | --- | --- | --- |
| 1.1.1.1 | US01 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP, A2–A5 |
| 1.1.1.1 | US02 | [UC007](../bvapp/servicos/tests/cenarios/UC007.md) | A1–A3 |
| 1.1.1.1 | US03 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A5 |
| 1.1.2.1 | US01 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | FP |
| 1.1.2.2 | US01 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | A1 |
| 1.1.2.2 | US02 | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | A1 |
| 1.1.3.1 | US01 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A1, A2, A4 |
| 1.1.3.1 | US02 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A2, A4 |
| 1.1.3.1 | US03 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A2, A4 |
| 1.1.3.1 | US04 | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP, A3, A4 |
| 1.1.4.1 | US01 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6 |
| 1.1.4.1 | US02 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6–A8, A10 |
| 1.1.4.1 | US03 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A10 |
| 1.1.4.1 | US04 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A9 |
| 1.1.5.1 | US01 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11–A13 |
| 1.1.5.1 | US02 | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A12 |
| 1.1.6.1 | US01 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | A1 |
| 1.1.6.1 | US02 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | A2, A3 |
| 1.1.6.1 | US03 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP |
| 1.1.6.1 | US04 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP |
| 1.1.6.1 | US05 | [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | FP, A2 |
| 1.1.7.1 | US01 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP, A1, A2 |
| 1.1.7.1 | US02 | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | A3, A4; autorização em UC007 |
| 1.1.7.2 | US01 | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | FP, A1–A3 |

## Regras transversais e rotas

- Nome, descrição, tipo, ativos, periodicidade, datas de cadastro, edição e auditoria: UC001, RN1–RN5.
- Resposta atual, lista vazia, ordenação global e paginação: UC002.
- Interseção, unidades e limites temporais: UC003, RN1/RN2.
- Identidade, relações não excluídas e cálculo único: UC004, RN1/RN2.
- Campos, nomes de arquivos, UTC, formatos e bloqueio de arquivo incompleto: UC005/UC006.
- Permissões efetivas e acesso direto: UC007, RN1.
- Os 11 pares método/rota do backend de serviços em escopo e os dois GET de OS usados como vínculos estão em [rotas.md](rotas.md). A página, os Route Handlers e o backend são distinguidos nesse mapa.

## Pendências e limites de implementação

Os resultados dos fluxos são expectativas. A inspeção local nesta atualização identificou caminhos e parâmetros, sem executar o sistema e sem alterar backend/frontend. Alguns comportamentos exigidos pela revisão ainda dependem de implementação: consistência das validações, IDs de vínculos, datas UTC e próxima execução, auditoria, filtragem de relações excluídas, dias na interface de filtro e envio de ordenação/nome UTC na exportação.

O backend possui PATCH de status e GET de ativos; o frontend examinado atualiza pelo formulário e carrega ativos pela resposta do detalhe. A navegação para OS deve preservar o ID selecionado mesmo se seu controle ainda não estiver concluído. Os cenários descrevem o resultado exigido, sem declarar que essas funções estão prontas.

Manutenção de OS (Mariana), tipos de serviço (Thaty), gráficos (Ryan), geração automática e workers ficam fora. Tipos/ativos são dados de apoio já preparados. Leitura de OS neste conjunto serve apenas aos vínculos de serviços. Não houve alteração do OpenProject, publicação, commit ou envio de mensagens nesta revisão dos arquivos.

O arquivo [cobertura.json](cobertura.json) contém os vínculos estruturados para conferência de completude.
