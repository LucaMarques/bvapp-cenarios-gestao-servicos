# BVapp — Casos de uso de Gestão de Serviços

**Autor:** Luca Lopes Marques  
**Instituição:** Instituto Federal da Paraíba — IFPB  
**Disciplina:** Verificação, Validação e Testes de Software

Sete casos de uso documentam os requisitos de Gestão de Serviços, sem repetir cenários equivalentes para completar uma quantidade. Cada arquivo segue o padrão Objetivo, Requisitos, Ator, fluxo principal [FP], alternativas [A1]... e regras [RN1]..., com narrativa de ações do ator e respostas esperadas do sistema.

Os arquivos descrevem expectativas para execução futura. Nenhum cenário foi executado no BVapp e a revisão documental não comprova implementação concluída ou aprovação de stakeholders.

## Requisitos

Os dez requisitos locais estão em [requisitos/requisitos-funcionais.md](requisitos/requisitos-funcionais.md), no formato de histórias de usuário. Contêm objetivos e dados dos formulários; as validações e alternativas detalhadas ficam nos cenários. RF001 a RF010 identificam requisitos desta documentação, não os RF do exemplo de produtos e garantias.

## Casos de uso

| Caso | Objetivo | Requisitos |
| --- | --- | --- |
| [UC001 — Manter serviços](bvapp/servicos/tests/cenarios/UC001.md) | Cadastrar, editar, tratar vínculos, alterar status e remover | RF001, RF005, RF006 |
| [UC002 — Consultar e ordenar](bvapp/servicos/tests/cenarios/UC002.md) | Listar e ordenar pelas cinco colunas antes da paginação | RF002, RF003 |
| [UC003 — Buscar e filtrar](bvapp/servicos/tests/cenarios/UC003.md) | Combinar busca e filtros, validar intervalos e limpar | RF007 |
| [UC004 — Visualizar serviço e relações](bvapp/servicos/tests/cenarios/UC004.md) | Detalhes, próxima execução, ativos, OS e abertura do ID escolhido | RF004 |
| [UC005 — Exportar lista](bvapp/servicos/tests/cenarios/UC005.md) | PDF e CSV do conjunto filtrado e ordenado | RF008 |
| [UC006 — Exportar individual](bvapp/servicos/tests/cenarios/UC006.md) | PDF exclusivo de um serviço e suas relações | RF009 |
| [UC007 — Controlar acesso](bvapp/servicos/tests/cenarios/UC007.md) | Autenticação e permissão efetiva para cada operação | RF010 |

## Cobertura e rotas

- [Rastreabilidade](docs/rastreabilidade.md): nove features, 76 CA, 24 US e responsável primário por verificação.
- [Mapa de rotas](docs/rotas.md): página `/servicos`, caminhos do frontend e métodos/endpoints do backend, com os fluxos que os cobrem.
- [Cobertura estruturada](docs/cobertura.json): referências para conferência documental.

Quando um fluxo precisa alcançar outra função, ele referencia o respectivo caso em vez de copiar suas verificações. PDF/CSV, sentidos de ordenação e variações de entrada são alternativas parametrizadas, sem arquivos duplicados.

## Fonte e limites

A fonte normativa é BVapp_Gestao_Servicos_Ajustada.docx, seções 1.1.1 a 1.1.7 e regras transversais. O modelo UC001 — Manter produtos e os RF de produtos/garantias servem apenas de formato. Os IDs do backlog são preservados; o PDF individual usa #36153, criado na atualização de 06/11/2026. CA e US continuam locais às respectivas features.

Cada caso declara sua preparação, com massa fictícia e alternativas independentes. Não é necessário executar outro caso para preparar dados. Exemplos de datas e tamanhos de página não impõem novos padrões ao produto. Rótulos não definidos na fonte são descritos por sua finalidade, sem exigir texto literal inventado.

Gráficos de Serviço, manutenção de Tipo de Serviço e manutenção de Ordem de Serviço estão fora. As OS aparecem somente nas relações do serviço, no bloqueio de remoção e na abertura do registro selecionado. Nenhum cenário gera OS ou executa workers. O repositório contém documentação, sem credenciais, dados reais, aplicação ou testes automatizados.
