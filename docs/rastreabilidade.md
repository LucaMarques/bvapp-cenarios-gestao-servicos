# Rastreabilidade — Gestão de Serviços

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificação documental; cenários não executados.

## Origem das referências

Fonte: `BVapp_Gestao_Servicos_Ajustada.docx`, disponibilizado pelo autor e lido em 05/11/2026. O arquivo não é publicado. A matriz usa exatamente as nove features de 1.1.1 a 1.1.7; identificadores CA/US valem apenas dentro da seção indicada. Intervalos, como CA01–CA04, incluem todos os identificadores entre os extremos.

As referências aos critérios vêm dos blocos `.1. CA` de cada feature. As US vêm dos blocos intitulados US01, US02 etc. dentro da mesma feature. A US01 de cadastro, por exemplo, está em 1.1.1.1.3; as US não devem ser renumeradas a partir do número do cenário.

## Nove features e cobertura especificada

“Cobertura” significa comportamentos previstos no texto dos cenários, sem afirmar implementação ou aprovação em execução. Mesmo quando todos os CA são referenciados, não se presume cobertura exaustiva de combinações, fronteiras e falhas.

| Feature / seção | Backlog | Cenários e CA/US efetivamente usados | Limite de cobertura |
| --- | --- | --- | --- |
| Cadastro / 1.1.1.1 | 24078 | [001](../bvapp/servicos/tests/cenarios/CT-SER-001.md): CA01–CA14; US01–US03 | Parcial: exemplos de obrigatoriedade, normalização, duplicidade, período, vínculos, autorização e falha; não exaure combinações ou fronteiras de entrada. |
| Consulta / 1.1.2.1 | 24115 | [001](../bvapp/servicos/tests/cenarios/CT-SER-001.md): CA01, CA02, CA04; US01. [002](../bvapp/servicos/tests/cenarios/CT-SER-002.md): CA01–CA05; US01. [010](../bvapp/servicos/tests/cenarios/CT-SER-010.md): CA03; US01, foco em permissão. | Campos, exclusão, resposta atual, vazio, falha e autorização especificados; sem execução. |
| Ordenação / 1.1.2.2 | 24147 | [003](../bvapp/servicos/tests/cenarios/CT-SER-003.md): CA01–CA04; US01, US02. [008](../bvapp/servicos/tests/cenarios/CT-SER-008.md): CA01–CA03; US01, US02, uso de nome nos dois sentidos. | Parcial: nome e início com paginação; não exercita colunas tipo, periodicidade e status. |
| Detalhes / 1.1.3.1 | 24170 | [001](../bvapp/servicos/tests/cenarios/CT-SER-001.md): CA01–CA03, CA07; US01. [006](../bvapp/servicos/tests/cenarios/CT-SER-006.md): CA01–CA07; US01–US04. [007](../bvapp/servicos/tests/cenarios/CT-SER-007.md): CA02, CA03; US01, foco em cálculo. [010](../bvapp/servicos/tests/cenarios/CT-SER-010.md): US01, foco em permissão. | Campos, vínculos, navegação, cálculo e falhas descritos; sem manutenção de OS/ativos. |
| Edição / 1.1.4.1 | 24186 | [001](../bvapp/servicos/tests/cenarios/CT-SER-001.md): CA01–CA10, CA12; US01–US04 | Parcial: não verifica CA11, reflexo de alterações dos vínculos atuais nas consultas das OS e preservação de seus demais campos. Sem alterar módulo de OS. |
| Remoção / 1.1.5.1 | 24211 | [001](../bvapp/servicos/tests/cenarios/CT-SER-001.md): CA01–CA08; US01, US02 | Confirmação, cancelamento, exclusão lógica e bloqueio por OS de qualquer estado descritos. |
| Filtragem / 1.1.6.1 | 24232 | [004](../bvapp/servicos/tests/cenarios/CT-SER-004.md): CA01, CA02, CA05–CA09; US01, US03–US05; orientação após US05. [005](../bvapp/servicos/tests/cenarios/CT-SER-005.md): CA01, CA03, CA04, CA06–CA09; US02, US04, US05. [008](../bvapp/servicos/tests/cenarios/CT-SER-008.md): CA01, CA06, CA07, CA09; US05, uso de status e período. | Busca, igualdade, interseção, limpeza e datas descritas; combinações possíveis não são exauridas. |
| Exportação da lista / 1.1.7.1 | 24304 | [008](../bvapp/servicos/tests/cenarios/CT-SER-008.md): CA01–CA11; US01, US02. [010](../bvapp/servicos/tests/cenarios/CT-SER-010.md): CA10; US02, foco em permissão. | Dois formatos, todos os resultados, ordem, campos, nome UTC, vazio, falha e autorização especificados; sem exigir layout visual não definido. |
| PDF individual / 1.1.7.2 | Sem ID definitivo | [009](../bvapp/servicos/tests/cenarios/CT-SER-009.md): CA01–CA06; US01. [010](../bvapp/servicos/tests/cenarios/CT-SER-010.md): CA01; US01, foco em permissão. | Exclusividade, campos, relações, nome, ausências, falha e autorização especificados. NOVO-3.1.10 é referência histórica, sem substituir ID definitivo. |

