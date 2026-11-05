# CT-SER-002 — Consultar a listagem

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Conferir os registros e campos da listagem e distinguir resultado vazio de erro de consulta.

## Requisitos relacionados

DOCX, 1.1.2.1 / backlog 24115: CA01–CA05, US01. Regras de dados: Autorização e Resultados vazios e falhas.

## Ator e permissões

U02 autenticado com SERVICO_LISTAR.

## Pré-condições e dados fictícios

Serviços já cadastrados, sem filtros ou busca, página com capacidade para os dois elegíveis. Tipos e ativos da tabela existem e não estão excluídos. Nenhum cadastro será realizado.

| ID | Nome | Tipo | Periodicidade em dias | Ativos | Excluído |
| --- | --- | --- | --- | --- | --- |
| L01 | Ajuste de bancada | Corretiva | 0 | A01 — Bancada | não |
| L02 | Revisão do motor | Preventiva | 7 | nenhum | não |
| L03 | Serviço antigo | Preventiva | 30 | A02 — Motor | sim |

## Fluxo principal

1. U02 acessa a consulta pelo menu. Espera-se que a opção esteja disponível para SERVICO_LISTAR.
2. U02 aguarda a resposta. Esperam-se apenas L01 e L02, inicialmente por nome crescente, e nenhum L03.
3. U02 confere as linhas: L01 deve mostrar Ajuste de bancada, Corretiva, 0 dias e A01 — Bancada; L02 deve mostrar Revisão do motor, Preventiva, 7 dias e vínculo vazio. Não deve ser inventado um ativo para L02. Os IDs identificam a massa, sem impor uma coluna adicional à lista.
4. Em estado preparado com a periodicidade de L02 atualizada para 14 dias antes de nova consulta, U02 consulta novamente. Espera-se 14 dias na nova resposta, sem manter 7 como se fosse o valor atual.

## Fluxos alternativos

| Início | Condição | Resultado e término |
| --- | --- | --- |
| Passo 2 | Base preparada só com L03 excluído | Indicar lista vazia, sem linhas; terminar com consulta vazia bem-sucedida. |
| Passo 2 | Falha interna de consulta preparada | Apresentar erro, sem detalhes internos e sem tratar o erro como ausência de serviços. Linhas anteriores não devem representar uma resposta nova confirmada. Terminar com consulta não confirmada. |

## Regras de negócio

A consulta usa serviços não excluídos e valores da resposta mais recente. Nome, tipo, periodicidade em dias e ativos são campos obrigatórios da apresentação da lista; vínculo ausente não autoriza inventar dados.

## Dados e resultados esperados

Resposta inicial: [L01, L02], com os quatro campos descritos no passo 3. Resposta atualizada: mesmos IDs, L02 com 14 dias. L03 nunca aparece. Lista vazia e erro são estados diferentes.

## Pós-condição

Nenhum registro foi alterado pela consulta. A atualização do passo 4 faz parte do estado preparado, sem executar manutenção neste cenário.
