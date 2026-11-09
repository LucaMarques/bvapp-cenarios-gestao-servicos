# Rotas e caminhos de Gestão de Serviços

Mapa documental conferido nos arquivos locais em 09/11/2026. A página de entrada do frontend é `/servicos`; cadastro, edição, confirmação e abas de detalhes são abertos dentro dessa página. Não foram inventadas URLs `/servicos/novo` ou `/servicos/{id}/editar`.

Os caminhos `/api/...` são Route Handlers do frontend; `/api/v1/...` são endpoints do backend. `{servico_id}` representa o ID do registro da aplicação e não o ID de requisito ou de work package. Cada método é tratado separadamente. O UC007 concentra autenticação, permissão ausente e tentativas diretas para todas as operações da tabela.

| Método | Backend | Frontend / acesso | Permissão | Caso de uso | Fluxos | Possibilidades documentadas |
| --- | --- | --- | --- | --- | --- | --- |
| POST | `/api/v1/servicos/` | `/api/servicos` | `SERVICO_ADICIONAR` | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | FP; A1–A5 | Cadastro válido, cancelado, inválido, duplicado e falha |
| GET | `/api/v1/servicos/` | `/api/servicos` | `SERVICO_LISTAR` | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) | A4; A2; A3 | Lista sem paginação, vazia e falha |
| GET | `/api/v1/servicos/paginacao` | `/api/servicos/paginacao` | `SERVICO_LISTAR` | [UC002](../bvapp/servicos/tests/cenarios/UC002.md) / [UC003](../bvapp/servicos/tests/cenarios/UC003.md) | UC002 FP/A1–A4; UC003 FP/A1–A4 | Página, ordem, busca, filtros, limites, vazio, entrada inválida e falha |
| GET | `/api/v1/servicos/{servico_id}` | `/api/servicos/{servicoId}` | `SERVICO_VISUALIZAR` | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP; A1; A2; A4 | Detalhe correto, cálculo, ausência e falha |
| PUT | `/api/v1/servicos/{servico_id}` | `/api/servicos/{servicoId}` | `SERVICO_EDITAR` | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A6–A10 | Edição completa/parcial, vínculos, datas nulas, auditoria, cancelamento, inválido, não encontrado e falha |
| DELETE | `/api/v1/servicos/{servico_id}` | `/api/servicos/{servicoId}` | `SERVICO_EXCLUIR` | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A11–A13 | Confirmação, cancelamento, OS impeditiva, exclusão lógica, não encontrado e falha |
| PATCH | `/api/v1/servicos/{servico_id}/status` | Sem Route Handler próprio localizado | `SERVICO_EDITAR` | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A9; A10 | Ativar/inativar, cancelar, sem mudança, não encontrado e falha |
| GET | `/api/v1/servicos/{servico_id}/ativos` | A interface usa o GET de detalhe para a aba de ativos | `SERVICO_VISUALIZAR` | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP; A2; A4 | Ativos vinculados, inativos elegíveis, exclusão, vazio, não encontrado e falha |
| GET | `/api/v1/servicos/{servico_id}/ordens-servico` | `/api/servicos/{servicoId}/ordens-servico` | `SERVICO_VISUALIZAR` | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP; A2; A4 | OS elegíveis, previsão decrescente, vazio, não encontrado e falha |
| GET | `/api/v1/servicos/exportar/{formato}` | `/api/servicos/exportar/{formato}` | `SERVICO_LISTAR` | [UC005](../bvapp/servicos/tests/cenarios/UC005.md) | FP; A1–A4 | PDF/CSV, conjunto completo, ordem/filtros, ausência, formato inválido e falha |
| GET | `/api/v1/servicos/{servico_id}/export` | `/api/servicos/{servicoId}/export` | `SERVICO_VISUALIZAR` | [UC006](../bvapp/servicos/tests/cenarios/UC006.md) | FP; A1–A3 | PDF exclusivo, pontual, relações, não encontrado e falha |
| GET | `/api/v1/ordens_servico/{ordem_de_servico_id}` | `/api/servicos/ordem-servico/{ordemServicoId}` | `SERVICO_VISUALIZAR` | [UC004](../bvapp/servicos/tests/cenarios/UC004.md) | FP; A3; A4 | Somente navegação para OS selecionada; não encontrado e falha |
| GET | `/api/v1/ordens_servico/{ordem_de_servico_id}/ativos` | `/api/servicos/ordem-servico/{ordemServicoId}/ativos` | `SERVICO_VISUALIZAR` | [UC001](../bvapp/servicos/tests/cenarios/UC001.md) | A8 | Somente reflexo dos vínculos atuais do serviço na consulta da OS |

## Parâmetros da consulta

`page`, `page_size`, `order_by`, `order_dir`, `busca`, `tipo_servico_id`, `status`, `ativo_id`, `periodicidade`, `data_inicio_inicio`, `data_inicio_fim`, `data_ultima_realizacao_inicio` e `data_ultima_realizacao_fim` foram identificados na consulta paginada. As exportações de lista devem receber os mesmos filtros e ordenação, sem limitar a seleção à página.

As chaves de ordenação são `nome`, `tipo_servico`, `periodicidade`, `status` e `data_criacao`. No código, `data_criacao` está mapeada para data de início: o título e o significado funcionais permanecem Data de início. Os sentidos técnicos são `asc` e `desc`. As datas de exemplos são apresentadas como DD/MM/AAAA; os parâmetros de data da interface usam AAAA-MM-DD.

## Limites e fontes

- Backend: `bvapp-backend/src/bvapp/api/servicos/servico.py` e os GET de detalhe/ativos em `api/servicos/ordem_servico.py`; parâmetros em `schemas/servicos/servico_schema.py` e ordenação em `services/servicos/servico_service.py`.
- Frontend: `bvapp-frontend/src/app/(dashboard)/servicos/page.tsx`, `src/app/api/servicos/` e `components/features/servicos/servicos-section.tsx`, formulários e wrappers de detalhe.
- A rota PATCH de status existe no backend; não foi localizado Route Handler específico no frontend. A aba de ativos usa a resposta do detalhe, embora o backend também exponha GET de ativos. Isso não cria novos requisitos de tela.
- O cadastro consulta tipos e ativos como dados de apoio. Manutenção desses módulos e indicadores/gráficos não integra estes cenários.
- Rotas externas de OS aparecem apenas para abrir o ID selecionado e conferir o reflexo dos vínculos de ativos. Não se executam manutenção de OS, geração automática ou workers.
- Formato/ordenação inválidos e falhas de leitura/escrita estão como alternativas de robustez das rotas existentes. Não se presume cobertura de toda combinação arbitrária de parâmetros, transporte ou concorrência.
- A leitura do código identifica caminhos; não comprova implementação correta nem substitui execução. Permanecem como expectativas os ajustes definidos na revisão, como dias no filtro, envio da ordenação à exportação, nome UTC, auditoria e consistência das relações.
