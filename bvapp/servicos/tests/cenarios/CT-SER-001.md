# CT-SER-001 — Manter serviço: CRUD completo

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Verificar criação, consulta, atualização e exclusão lógica acompanhando o mesmo ID gerado, além das alternativas que preservam ou bloqueiam a manutenção.

## Requisitos relacionados

Referências ao documento `BVapp_Gestao_Servicos_Ajustada.docx`. CA e US são locais a cada feature:

| Seção / backlog | CA usados | US usadas |
| --- | --- | --- |
| 1.1.1.1 / 24078 | CA01–CA14 | US01–US03 |
| 1.1.2.1 / 24115 | CA01, CA02, CA04 | US01 |
| 1.1.3.1 / 24170 | CA01–CA03, CA07 | US01 |
| 1.1.4.1 / 24186 | CA01–CA10, CA12 | US01–US04 |
| 1.1.5.1 / 24211 | CA01–CA08 | US01, US02 |

Também se aplicam Regras de dados e tratamento de falhas: Autorização, Nome e descrição, Tipo e ativos, Periodicidade, Datas e próxima execução, Edição e auditoria e Resultados vazios e falhas.

## Ator e permissões

Usuário fictício U01, autenticado, com SERVICO_ADICIONAR, SERVICO_LISTAR, SERVICO_VISUALIZAR, SERVICO_EDITAR e SERVICO_EXCLUIR. O nome do perfil não concede essas permissões.

## Pré-condições e dados fictícios

Ambiente de verificação preparado e isolado, com acesso autorizado à evidência de persistência e auditoria. Não há serviço não excluído chamado `Inspeção bancada N3`. T01 = Preventiva e T02 = Corretiva são tipos existentes, ativos e não excluídos. A01 = Bancada e A02 = Motor são ativos existentes e não excluídos; A02 está inativo e pode ser associado. O fluxo principal não possui OS.

| Campo | Cadastro | Edição principal |
| --- | --- | --- |
| Nome | `  Inspeção bancada N3  ` | Inspeção bancada revisada N3 |
| Descrição | `  Conferir fixações  ` | Conferir fixações e proteção |
| Tipo | T01 | omitido |
| Periodicidade | recorrente, 1 semana = 7 dias | 14 dias |
| Ativos | [A01] | omitido |
| Data de início | 01/11/2026 | omitida |
| Última realização | ausente | omitida |

Para alternativas de duplicidade, existe D01, não excluído, nome `Nome ocupado N3`. Para bloqueio, existem B01, B02 e B03, não excluídos, cada um com apenas uma OS já vinculada: O01 Aberta, O02 Cancelada e O03 excluída logicamente, respectivamente. Nenhuma OS é criada neste cenário. Cada alternativa começa de sua própria cópia do estado indicado.

## Fluxo principal

1. U01 abre o cadastro e preenche a coluna Cadastro. Espera-se que os campos obrigatórios possam ser informados e o ID não seja exigido.
2. U01 salva. Espera-se confirmação do backend antes do sucesso, remoção dos espaços externos de nome e descrição, periodicidade armazenada em 7 dias, solicitante U01 e criação em UTC. Anotar o ID retornado como **S**; nenhum valor fixo deve ser presumido para o ID.
3. U01 consulta a lista e abre o serviço de ID S. Espera-se S na lista e, nos detalhes, nome `Inspeção bancada N3`, descrição `Conferir fixações`, T01, 7 dias, A01 e início 01/11/2026. Registrar o status inicialmente retornado como E0, sem presumir um padrão não definido. Última realização: Não informado; próxima execução: 08/11/2026. A criação deve ser um instante UTC separado do início.
4. U01 edita S com a coluna Edição principal e confirma o status Inativo. Espera-se validação antes da gravação e sucesso somente depois da confirmação. O ID continua S.
5. U01 consulta novamente S. Esperam-se o novo nome, descrição, 14 dias e status Inativo; T01, A01, data inicial, última realização ausente, solicitante e criação permanecem. A próxima execução deve ser 15/11/2026, mesmo estando inativo. Conferir auditoria com S, U01, instante UTC e valores anterior/novo de nome, descrição e periodicidade, além do status se E0 diferir de Inativo. Campos omitidos não devem aparecer como alterações efetivas.
6. U01 solicita remoção de S. Espera-se confirmação identificando S e seu nome, com Confirmar e Cancelar.
7. U01 confirma. Sem OS vinculada, espera-se marcação de excluído, preservação física do registro, sucesso após confirmação e nova consulta da lista com os filtros vigentes.
8. U01 verifica a lista e solicita diretamente os detalhes de S. Espera-se ausência de S na lista e indicação de não encontrado nos detalhes, sem reapresentar os dados antigos como consulta válida.

## Fluxos alternativos

