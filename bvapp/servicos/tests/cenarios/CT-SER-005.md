# CT-SER-005 — Filtrar por datas

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Separar data de início de última realização e criação, verificando limites inclusivos, limites únicos, intervalo inválido e data ausente.

## Requisitos relacionados

DOCX, 1.1.6.1 / backlog 24232: CA01, CA03, CA04, CA06–CA09, US02, US04, US05. Regras de dados: Datas e próxima execução e Resultados vazios e falhas. Decisões adotadas: Data dos filtros e próxima execução.

## Ator e permissões

U05 autenticado com SERVICO_LISTAR.

## Pré-condições e dados fictícios

Cinco serviços existentes não excluídos; nenhum outro registro. Cada exemplo começa sem filtros, salvo combinação expressa. As criações são propositalmente iguais e externas ao intervalo principal.

| ID | Início | Última realização | Criação UTC |
| --- | --- | --- | --- |
| D01 | 01/11/2026 | 04/11/2026 | 01/10/2026 10:00:00 UTC |
| D02 | 03/11/2026 | 01/11/2026 | 01/10/2026 10:00:00 UTC |
| D03 | 05/11/2026 | 05/11/2026 | 01/10/2026 10:00:00 UTC |
| D04 | 06/11/2026 | ausente | 01/10/2026 10:00:00 UTC |
| D05 | 31/10/2026 | 06/11/2026 | 01/10/2026 10:00:00 UTC |

## Fluxo principal

1. U05 aplica cada linha válida da tabela abaixo, limpando a anterior. Espera-se exatamente o conjunto de IDs indicado, independentemente da ordem.
2. U05 compara os resultados dos dois filtros para o mesmo intervalo 01 a 05/11. Espera-se D01,D02,D03 em ambos por coincidência da massa, e usa o intervalo 03 a 05/11 para distinguir os campos: início D02,D03; última realização D01,D03.
3. U05 combina início de 03 a 06/11 e última realização de 01 a 05/11. Esperam-se somente D02,D03; D04 não tem última realização.

## Fluxos alternativos

| Início | Entrada | Resultado e estado final |
| --- | --- | --- |
| Passo 1 | Início: 05/11/2026 até 01/11/2026 | Identificar intervalo invertido e rejeitar, sem executar consulta com limites trocados ou diferentes. Consulta anterior não representa resultado válido desses parâmetros. Dados intactos. |
| Passo 1 | Última realização: 05/11/2026 até 01/11/2026 | Mesma rejeição, aplicada ao filtro correto. Nenhuma alteração de serviço. |
| Passo 1 | Última realização: 07/11/2026 até 08/11/2026 | Indicar ausência de resultados; D04 não deve entrar por estar sem data. Terminar com consulta vazia confirmada. |

## Regras de negócio

Ambos os limites são inclusivos. Um só limite restringe apenas seu lado. Início usa exclusivamente data de início; última realização usa exclusivamente seu próprio campo. Ausência de última realização não atende a filtro desse campo. Criação não substitui nenhum deles.

## Dados e resultados esperados

Todas as datas abaixo são de 2026; “—” significa limite não preenchido.

| Campo | Limite inicial | Limite final | IDs esperados |
| --- | --- | --- | --- |
| Início | 01/11 | 05/11 | D01,D02,D03 |
| Início | 03/11 | 05/11 | D02,D03 |
| Início | 05/11 | — | D03,D04 |
| Início | — | 01/11 | D01,D05 |
| Última realização | 01/11 | 05/11 | D01,D02,D03 |
| Última realização | 03/11 | 05/11 | D01,D03 |
| Última realização | 05/11 | — | D03,D05 |
| Última realização | — | 01/11 | D02 |
| Nenhum filtro de data | — | — | D01,D02,D03,D04,D05 |

D01 e D03 exercitam os limites do intervalo de início 01 a 05/11; D02 e D03 exercitam os de última realização. A criação em outubro não deve excluir esses registros das consultas de novembro.

## Pós-condição

Nenhum registro alterado; ficam selecionados apenas os parâmetros da última consulta válida realizada.
