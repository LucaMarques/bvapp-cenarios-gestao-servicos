# CT-SER-004 — Buscar e combinar filtros

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Conferir busca parcial normalizada e interseção com tipo, status, ativo e periodicidade, incluindo ausência de resultados e limpeza.

## Requisitos relacionados

DOCX, 1.1.6.1 / backlog 24232: CA01, CA02, CA05–CA09, US01, US03–US05 e orientação após US05 sobre limpar filtros. Regras de dados: Periodicidade e Autorização.

## Ator e permissões

U04 autenticado com SERVICO_LISTAR.

## Pré-condições e dados fictícios

Os sete serviços abaixo já existem e não estão excluídos. T01 e T02 são IDs de tipos existentes, A01 e A02 são IDs de ativos existentes não excluídos. Nenhum vínculo é alterado. Sem outras linhas na consulta; página de duas linhas no ambiente preparado.

| ID | Nome | Tipo ID | Status | Ativo ID | Período em dias |
| --- | --- | --- | --- | --- | --- |
| F01 | Revisão motor | T01 | Ativo | A01 | 7 |
| F02 | REVISÃO bomba | T02 | Ativo | A01 | 7 |
| F03 | Revisão painel | T01 | Inativo | A01 | 7 |
| F04 | Revisão bancada | T01 | Ativo | A02 | 7 |
| F05 | Revisão filtro | T01 | Ativo | A01 | 14 |
| F06 | Limpeza motor | T01 | Ativo | A01 | 7 |
| F07 | Revisão eixo | T01 | Ativo | A01 | 7 |

## Fluxo principal

1. U04 pesquisa `  rEvIsÃo  `. Espera-se remover espaços externos e comparar sem diferenciar maiúsculas de minúsculas, retornando F01,F02,F03,F04,F05,F07 como conjunto.
2. U04 verifica separadamente cada condição da tabela de resultados, limpando as demais antes de cada consulta. Esperam-se os conjuntos isolados indicados abaixo.
3. U04 combina a busca do passo 1 com tipo T01, status Ativo, ativo A01 e periodicidade 7 dias. Esperam-se somente F01 e F07, pois ambos atendem a todas as condições.
4. U04 muda somente a periodicidade da combinação para 99 dias. Espera-se ausência de resultados, sem apresentar as linhas anteriores como resposta dessa busca.
5. U04 limpa busca e todos os filtros. Espera-se nova consulta de todos os sete serviços não excluídos e retorno à primeira página. Com nome crescente, a primeira página deve conter F06 e F04.

## Fluxos alternativos

No passo 3, informar o ID T02 em vez de T01, mantendo as outras condições: esperar somente F02; terminar com consulta filtrada nesse registro. A seleção usa o ID do tipo, não um nome reconstruído. Nenhuma alternativa altera serviços.

## Regras de negócio

Busca é parcial e ignora apenas espaços externos do termo e diferença de caixa. Tipo usa ID; status, ativo e período usam igualdade. A combinação é uma interseção lógica. A regra de busca não muda a comparação de nomes duplicados no cadastro.

## Dados e resultados esperados

Os IDs abaixo expressam conjuntos; a ordem só é verificada no passo 5.

| Condição isolada | IDs esperados |
| --- | --- |
| Nome contém `rEvIsÃo`, após trim | F01,F02,F03,F04,F05,F07 |
| Tipo T01 | F01,F03,F04,F05,F06,F07 |
| Status Ativo | F01,F02,F04,F05,F06,F07 |
| Ativo A01 | F01,F02,F03,F05,F06,F07 |
| Periodicidade = 7 dias | F01,F02,F03,F04,F06,F07 |
| Todas as cinco condições | F01,F07 |
| Todas, mas periodicidade = 99 | nenhum |
| Filtros e busca limpos | F01–F07; primeira página F06,F04 por nome |

## Pós-condição

Dados intactos; ao concluir o fluxo principal a consulta está sem busca e filtros, na primeira página.
