# BVapp — Cenários de Gestão de Serviços

**Autor:** Luca Lopes Marques  
**Instituição:** Instituto Federal da Paraíba — IFPB  
**Disciplina:** Verificação, Validação e Testes de Software  
**Atividade:** N3 — mini projeto individual  
**Entrega e apresentação:** 06/11/2026

Esta entrega reúne dez cenários documentais do módulo de Gestão de Serviços do BVapp. Eles descrevem ações e resultados esperados; **nenhum cenário foi executado**. A revisão dos arquivos é uma conferência documental, sem execução de testes do BVapp.

## Fonte e escopo

A fonte normativa é `BVapp_Gestao_Servicos_Ajustada.docx`, fornecido pelo autor, especialmente as seções 1.1.1 a 1.1.7, Regras de dados e tratamento de falhas, Decisões adotadas e evidências no código e Ajustes que ainda faltam no código. A numeração e os IDs do backlog foram preservados. CA e US são identificadores locais à respectiva feature: CA01 de cadastro não é CA01 de consulta.

O DOCX e eventuais planilhas não fazem parte da publicação. Nenhuma planilha individual foi fornecida nesta sessão. O código da equipe não foi recebido nem analisado nesta entrega: as pendências citadas vêm da análise estática já registrada no DOCX. Não há aplicação, banco de dados, testes automatizados, credenciais ou dados reais neste repositório.

O escopo inclui cadastro, consulta, ordenação, detalhes, edição, remoção, filtros, exportação da lista e PDF individual. Gráficos (1.1.8, Ryan), manutenção de tipos (Thaty) e gestão de OS (Mariana) ficam fora. Tipos, ativos e OS aparecem somente como dados fictícios de apoio às regras do próprio serviço. Nenhum cenário gera OS ou executa worker.

## Organização e leitura

A estrutura adapta a separação de projeto, módulo e testes para uma entrega documental:

```text
README.md
bvapp/
  servicos/
    tests/
      cenarios/
        CT-SER-001.md ... CT-SER-010.md
docs/
  rastreabilidade.md
  apresentacao-5min.md
  revisao-documental.md
```

A [imagem indicada pelo professor](https://maxwellamaral.github.io/aula-eng-testes/assets/images/06-introducao-tdd/estrutura-pastas.png) foi consultada em 05/11/2026, mas não pôde ser aberta pela ferramenta. O caminho adotado é a alternativa prevista no enunciado, sem alegar reprodução literal da imagem. A organização interna dos cenários segue os campos solicitados para o modelo UC001 — Manter produtos da Aula 06; o material original completo da aula não foi fornecido.

Comece pelo CT-SER-001 para acompanhar o ID gerado nas quatro operações. Depois leia os cenários do comportamento que deseja conferir e a [matriz de rastreabilidade](docs/rastreabilidade.md). Cada arquivo declara seu próprio estado inicial; não é preciso executar um cenário para preparar outro. Massas e IDs são fictícios e locais a cada arquivo.

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
- [Roteiro da apresentação de cinco minutos](docs/apresentacao-5min.md)
- [Conferência documental da entrega](docs/revisao-documental.md)

Todos os resultados nos cenários são expectativas para uma execução futura. Um checklist sobre clareza de requisitos não comprova teste aprovado; decisões desta revisão também não representam aprovação já obtida dos stakeholders.
