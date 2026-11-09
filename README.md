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

Cada caso declara sua preparação, com massa fictícia e alternativas independentes. Não é necessário executar outro caso para preparar dados. Exemplos de datas e tamanhos de página não impõem novos padrões ao produto. Rótulos não definidos na fonte são descritos por sua finalidade, sem exigir texto literal inventado.

Os IDs CT-SER identificam cenários e não substituem os IDs de backlog. Alternativas, formatos de arquivo e linhas das tabelas são partes desses dez cenários, sem criar cenários adicionais.

## Material de apoio

- [Rastreabilidade, limites de cobertura e pendências](docs/rastreabilidade.md)

Todos os resultados nos cenários são expectativas para uma execução futura. Um checklist sobre clareza de requisitos não comprova teste aprovado.
