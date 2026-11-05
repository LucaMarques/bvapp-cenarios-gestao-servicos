# CT-SER-003 — Ordenar antes de paginar

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Verificar ordenação global por nome e data de início nos dois sentidos, antes da divisão em páginas.

## Requisitos relacionados

DOCX, 1.1.2.2 / backlog 24147: CA01–CA04, US01, US02. Decisões adotadas: Data dos filtros e próxima execução. Cobertura das colunas é parcial: tipo, periodicidade e status não são exercitados aqui.

## Ator e permissões

U03 autenticado com SERVICO_LISTAR.

## Pré-condições e dados fictícios

Quatro serviços existentes e não excluídos; sem filtros. Capacidade de duas linhas por página configurada no ambiente de verificação, como dado do exemplo, sem impor tamanho de página ao produto. Datas de início e criação não coincidem. Ordem de preparação: R01, R02, R03, R04.

| ID | Nome | Data de início | Criação UTC |
| --- | --- | --- | --- |
| R01 | Delta | 01/11/2026 | 04/10/2026 10:00:00 UTC |
| R02 | Alfa | 04/11/2026 | 01/10/2026 10:00:00 UTC |
| R03 | Charlie | 02/11/2026 | 02/10/2026 10:00:00 UTC |
| R04 | Bravo | 03/11/2026 | 03/10/2026 10:00:00 UTC |

## Fluxo principal

1. U03 abre a lista. Espera-se ordenação inicial por nome crescente, com indicação da coluna e sentido.
2. U03 percorre as duas páginas e anota seus IDs. Esperam-se as páginas da linha Nome crescente abaixo.
3. U03 clica novamente no título Nome e percorre as páginas. Espera-se inversão para decrescente e indicação atualizada.
4. U03 seleciona Data de início crescente e percorre as páginas. Espera-se o rótulo Data de início e a sequência da tabela, usando início, sem usar criação.
5. U03 inverte Data de início e percorre as páginas. Espera-se a sequência decrescente da tabela e indicação de sentido.

## Fluxos alternativos

No passo 4, se a coluna estiver em sentido decrescente por uma seleção anterior, selecionar explicitamente crescente antes da conferência; terminar com [R01,R03] / [R04,R02]. Isso evita presumir um sentido ao entrar na coluna. Não há regra nova para desempate: a massa não tem nomes ou datas iniciais iguais.

## Regras de negócio

Ordenar todo o conjunto elegível antes de selecionar a página. A chave interna mencionada no DOCX não muda o significado da coluna: ela representa data de início.

## Dados e resultados esperados

| Ordenação | Página 1 | Página 2 | Sequência completa |
| --- | --- | --- | --- |
| Nome crescente | R02, R04 | R03, R01 | R02, R04, R03, R01 |
| Nome decrescente | R01, R03 | R04, R02 | R01, R03, R04, R02 |
| Início crescente | R01, R03 | R04, R02 | R01, R03, R04, R02 |
| Início decrescente | R02, R04 | R03, R01 | R02, R04, R03, R01 |

Ordenar por criação crescente daria R02,R03,R04,R01, diferente de início crescente. Essa diferença permite detectar a troca indevida de campos. Nenhum registro deve sumir ou se repetir ao percorrer páginas de uma consulta estável.

## Pós-condição

Serviços intactos; apenas coluna, sentido e página da consulta foram selecionados.
