# BVapp — Cenários de Gestão de Serviços

**Autor:** Luca Lopes Marques  
**Instituição:** Instituto Federal da Paraíba — IFPB  
**Disciplina:** Verificação, Validação e Testes de Software  
**Atividade:** N3 — mini projeto individual  
**Entrega e apresentação:** 06/11/2026

Esta entrega reúne dez cenários documentais do módulo de Gestão de Serviços do BVapp. Eles descrevem ações e resultados esperados; 

## Organização e leitura

Os cenários funcionais de Gestão de Serviços estão em bvapp/servicos/tests/cenarios/, um arquivo Markdown por cenário. Essa pasta corresponde à finalidade de functional_tests/ no exemplo da Aula 06.

```text
README.md
bvapp/
  servicos/
    tests/
      cenarios/
        CT-SER-001.md ... CT-SER-010.md
docs/
  rastreabilidade.md
```

## Índice dos dez cenários

| Cenário | Objetivo principal |
| --- | --- |
| [CT-SER-001](bvapp/servicos/tests/cenarios/CT-SER-001.md) | Manter serviço em um fluxo CRUD completo |
| [CT-SER-002](bvapp/servicos/tests/cenarios/CT-SER-002.md) | Consultar registros e campos da lista |
| [CT-SER-003](bvapp/servicos/tests/cenarios/CT-SER-003.md) | Ordenar o conjunto antes de paginar |
| [CT-SER-004](bvapp/servicos/tests/cenarios/CT-SER-004.md) | Buscar e combinar filtros por interseção |
| [CT-SER-005](bvapp/servicos/tests/cenarios/CT-SER-005.md) | Filtrar início e última realização |
| [CT-SER-006](bvapp/servicos/tests/cenarios/CT-SER-006.md) | Consultar detalhes, ativos e OS vinculadas |
| [CT-SER-007](bvapp/servicos/tests/cenarios/CT-SER-007.md) | Conferir próxima execução calculada |
| [CT-SER-008](bvapp/servicos/tests/cenarios/CT-SER-008.md) | Exportar toda a lista em CSV e PDF |
| [CT-SER-009](bvapp/servicos/tests/cenarios/CT-SER-009.md) | Exportar somente o serviço escolhido em PDF |
| [CT-SER-010](bvapp/servicos/tests/cenarios/CT-SER-010.md) | Distinguir permissões efetivas de leitura |

Os IDs CT-SER identificam cenários e não substituem os IDs de backlog. Alternativas, formatos de arquivo e linhas das tabelas são partes desses dez cenários, sem criar cenários adicionais.

## Material de apoio

- [Rastreabilidade, limites de cobertura e pendências](docs/rastreabilidade.md)

Todos os resultados nos cenários são expectativas para uma execução futura. Um checklist sobre clareza de requisitos não comprova teste aprovado.