## Regras transversais usadas

| Bloco do DOCX | Aplicação |
| --- | --- |
| Autorização | 001, 002, 004, 006, 007, 008, 009 e 010: autenticação e permissão efetiva da operação; 003 e 005 usam SERVICO_LISTAR. |
| Nome e descrição; Tipo e ativos; Periodicidade | 001: validação e manutenção; 002/004/008/009: dias e dados de consulta. |
| Datas e próxima execução | 001, 005, 006, 007, 008 e 009: datas independentes, cálculo único, ausência e formatos. |
| Edição e auditoria | 001: campos omitidos, valores nulos, vínculos por ID, registro de mudanças efetivas. |
| Resultados vazios e falhas | 001, 002, 004, 005, 006, 008 e 009: resultado vazio, erro, não encontrado e sucesso confirmado. |
| Exportações | 008 e 009: conjunto exportado, campos, delimitador, nomes e datas. |

## Decisões já resolvidas

- Qualquer OS vinculada bloqueia exclusão, inclusive cancelada ou excluída logicamente. Origem: 1.1.5.1 CA08 e Decisões adotadas — Permissões e exclusão. Consulta de OS pode omitir excluídas; bloqueio de remoção não as ignora.
- A coluna e o filtro usam data de início; criação é um instante separado. Origem: 1.1.2.2 CA01, 1.1.6.1 CA03 e Decisões adotadas — Data dos filtros e próxima execução.
- Próxima execução usa última realização ou, na ausência, início, mais dias corridos. Origem: Regras de dados — Datas e próxima execução.
- Permissão efetiva substitui inferência pelo nome de perfil. Origem: Regras de dados — Autorização.

## Pendências de implementação registradas pela fonte

As notas abaixo resumem “Ajustes que ainda faltam no código” e “Decisões adotadas e evidências no código” do DOCX. São diferenças conhecidas pela análise estática anterior, **não falhas observadas nesta entrega**:

| Pendência relevante | Expectativa afetada |
| --- | --- |
| Uniformizar trim, limites de nome, validação de tipos/ativos/IDs repetidos, recorrência positiva e preservação de IDs | 001 |
| Unificar fórmula de próxima execução, data padrão UTC, created_at no detalhe e auditoria | 001, 006, 007, 008, 009 |
| Harmonizar exclusão em relações aninhadas, rejeitar intervalos invertidos e padronizar dias | 001, 002, 004, 005, 006, 008, 009 |
| Enviar ordenação ao exportar lista e incluir instante UTC no nome; conferir template individual não recebido na análise original | 008, 009 |
| Concluir navegação para a OS selecionada | 006 |
| Registrar no dotProject complementos sem ID definitivo | 1.1.7.2; não inventar ID |

As referências a rotas, schemas e exportadores no DOCX são evidências da revisão anterior. Não foi feita nova inspeção desses arquivos nem execução do sistema. Pendências de gráficos ficam fora desta entrega.