| Início | Ação alternativa | Resultado observável e estado final |
| --- | --- | --- |
| Passo 1 | Omitir nome, descrição, tipo ou periodicidade; enviar texto só com espaços; nome com 151 caracteres; periodicidade negativa ou fracionária; recorrente com zero | Rejeitar e identificar campo/restrição; nenhum novo serviço persistido. Encerrar a tentativa. |
| Passo 1 | Usar tipo inexistente, excluído ou inativo; ativo inexistente/excluído; ativos [A01,A01] | Rejeitar antes de persistir, sem cadastro parcial. A02 inativo, mas não excluído, deve ser aceito em tentativa válida separada. |
| Passo 1 | Nome `  Nome ocupado N3  ` | Após trim coincide com D01: rejeitar duplicidade; D01 intacto e nenhum novo serviço. A comparação distingue maiúsculas de minúsculas; não aplicar a regra da busca à unicidade. |
| Passo 2 | Serviço pontual com zero; ou recorrente com 2 dias, 2 semanas, 2 meses, 2 anos | Em tentativas válidas separadas, esperar 0, 2, 14, 60 e 720 dias. Para pontual, próxima execução Não se aplica. Cada tentativa termina com seu cadastro confirmado, sem executar os passos seguintes. |
| Passo 2 | Omitir ou informar nula a data de início | Usar a data UTC do instante de cadastro; exemplo controlado de 05/11/2026 01:00:00 UTC resulta em início 05/11/2026. Criação mantém o instante, sem confundi-lo com data inicial. Cadastro confirmado encerra a alternativa. |
| Passo 2 | Falha interna de salvamento em ambiente preparado | Informar que o cadastro não foi confirmado, sem detalhes internos ou sucesso. Não assumir persistência; consultar o estado antes de repetir. Encerrar a tentativa. |
| Passos 1, 4 ou 6 | Usuário sem autenticação ou sem a permissão da operação | Negar a operação correspondente; nenhum cadastro, edição ou exclusão deve ser realizado por essa tentativa. |
| Passo 4 | Modificar o formulário e cancelar antes de enviar | Descartar mudanças; S permanece como no passo 3, sem auditoria de alteração concluída. Encerrar antes da exclusão. |
| Passo 4 | Nome duplicado D01 ou dados inválidos das regras do cadastro | Rejeitar edição, preservar integralmente S e seus vínculos; sem auditoria de edição concluída. Encerrar. Manter o próprio nome de S não deve gerar duplicidade consigo mesmo. |
| Passo 4 | Confirmar somente descrição `Revisão parcial`, omitindo os demais campos | Persistir só a descrição; manter nome, tipo, 7 dias, A01, status E0 e datas. Auditoria contém S, U01, instante UTC e descrição anterior/nova. Encerrar após nova consulta de S. |
| Passo 4 | Informar data inicial nula, última realização nula e ativos [] em cópia de S com última realização 05/11/2026 | Manter início 01/11/2026, limpar última realização e remover vínculos. Auditoria registra apenas mudanças efetivas, inclusive IDs de vínculos anterior/novo. Em outras cópias independentes, [A02] substitui [A01], e [A01,A02] mantém dois vínculos válidos. Terminar com S atualizado conforme a lista enviada. |
| Passo 4 | Tipo T01 foi inativado depois do cadastro e o campo é omitido | Manter T01; não rejeitar por um vínculo que não foi substituído. Ativos omitidos preservam A01 por ID; se a interface não tiver IDs, deve consultá-los, sem reconstruí-los por nome. Edição válida termina confirmada. |
| Passo 4 | Confirmar mudança para Ativo em cópia inicialmente Inativa | Persistir Ativo, atualizar a apresentação e registrar a alteração anterior/nova na auditoria. Sem mudança de valor, não há alteração efetiva a registrar. Encerrar. |
| Passo 4 | Falha interna ao editar | Informar alterações não confirmadas, sem sucesso ou detalhes internos. Verificar o estado por consulta antes de repetir; não declarar gravação bem-sucedida. Encerrar. |
| Passo 6 | Cancelar exclusão | Preservar S com os valores do passo 5; continuar visível e acessível. Encerrar sem exclusão. |
| Passo 7 | Usar B01, B02 ou B03 da massa alternativa | Em cada tentativa independente, bloquear pela existência da OS e informar o motivo. Todos permanecem não excluídos, visíveis e com vínculos intactos, inclusive B02 com OS cancelada e B03 com OS excluída logicamente. |

## Regras de negócio

Excluir é marcar logicamente, nunca apagar o registro. Qualquer OS bloqueia a remoção, sem aplicar o filtro de visibilidade das OS ao bloqueio. Nome tem até 150 caracteres após trim; descrição é obrigatória após trim. Tipo substituído deve estar ativo; ativos inativos não excluídos são permitidos. Campos omitidos são preservados. Mensagens são descritas por seu sentido, sem exigir texto literal.

## Dados e resultados esperados

O encadeamento verificável é **criar → S → consultar S → editar S → consultar S → excluir S → não encontrar S**. Nenhuma etapa troca o identificador. Conferir os valores das duas colunas e as exceções da tabela; auditoria depende de alteração efetiva. O acesso à auditoria é preparação de verificação, sem inventar uma tela ou um perfil do produto.

## Pós-condição

No fluxo principal, S está excluído logicamente, preservado na persistência e ausente da consulta e dos detalhes. Cada alternativa termina no estado descrito em sua linha. Nenhum fluxo cria OS.
