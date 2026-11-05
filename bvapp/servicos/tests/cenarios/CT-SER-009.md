# CT-SER-009 — Exportar um único serviço em PDF

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Conferir que o PDF individual contém exclusivamente o serviço solicitado e suas relações elegíveis, distinguindo não encontrado de falha de geração.

## Requisitos relacionados

DOCX, 1.1.7.2, **sem ID definitivo de backlog**: CA01–CA06, US01. O identificador anterior NOVO-3.1.10 é apenas a referência histórica informada no DOCX, não um ID definitivo. Regras de dados: Exportações, Datas e próxima execução, Resultados vazios e falhas.

## Ator e permissões

U09 autenticado apenas com SERVICO_VISUALIZAR, suficiente para a exportação individual.

## Pré-condições e dados fictícios

Serviços 901 e 902 existentes não excluídos; 903 excluído; 999 inexistente. Não cadastrar, editar ou gerar OS. A01 e A02 não excluídos; A03 excluído.

| Campo | Serviço 901, escolhido | Serviço 902, controle |
| --- | --- | --- |
| Nome | Revisão motor | Limpeza bancada |
| Descrição | Conferir proteção | Limpar superfície |
| Tipo | Preventiva | Corretiva |
| Periodicidade em dias | 7 | 0 |
| Status | Ativo | Inativo |
| Início | 01/11/2026 | 02/11/2026 |
| Última realização | 05/11/2026 | ausente |
| Próxima execução | 12/11/2026 | ausente |
| Ativos vinculados | A01 — Motor; A03 — Painel antigo | A02 — Bancada |

| OS | Serviço | Status | Abertura | Excluída |
| --- | --- | --- | --- | --- |
| O91 | 901 | Aberta | 03/11/2026 | não |
| O92 | 901 | Cancelada | 04/11/2026 | não |
| O93 | 901 | Concluída | 01/11/2026 | sim |
| O94 | 902 | Aberta | 02/11/2026 | não |

## Fluxo principal

1. U09 solicita o PDF individual de 901. Espera-se autorização por SERVICO_VISUALIZAR e uso desse ID, sem exportar a consulta inteira.
2. U09 aguarda a geração. Espera-se download completo somente após confirmação, com nome `servico_901.pdf`.
3. U09 abre o PDF. Esperam-se os valores da coluna 901 para nome, descrição, tipo, periodicidade 7 dias, status, início, última realização e próxima execução, além de A01 e OS O91 e O92.
4. U09 confere as OS do PDF: O91 / Aberta / 03/11/2026 e O92 / Cancelada / 04/11/2026. Espera-se ausência de O93 excluída, A03 excluído e todos os dados exclusivos de 902, incluindo A02 e O94. O requisito individual não define ordenação das OS no arquivo; conferir o conjunto, sem impor a ordenação da tela de detalhes.

## Fluxos alternativos

| Início | Solicitação | Resultado e estado final |
| --- | --- | --- |
| Passo 1 | ID 999 | Informar não encontrado; nenhum PDF gerado. Dados intactos. |
| Passo 1 | ID 903 | Mesmo resultado de não encontrado, pois está excluído. Nenhum PDF. |
| Passo 2 | Falha preparada de geração para 901 | Informar falha sem detalhes internos e sem permitir download incompleto. Nenhum arquivo válido dessa tentativa. |
| Passo 1 | Selecionar 902 em tentativa independente | Gerar somente `servico_902.pdf`, com campos de 902, A02 e O94. Periodicidade zero aparece como Não recorrente; última realização Não informado e próxima execução Não se aplica. Nenhum dado exclusivo de 901 deve aparecer. Terminar com PDF de 902. |

## Regras de negócio

Serviço inexistente ou excluído não gera PDF. Relações excluídas não entram no documento; OS cancelada não excluída entra. Datas presentes usam DD/MM/AAAA. Datas opcionais ausentes usam Não informado; o campo calculado próxima execução de serviço pontual usa Não se aplica, conforme regra específica. Nenhum ID definitivo de backlog é atribuído a esta feature.

## Dados e resultados esperados

Arquivo principal: `servico_901.pdf`, serviço 901, ativos {A01}, OS {O91,O92} com ID, status e abertura da tabela. Controle: 902 não participa desse arquivo. Não se exige criação ou coluna extra não prevista no contrato do PDF individual.

## Pós-condição

Registros intactos. Arquivo completo somente para serviço elegível e geração bem-sucedida; sem arquivo válido nas alternativas de falha ou não encontrado.
