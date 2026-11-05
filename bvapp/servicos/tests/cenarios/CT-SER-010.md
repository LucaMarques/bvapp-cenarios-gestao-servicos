# CT-SER-010 — Distinguir permissões de leitura

**Responsável pela elaboração:** Luca Lopes Marques  
**Situação:** especificado; não executado.

## Objetivo

Comparar permissões efetivas de listagem e visualização, incluindo exportações e acesso não autenticado, sem repetir manutenção.

## Requisitos relacionados

DOCX: 1.1.2.1 / 24115, CA03 e US01; 1.1.3.1 / 24170, US01; 1.1.7.1 / 24304, CA10 e US02; 1.1.7.2 / sem ID definitivo, CA01 e US01. Regras de dados: Autorização. Decisões adotadas: Permissões e exclusão. Cobertura dessas referências limitada à autorização.

## Ator e permissões

Usuários fictícios U10L, autenticado somente com SERVICO_LISTAR, e U10V, autenticado somente com SERVICO_VISUALIZAR; visitante sem autenticação. Nomes de perfis não participam da decisão.

## Pré-condições e dados fictícios

Serviço 1001 = Inspeção N3 existente, não excluído, com dados válidos para consulta e exportação. Mesma massa nas três sessões, independentes e sem permissões adicionais herdadas. O acesso direto ao ID 1001 está disponível para tentar detalhes e PDF sem depender da abertura da lista. Geração de arquivos preparada para sucesso quando autorizada.

## Fluxo principal

1. U10L tenta listar serviços e exportar a lista, separadamente em CSV e PDF. Esperam-se consulta e ambas as exportações autorizadas.
2. U10L tenta abrir diretamente os detalhes de 1001 e seu PDF individual. Espera-se negação em ambas as operações, sem dados ou arquivo individual disponibilizado.
3. U10V tenta listar e exportar a lista nos dois formatos. Espera-se negação nas três tentativas, sem dados de listagem ou arquivo de lista disponibilizado.
4. U10V abre diretamente os detalhes de 1001 e solicita seu PDF individual. Esperam-se detalhes de 1001 e `servico_1001.pdf` após geração bem-sucedida, sem exigir SERVICO_LISTAR para essas operações.
5. Sem autenticação, o visitante tenta as quatro operações da matriz, repetindo a exportação de lista em ambos os formatos. Espera-se negação de todas, sem dados ou arquivos disponibilizados.

## Fluxos alternativos

No passo 2 ou 3, atribuir ao usuário, na massa de autorização preparada, um nome de perfil que aparente maior acesso, mantendo exatamente as permissões efetivas originais. Repetir as operações negadas: esperar as mesmas negativas da matriz. Encerrar sem acesso adicional. Não se presume um perfil real nem se define um nome obrigatório para ele.

## Regras de negócio

Autenticação e permissão da operação são exigidas em conjunto. SERVICO_LISTAR permite lista, filtros e exportação de lista; SERVICO_VISUALIZAR permite detalhes e PDF individual. Uma permissão não implica a outra. Não fixar código HTTP, texto literal ou mecanismo de redirecionamento não especificado.

## Dados e resultados esperados

| Sessão | Listar | Exportar lista CSV/PDF | Abrir detalhes por ID | Exportar PDF individual |
| --- | --- | --- | --- | --- |
| U10L: só SERVICO_LISTAR | permitir | permitir ambos | negar | negar |
| U10V: só SERVICO_VISUALIZAR | negar | negar ambos | permitir | permitir |
| Sem autenticação | negar | negar ambos | negar | negar |

“Permitir” significa receber os dados ou arquivo da operação solicitada quando não há outra falha. “Negar” significa não disponibilizar os dados ou arquivo protegido, mesmo em tentativa de acesso direto.

## Pós-condição

Serviço 1001 intacto e nenhuma manutenção realizada. Cada sessão permanece limitada às suas permissões efetivas.
