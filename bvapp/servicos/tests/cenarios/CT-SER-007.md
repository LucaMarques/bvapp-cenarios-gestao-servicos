# CT-SER-007 — Conferir a próxima execução

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Conferir a data calculada a partir da última realização ou do início e a apresentação de serviço pontual, sem executar geração automática.

## Requisitos relacionados

DOCX, 1.1.3.1 / backlog 24170: CA02, CA03, US01, com foco no campo próxima execução. Regras de dados: Periodicidade, Datas e próxima execução, Resultados vazios e falhas. Decisões adotadas: Data dos filtros e próxima execução. Cobertura parcial do detalhe.

## Ator e permissões

U07 autenticado com SERVICO_VISUALIZAR, consultando diretamente os IDs preparados.

## Pré-condições e dados fictícios

Os quatro serviços existem e não estão excluídos. Última realização ausente é nula. Criação de todos: 20/10/2026 12:00:00 UTC, distinta do início. Nenhum worker será executado e nenhuma OS será gerada.

| ID / nome | Início | Última realização | Período em dias | Status |
| --- | --- | --- | --- | --- |
| P01 / Revisão inicial | 01/11/2026 | ausente | 7 | Ativo |
| P02 / Revisão realizada | 01/11/2026 | 05/11/2026 | 7 | Ativo |
| P03 / Atendimento pontual | 01/11/2026 | ausente | 0 | Ativo |
| P04 / Revisão inativa | 01/11/2026 | 05/11/2026 | 7 | Inativo |

## Fluxo principal

1. U07 consulta P01. Esperam-se última realização Não informado e próxima execução 08/11/2026: início 01/11 + 7 dias corridos.
2. U07 consulta P02. Espera-se 12/11/2026: última realização 05/11 + 7 dias, sem somar ao início ou à criação.
3. U07 consulta P03. Espera-se próxima execução Não se aplica, sem inventar data para período zero.

## Fluxos alternativos

No passo 2, consultar P04: esperar status Inativo e a mesma data calculada 12/11/2026. Terminar com P04 intacto. A existência da data não deve ser apresentada como prova de elegibilidade ou de geração automática de OS.

## Regras de negócio

Para período positivo, usar última realização quando preenchida; senão, início. Somar dias corridos. Para zero, a data fica ausente e aparece como Não se aplica. Não substituir última realização ausente pelo instante de criação.

## Dados e resultados esperados

| ID | Próxima execução esperada |
| --- | --- |
| P01 | 08/11/2026 |
| P02 | 12/11/2026 |
| P03 | Não se aplica |
| P04 | 12/11/2026 |

## Pós-condição

Nenhum dado alterado e nenhuma OS criada. Os resultados são expectativas de consulta, sem execução de jobs.
