# CT-SER-006 — Consultar detalhes e vínculos

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Conferir a identidade do serviço, seus campos, vínculos elegíveis e a navegação para a OS selecionada, sem manter ativos ou OS.

## Requisitos relacionados

DOCX, 1.1.3.1 / backlog 24170: CA01–CA07, US01–US04. Regras de dados: Autorização, Datas e próxima execução, Resultados vazios e falhas.

## Ator e permissões

U06 autenticado com SERVICO_LISTAR para partir da lista e SERVICO_VISUALIZAR para detalhes, ativos, OS e abertura da OS.

## Pré-condições e dados fictícios

V01, V02 e V04 estão cadastrados e não excluídos; V03 está excluído; V99 não existe. V02 = Limpeza pontual, sem vínculos. V04 = Inspeção da bomba, com os vínculos de controle abaixo. V01 tem os seguintes valores:

| Campo | Valor de V01 |
| --- | --- |
| Nome / descrição / tipo | Revisão motor / Conferir proteção / Preventiva |
| Periodicidade / status | 7 dias / Ativo |
| Início / última realização / próxima execução | 01/11/2026 / 05/11/2026 / 12/11/2026 |
| Criação | 20/10/2026 12:00:00 UTC |

| Registro preparado | Vínculo | Estado | Data prevista |
| --- | --- | --- | --- |
| A01 — Motor | V01 | ativo, não excluído | — |
| A02 — Bancada | V01 | inativo, não excluído | — |
| A03 — Painel antigo | V01 | excluído | — |
| A04 — Bomba | V04 | não excluído, mas sem vínculo com V01 | — |
| O11 | V01 | Aberta, não excluída | 08/11/2026 |
| O12 | V01 | Cancelada, não excluída | 10/11/2026 |
| O13 | V01 | excluída | 12/11/2026 |
| O14 | V04 | não excluída, sem vínculo com V01 | 15/11/2026 |

A04 e O14 pertencem a V04 e servem para provar exclusão de registros alheios. V02 permanece sem vínculos. Não executar criação ou alteração desses registros durante o cenário.

## Fluxo principal

1. U06 localiza V01 e usa sua ação de detalhes. Espera-se que o identificador encaminhado seja V01.
2. U06 confere identificador V01 e todos os campos da primeira tabela. Esperam-se os valores de V01, sem troca pelos de V02, inclusive criação UTC e próxima execução calculada.
3. U06 abre os ativos. Esperam-se somente A01 e A02; inatividade de A02 não significa exclusão. A03 e A04 não aparecem.
4. U06 abre as OS vinculadas. Espera-se [O12,O11], nessa ordem por previsão decrescente. O13 excluída e O14 de outro serviço não aparecem; O12 cancelada continua elegível para consulta.
5. U06 seleciona O11, e não a primeira linha O12. Espera-se abertura dos detalhes de O11, encaminhando esse ID mediante SERVICO_VISUALIZAR. Não editar a OS.

## Fluxos alternativos

| Início | Condição | Resultado e término |
| --- | --- | --- |
| Passo 1 | Abrir V02 na massa sem vínculos | Mostrar V02 e indicar relações de ativos e OS vazias, sem reaproveitar relações de V01. Terminar nos detalhes de V02. |
| Passo 1 | Solicitar V99 ou V03 | Informar serviço não encontrado e não exibir dados de V01 como resposta. Terminar sem detalhes válidos. |
| Passo 2 | Falha preparada na consulta de V01 | Informar erro sem detalhes internos e sem mostrar outro serviço. Terminar com consulta não confirmada. |
| Passo 5 | O11 foi excluída ou deixou de existir antes da abertura, em estado alternativo preparado | Informar OS não encontrada; não abrir O12 no lugar. Terminar sem detalhes válidos de O11. |

## Regras de negócio

Os detalhes usam o ID selecionado. Relações mostram somente vínculos não excluídos; OS são ordenadas por previsão decrescente. A permissão da navegação para OS é a definida no documento, sem especificar manutenção do módulo de OS.

## Dados e resultados esperados

Detalhe: V01 com campos da tabela; ativos {A01,A02}; OS [O12,O11]; destino selecionado O11. A consulta de vínculos exclui O13, mas essa exclusão da apresentação não significa que O13 deixaria de bloquear a remoção do serviço.

## Pós-condição

Serviços, ativos, OS e vínculos permanecem intactos; apenas consultas e navegação foram especificadas.
