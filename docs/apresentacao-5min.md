# Roteiro de apresentação — 06/11/2026

**Responsável pela elaboração:** Luca Lopes Marques  
**Duração:** cinco minutos. Os trechos abaixo são falas sugeridas. Manter README, CT-SER-001 e rastreabilidade em abas prontas.

## 0:00–0:40 — Meu escopo

**Abrir:** [README.md](../README.md), início e Fonte e escopo.

“Sou Luca Lopes Marques. Minha parte no BVapp é Gestão de Serviços. Nesta atividade N3, preparei dez cenários documentais para verificar manutenção, consultas, filtros e exportações. Usei o documento revisado de requisitos. Não incluí gráficos, manutenção de tipos ou gestão de OS. Os registros apresentados são fictícios. Os cenários ainda não foram executados.”

## 0:40–1:20 — Como navegar

**Abrir:** [README.md](../README.md), Organização e leitura e Índice dos dez cenários.

“A pasta bvapp representa o projeto; servicos representa meu módulo; tests/cenarios guarda os dez arquivos Markdown. A organização foi adaptada para uma entrega documental. Pelo índice, posso abrir qualquer cenário. Cada um declara objetivo, referência aos CA e US da sua feature, permissões, dados iniciais, passos, alternativas e pós-condição. Não preciso executar um cenário anterior para preparar outro. A pasta docs contém a rastreabilidade e este roteiro.”

## 1:20–3:30 — O mesmo ID no CRUD completo

**Abrir:** [CT-SER-001.md](../bvapp/servicos/tests/cenarios/CT-SER-001.md), tabela inicial e Fluxo principal.

**1:20–1:50:** “O serviço começa sem OS. No cadastro, informo nome, descrição, tipo, sete dias e o ativo A01. O sistema deve remover espaços externos e gerar um ID. No roteiro, chamo esse ID de S, porque não devo presumir qual número será gerado. O solicitante vem do usuário e a criação é registrada em UTC.”

**1:50–2:20:** “Na consulta, procuro o mesmo S. Confiro nome, tipo, sete dias, início em primeiro de novembro e próxima execução em oito de novembro. A última realização está ausente. A criação é outra informação, separada do início.”

**2:20–2:55:** “Na edição, continuo com S. Altero nome, descrição, periodicidade para quatorze dias e confirmo Inativo. Depois consulto S novamente: os novos valores devem aparecer e os campos omitidos, como tipo e ativos, devem continuar iguais. A auditoria deve registrar usuário, instante UTC e valores anteriores e novos das mudanças efetivas.”

**2:55–3:30:** “Na exclusão, a confirmação deve identificar S. Como não há OS, espero exclusão lógica, preservando o registro. A nova listagem deve omitir S e os detalhes devem indicar não encontrado. Isso fecha as quatro operações no mesmo cenário e com o mesmo identificador. Se eu cancelar edição ou exclusão, a alternativa informa que o estado persistido deve permanecer.”

## 3:30–4:30 — Por que até OS cancelada impede exclusão

**Continuar em:** [CT-SER-001.md](../bvapp/servicos/tests/cenarios/CT-SER-001.md), massa B01/B02/B03 e última alternativa.

“Para verificar o bloqueio, uso outra massa já preparada, sem criar OS. B01 tem uma OS aberta, B02 uma cancelada e B03 uma excluída logicamente. Nos três casos, o serviço deve permanecer sem exclusão e o sistema deve informar o motivo. A regra revisada considera qualquer vínculo de OS. Uma OS excluída pode não aparecer na consulta dos vínculos, mas ainda impede apagar logicamente o serviço. Essa decisão já está no documento e não é uma dúvida nova nem um resultado de teste que eu executei.”

## 4:30–5:00 — Rastreabilidade e especificação

**Abrir:** [rastreabilidade.md](rastreabilidade.md), tabela Nove features e cobertura especificada.

“A matriz liga as nove features aos cenários e aos CA e US usados. Os CT-SER não substituem os IDs do backlog, e o PDF individual continua sem ID definitivo. Indiquei cobertura parcial quando necessário. Escrever o resultado esperado é especificar o teste; executar seria observar o BVapp e registrar evidências. Aqui houve somente revisão documental. As pendências de código vieram do DOCX, sem serem apresentadas como testes reprovados.”
