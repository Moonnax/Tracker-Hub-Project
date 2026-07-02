
                                        SHOPEE BR — GROUP PRODUCT MANAGEMENT
                                                   PM HUB CHALLENGE
Luana Alves de Oliveira
Product Team - Integrations 
================================================================================

Este ficheiro README.txt foi desenvolvido em conformidade com as regras
do "PM Hub Challenge — One Pager", documentando detalhadamente todas as frentes
do desafio, separado por missões: Lista completa de bugs e prompts (Missão A), a arquitetura do 
sistema multi-usuário (Missão B), o plano de publicação em produção (Missão C),
a expansão do Dashboard (Missão D) e os módulos de acabamento premium (Missão E).

--------------------------------------------------------------------------------
🐛 MISSÃO A: BUG HUNT & UX REFINEMENT (UTILIZANDO AS HEURÍSTICAS DE NIELSEN)
--------------------------------------------------------------------------------

Abaixo encontra-se a listagem dos 36 bugs identificados, mapeados e corrigidos 
no sistema para garantir a eliminação de regressões e a consistência visual:

[DASHBOARD & GRÁFICOS]
01. Tooltip do Heatmap cortado: O pop-up flutuante da primeira linha da tabela ficava oculto sob o cabeçalho.
02. TOTAL do Heatmap ilegível: Texto renderizado em branco sobre fundo claro, violando as regras de contraste.
03. Quebra de linha no Dashboard: Gráficos como "By Status" e "By PM" apresentavam desalinhamentos por falta de indentação estável.
04. Desalinhamento em "Dashboard by Product Line": Barras desalinhadas verticalmente devido ao comprimento irregular dos nomes das categorias.
05. Estouro do texto "Seller Platform": O título empurrava a barra horizontal para fora da viewport. Ajustado para quebrar o texto em múltiplas linhas.
06. Gráfico "By Status" desordenado: Exibido sem critério lógico. Alterado para ordem decrescente de volume, padronizando com os outros gráficos.
07. Truncamento de Tooltip no Heatmap: Mostrava "+more" de forma genérica. Corrigido para indicar a contagem exata de projetos ocultos e link funcional para filtragem.
37. Workload Heatmap com células brancas no dark mode: As células vazias permaneciam brancas mesmo com o tema escuro ativo, quebrando a harmonia visual. A função hC() foi ajustada para retornar var(--bg-card) quando n=0, respeitando o token de cor do tema.

[📁 PROJETOS — ABA PROJECTS]
08. Header da aba Projects desalinhado: Barra de filtros torta e desalinhada em relação ao grid de dados.
09. Alturas inconsistentes no Header: Componentes de filtros, search, selects, botões e headers desalinhados verticalmente. Padronizado com alinhamento centralizado, pading e line-height idênticos.
10. Clique na linha expandindo inline: O clique na linha expandia o conteúdo inline desnecessariamente em vez de abrir o modal de edição de forma direta.
11. Falta de filtro de Favoritos: Existia o componente estético da estrela, mas não havia um filtro funcional para isolar os projetos favoritados.
12. Indicador Global Descontextualizado: O status "Saved 10s ago ✓" ficava fixado estaticamente no header de maneira global e incorreta.
13. Falta de Ordenação por Atualização: Inexistência de um critério de ordenação cronológica para listar projetos modificados recentemente.
38. Estrela (☆) invisível no modo escuro: O ícone de estrela não-selecionada desaparecia completamente no fundo escuro, tornando impossível identificar visualmente o campo de favoritar. Corrigido com opacity e filter CSS para garantir visibilidade como contorno claro sobre qualquer fundo.
39. Badge de notificações da aba "Projects" ilegível no dark mode: O contador numérico da aba Projects herdava fundo escuro no tema escuro. Corrigido para manter fundo claro (#FFF3F0) independentemente do tema ativo.

[📈 RELATÓRIOS — ABA REPORTS]
14. Filtro por status avariado: A seleção do status na aba Reports não atualizava os dados da tabela corretamente.
15. Aba Reports sem filtros estruturados: Inconsistência de UX em relação à aba Projects. Adicionados filtros completos para pesquisas em Reports.
16. Divisão rígida de telas por prioridade: A tela era dividida fixamente em blocos visuais de P0/P1/P2/P3. Esta divisão foi eliminada e convertida em apenas uma opção de filtro selecionável por prioridade (priority).
17. Desalinhamento do Header de Reports: Cabeçalho desalinhado em relação ao padrão estabelecido na aba Projects.
18. Contabilização errada de projetos "Live" no Overdue: Projetos já finalizados (Live) continuavam a ser contados como atrasados caso a data estimada de entrega estivesse no passado.

[📊 WORKLOAD GRAPH]
19. Excesso de vermelho no bloco do Total: Embora o valor estivesse visível, a linha continha um fundo vermelho forte e agressivo. Ajustado para um fundo vermelho claro/sutil em toda a linha, mantendo a fonte vermelha para assegurar excelente legibilidade e contraste.

[📋 BOARD / KANBAN]
20. Drag & Drop quebrado em mobile/touch: O quadro usava eventos nativos dragstart/dragend incompatíveis com ecrãs táteis. Corrigido para suportar interações touch em iOS e Android.
21. Sumiço de projetos por variação de status: Projetos com status ligeiramente fora da lista padrão 'STAGES' desapareciam do quadro. Corrigido para irem para uma coluna de fallback ou gerarem aviso, impedindo o sumiço.
22. Ausência de Estado Vazio: Colunas vazias no Kanban exibiam apenas o texto "Empty" sem qualquer orientação de ação para o utilizador.

[🗺️ ROADMAP & TRATAMENTO DE DATAS — EDGE CASES]
23. Datas e prazos quebrados (—): Datas salvas em formatos comuns não-ISO (como "23/04/26", "Lived on Nov/25" ou "NA") quebravam a função fmtD(), exibindo apenas "—".
24. Overdue Highlight Falso Positivo: Projetos com formatos fora do padrão ou marcados como "NA" geravam NaN em new Date(), marcando os projetos em vermelho como atrasados de forma errada.
25. Sumiço de projetos por localETA inválido: Se apenas o liveETA estivesse preenchido, o cálculo de span quebrava e o projeto sumia por completo da visualização do Roadmap.

[📋 FORMULÁRIOS, VALIDAÇÕES E ESTADO DE CACHE]
26. Bug de Cache ao Criar "New Project": Ao abrir um projeto existente para ler/editar, fechá-lo e imediatamente clicar em "New Project", os dados do PM do projeto anterior continuavam preenchidos por falha de limpeza de estado.
27. Formulário aceitando campos vazios com espaço: O sistema aceitava tarefas e campos obrigatórios preenchidos apenas com espaços em branco. Corrigido com a aplicação do método .trim() para rejeitar inputs invisíveis e destacar os campos inválidos com feedback visual de erro.
28. Falta de feedback visual em erros de formulário: O preenchimento incorreto gerava apenas um toast temporário, sem realçar graficamente o input em falta.
29. Exibição de tags HTML brutas no texto: Atualizações com texto rico renderizavam códigos brutos de programação (como <b>, <strong>, <ul>, <li>) nas notas de lançamento (generateReleaseNotes()).
30. Paleta de Comandos (Ctrl+K) com fechamento inadequado: Ao pressionar a tecla ESC para fechar a paleta de comandos, o código fechava todos os outros modais abertos em segundo plano ao mesmo tempo. Ajustado para isolar o fechamento do modal ativo.

[🔎 MAIS ERROS CORRIGIDOS NO CONTEXTO DA MISSÃO A]
31. Filtro "Starred" não persiste ao trocar de aba: Ao sair de Projects para o Dashboard e voltar, o filtro de favoritos perdia-se.
32. Bug de filtro por PM no Changelog: Ao filtrar por PM na aba Changelog, sair e voltar à aba, a marcação do filtro ficava ativa mas os dados eram recarregados de forma global (sem filtro).
33. Violação da Heurística de Controle do Utilizador (Undo inexistente): Exclusões acidentais de tarefas ou projetos não permitiam reversão. Adicionado mecanismo de "Undo" nos alertas.
34. Navegação móvel inadequada (Scroll Lateral): O menu superior comprimia-se num scroll horizontal desconfortável em mobile. Substituído por um menu hambúrguer responsivo completo.
35. Elemento do Dark Mode quebrando o Header Mobile: O ícone do Dark Mode desalinhava a barra superior em ecrãs pequenos. Corrigido para sumir do cabeçalho no mobile, aparecendo apenas como o último item textual ("Ativar / Desativar Dark Mode") dentro do menu hambúrguer.
36. Listar projetos por última alteração feita: Integração de um seletor funcional na aba de projetos para ordenar a listagem de forma cronológica decrescente a partir da última modificação efetuada.

--------------------------------------------------------------------------------
💬 PROMPTS UTILIZADOS NA MISSÃO A (Preservação do Core & Mapa de Código)
--------------------------------------------------------------------------------

"Você receberá: O arquivo HTML original do PM Hub; O arquivo hubchallengeonepager.html com as regras oficiais; O DOCX contendo a lista de bugs já identificados. Sua tarefa é completar a MISSÃO A integralmente.

PROMPT 1:

OBJETIVO PRINCIPAL: Revisar TODO o sistema visual e funcionalmente. Identificar bugs adicionais além dos listados. Corrigir TODOS os bugs encontrados. Manter 100% das funcionalidades atuais funcionando. Entregar novamente o HTML final funcionando, sem regressões.

REGRA MAIS IMPORTANTE: NENHUMA alteração pode quebrar, remover, simplificar ou alterar funcionalidades já existentes no sistema. O sistema deve continuar funcionando exatamente como antes, manter a mesma lógica original, manter persistência atual, manter o visual original, apenas adicionar/corrigir o que foi pedido. 

NÃO FAÇA: refactors desnecessários; organização estrutural do sistema; troca de arquitetura; mudança de naming; simplificação de lógica existente; reescrita de componentes inteiros sem necessidade; alterações fora do escopo dos bugs e melhorias pedidas.

SINGLE FILE OBRIGATÓRIO: O resultado final deve continuar sendo um único arquivo HTML sem dependências externas novas.

RESTRIÇÕES DE CÓDIGO (OBRIGATÓRIO): Seguir estritamente o "Mapa Frontend ↔ Código" presente no hubchallengeonepager.html. Você DEVE alterar apenas funções marcadas como "Seguro"; alterar funções "Médio" apenas se for realmente necessário; NÃO alterar nenhuma função marcada como "⚠️ Cuidado" ou "⚠️ Não altere". NÃO modificar: saveP(), saveT(), saveTasks(), renderOrgChart(), uid(), renderRoadmap() (exceto se absolutamente inevitável) ou qualquer outra função marcada como "Não altere" ou "Cuidado". Antes de alterar qualquer função: verificar no mapa se ela pode ser modificada; limitar alterações ao menor escopo possível; evitar impactos colaterais.

CRITÉRIOS OBRIGATÓRIOS: Visualmente manter o sistema fiel ao original. Alterar aparência APENAS quando solicitado. Manter alinhamentos consistentes. Garantir responsividade e funcionamento em desktop e mobile. Não gerar regressões. Não remover nenhuma feature existente. Não alterar fluxos já corretos. Preservar localStorage atual e compatibilidade total. [Seguem os dados dos 36 bugs mapeados para execução]"


PROMPT 2: REESTRUTURAÇÃO E RESPONSIVIDADE DE VIEWS

"Se for possível de acordo com as restrições de código do mapa frontend, nesta página de Projects, deixa as opções de visualização 'Table', 'Board' e 'Roadmap' perfeitamente alinhadas com os demais elementos. Caso necessário, indica-me apenas o bloco específico do código CSS/JS que devo mudar para que isso ocorra. Revê todos os bugs da lista consolidada e inspeciona o código para garantir zero regressões. Além disso, no comportamento de responsividade mobile, reposiciona o bloco 'Table/Board/Roadmap' para ficar posicionado acima dos inputs de busca ('search'), filtros de status e seletores, em vez de o manteres espremido de lado."

PROMPT 3: DESIGN DE INTERFACE E DISPOSIÇÃO NO DESKTOP

"Considerando a responsividade e o aproveitamento de ecrã em resoluções comuns de Desktop, a barra de navegação (nav) do header principal deve manter-se na sua posição original, rente à indicação de versão 'v3'. Não alteres este componente de lugar nesta faixa de resolução. Em contrapartida, os símbolos de utilidade localizados no header (Teclado/Atalhos, Cadeado/Login e Lupa/Busca Global) precisam de ser empurrados e fixados de forma alinhada à extrema direita da barra superior."

PROMPT 4: ADOÇÃO DE HEURÍSTICAS DE PADRÕES E COGNIÇÃO

"Os símbolos atualmente utilizados no header para 'Busca Global' e 'Shortcuts Help' violam as heurísticas de padrões e convenções que o cérebro do utilizador reconhece instantaneamente. Ajusta as cores e os ícones para que fiquem visíveis, altamente intuitivos e integrados com a identidade visual do site, seguindo o padrão universal onde o utilizador olha e sabe imediatamente que ali pode tirar dúvidas ou pesquisar. No caso da busca, substitui o botão por um campo de input real do tipo 'search' (caixa de busca típica de sistemas modernos), deixando um espaçamento equilibrado até encostar na nav sem ocupar a largura total. Quanto aos outros dois símbolos, altera-os para elementos gráficos que respeitem o mapeamento mental de plataformas globais consagradas. Tem em consideração que o símbolo de cadeado funcionará como o indicador visual de Login que, na etapa seguinte (Missão B), fará parte do sistema de Multi-Usuário."

--------------------------------------------------------------------------------
👥 MISSÃO B: SISTEMA MULTI-USUÁRIO (L1 E L2)
--------------------------------------------------------------------------------

Explicação da Arquitetura e Solução Baseada em LocalStorage:
A lógica de múltiplos perfis foi acoplada de forma limpa ao arquivo único, respeitando a persistência de dados atual e preservando as chaves globais ('sph_v3', 'sph_team3', 'sph_tasks3').

1. Login e Sessão (🔐):
      - Implementado um modal de login por correspondência de Nome.
      - O nível de acesso (`accessLevel`) é determinado consultando dinamicamente o cadastro do membro na base do Team. Se o nome introduzido não existir, o acesso é bloqueado.
      - Apenas o utilizador "Matheus Mendes" é iniciado na aplicação com privilégios de nível L1. Todos os outros são iniciados como nível L2.
      - A sessão é guardada em `sessionStorage` para reter o utilizador logado durante reloads, contendo um botão funcional de logout.

2. Controle de Acesso por Nível de Liderança (👤):
      - O atributo `accessLevel` (L1 ou L2) foi injetado na estrutura de dados dos membros do Team.
      - Comportamento L1 (Visão Global): Acesso irrestrito a todas as métricas, dashboards, projetos e equipas. Na aba Team, o administrador L1 pode visualizar e alterar o nível de acesso de qualquer membro através de uma secção de dropdown dedicada dentro do modal de edição.
      - Comportamento L2 (Visão Filtrada): Pode apenas visualizar a lista de membros do Team, com a secção de alteração de nível de permissão totalmente escondida e bloqueada.

3. Filtros Massivos e Comportamentos Restritos para L2:
      - Dashboard: Exibe métricas, gráficos e KPIs parametrizados apenas para os projetos sob a responsabilidade direta do PM logado.
      - Contador de Projetos: Atualiza-se dinamicamente para indicar o escopo real do PM L2 (Ex: "8 of 8") ocultando o volume cumulativo global (Ex: "8 of 211").
      - Projects: É aberto por padrão com o filtro rápido aplicado ao nome do PM ativo, contudo, permite que o utilizador remova o filtro manualmente para navegar.
      - Tasks: As funções `renderTasks()` e `renderTaskKanban()` executam uma filtragem imediata através do helper unificado `getVisibleTasks()`. Ao salvar uma nova tarefa (`saveNewTask()`), o sistema sugere/preenche automaticamente o nome do PM logado como owner.
      - Aba "My Tasks" (Exclusiva para L2): Já abre com os dados filtrados e omite os campos de filtro de "Owner" e "PIC" para limpar a UX. O utilizador L1 mantém a visão total com todos os seletores operacionais.
      - Busca Global (Ctrl+K): Corrigido para que usuários L2 vejam apenas os seus próprios projetos nos resultados da palette, sem expor projetos de outros PMs.
      - Changelog: Corrigido para exibir apenas updates dos projetos do PM logado quando o acesso for L2, garantindo privacidade entre membros da equipe.
      - Filtro de PM no Changelog: O seletor "All PMs" fica completamente oculto para L2, que vê apenas o filtro de projeto (seus próprios projetos com updates).

--------------------------------------------------------------------------------
🚀 MISSÃO C: PASSO A PASSO DE PUBLICAÇÃO (DEPLOY)
--------------------------------------------------------------------------------

Plataforma Escolhida: GitHub Pages
Custo Operacional: R$ 0,00 (Totalmente Gratuito)

Tutorial Sequencial de Publicação:
1. Criar o Repositório no GitHub:
      - Entre na sua conta na plataforma GitHub.
      - No painel principal, clique no menu superior direito no ícone "+" e selecione a opção "New repository".
      - Atribua um nome claro para o repositório (Ex: pm-hub-shopee).
      - Defina a visibilidade do repositório obrigatoriamente como "Public" (essencial para aceder ao plano gratuito de hospedagem).
      - Clique em "Create repository".

2. Enviar o Arquivo HTML:
      - Na página raiz do repositório, clique em "Add file" e selecione "Upload files".
      - Arraste o ficheiro HTML consolidado do projeto.
      - CERTIFIQUE-SE de mudar o nome do ficheiro para "index.html". Este passo é obrigatório para que o servidor web o identifique como o ponto de entrada da aplicação.
      - Na parte inferior, adicione uma nota de commit e clique no botão "Commit changes".

3. Ativar o GitHub Pages:
      - No menu superior da página do repositório, aceda à aba "Settings" (Configurações).
      - Na barra lateral esquerda, na secção de automações, clique na opção "Pages".
      - No bloco "Build and deployment", configure os seguintes campos:
          * Source: "Deploy from a branch"
          * Branch: Selecione a branch principal do projeto (geralmente "main")
          * Folder: Mantenha a configuração "/root" (diretório raiz)
      - Clique no botão "Save".

4. Acessar a Aplicação:
      - Aguarde cerca de 30 a 60 segundos para a execução interna do pipeline.
      - Atualize a página ("Settings" -> "Pages"). Um link estável e seguro com HTTPS será disponibilizado num banner no topo da tela, seguindo a estrutura oficial:
          https://<seu-usuario>.github.io/<nome-do-repositorio>/

--------------------------------------------------------------------------------
📊 MISSÃO D: EXPANSÃO E REFINAMENTO DO DASHBOARD
--------------------------------------------------------------------------------

Com o objetivo de tornar o Dashboard um ambiente harmónico e limpo para visualização diária, o painel foi redesenhado limitando a exibição ao teto máximo de 6 gráficos ativos, operando de forma dinâmica com o nível de acesso:

1. Gráficos Novos Adicionados:
      - Gráfico de Pizza (Pie Chart) - "Time Spent in Each Project": Se logado como L2, mostra a distribuição de tempo/esforço individual nos seus projetos. Se logado como L1, transforma-se automaticamente em "Team Time", somando os dados agregados de todas as pessoas.
        Refinamento posterior: o gráfico foi aumentado de 120px para 160px de diâmetro e centralizado na sua célula. A legenda foi reestruturada para eliminar o espaço excessivo entre o nome do projeto e os valores de horas, usando flex com gap controlado.
      - Gráfico de Barras Verticais (Vertical Bar Chart) - "Projects with More Updates": Um ranking vertical que monitoriza e lista os projetos ordenados pelo volume de atualizações registadas no histórico.

2. Alterações e Regras de Exibição por Nível:
      - Gráfico "By Priority": Teve a sua largura horizontal comprimida na interface para ocupar um espaço reduzido na tela, organizando o grid de forma elegante sem alterar o tamanho original das fontes, ícones e colunas de texto.
      - Health Score: Integração de um painel/indicador de saúde discreto avaliando a percentagem de projetos On-Track vs Overdue.
      - Remoções de Segurança para L2: No perfil L2, os gráficos "Workload Heatmap" e "By PM" são COMPLETAMENTE removidos da tela por código, deixando apenas os gráficos permitidos (máximo 4) configurados estritamente com os dados do PM ativo. O utilizador L1 retém o ecossistema completo dos 6 gráficos na tela.

--------------------------------------------------------------------------------
⭐ MISSÃO E: MÓDULOS EXTRAS E ACABAMENTO + RESPONSIVIDADE
--------------------------------------------------------------------------------

Implementações adicionais realizadas utilizando com precisão o Mapa de Funções
para blindar as rotinas de core originais da ferramenta:

1. Sistema de Favoritos Ativado:
      - Integração do filtro funcional que permite fixar, isolar e consultar projetos marcados com a estrela. O filtro permanece retido de forma consistente ao navegar e alternar entre diferentes abas.

2. Filtros Cronológicos de Atualização na Aba Projects:
      - Opção em seletor funcional para ordenar e listar os projetos pelas atualizações mais recentes ("Last Update") ou pelas atualizações mais antigas ("Oldest Update"), facilitando o rastreio imediato de itens estagnados há mais de 14 dias.

3. Painel de Controle de Permissões Injetado no Nível L1:
      - Na aba Team, ao abrir o perfil de edição de cada líder, o usuário de nível L1 ganha um botão dedicado e dropdown funcional para gerenciar e alterar o nível de permissão deles (L1 ou L2) diretamente na interface, persistindo os dados com sucesso no storage.

4. Centralização de Alertas e Exclusão de Redundâncias de Interface:
      - O banner de texto "Admin Mode Active" foi completamente removido e excluído de todos os acessos, eliminando poluição visual redundante em uma página que já possui o título explícito de Dashboard.
      - Substituição por um mecanismo de Notificação Inteligente, discreta e fechável (botão ✕) exibida no momento em que o usuário inicia a sessão, indicando as boas-vindas, o nome de quem efetuou o login e qual nível de acesso (L1 ou L2) está ativo na sessão atual.

5. Filtros Avançados de Pesquisa na Página de Relatórios:
      - Inclusão de um cabeçalho alinhado e estruturado contendo filtros para realizar buscas e pesquisas detalhadas diretamente dentro da aba de "Reports".

6. Recursos Avançados de Comunicação na Página Team (Modais L1 e L2):
      - Cada membro da equipa agora mostra o e-mail corporativo de forma visível, acompanhado de um botão de clique rápido para copiar o endereço para a área de transferência (📋).
      - Inclusão de botão de atalho direto para iniciar chamadas e conversas em tempo real através do Chat SeaTalk (💬) (não realmente conectado, pois os dados cadastrados são dados fictícios).
      - Inclusão de botão de atalho integrado para "Ver Agenda" (📅), que executa a abertura do Google Calendar em uma nova guia, injetando de forma automatizada o e-mail do membro selecionado no campo de busca para agendamento ágil de reuniões.

7. Central de Lembretes — Sino de Notificações (🔔):
      - Ícone de sino adicionado no header, à esquerda do botão de busca, visível para todos os níveis de acesso após login.
      - Badge numérico exibindo a contagem de lembretes com data/hora futura dos projetos visíveis ao usuário logado.
      - Ao clicar, abre um painel inline na mesma página listando cada lembrete com nome do projeto, data, hora e nota associada.
      - Clicar em qualquer item da lista fecha o painel e abre diretamente o modal de edição do projeto correspondente.
      - Resolve a baixa visibilidade dos lembretes, que antes ficavam enterrados dentro do modal de edição de cada projeto individualmente.

8. Botão de Atalho "Quick Update" na Tabela de Projetos:
      - Botão "+ Update" adicionado na coluna de ações de cada projeto na view de tabela, à esquerda do botão "Edit", disponível para todos os níveis de acesso.
      - Abre um popup compacto exibindo o nome do projeto e um campo de texto para o update, com data registrada automaticamente.
      - O update salvo aparece na lista de updates do modal de edição do projeto e no Changelog, idêntico ao fluxo do modal completo.

9. Sistema de Comunicação via Comentários no Changelog:
      - Funcionalidade de comunicação direta entre L1 (GPM) e L2 (PM) vinculada a cada update registrado no Changelog.
      - L1 pode comentar em qualquer update; o comentário aparece apenas no acesso do PM responsável pelo projeto.
      - L2 pode responder ao comentário; L1 recebe e pode continuar o thread. O chat é bidirecional e ilimitado até o L2 encerrar com "✓ Done".
      - Comentários de L1 destacados em laranja; respostas de L2 em azul para leitura clara do fluxo.
      - Cada update exibe uma seta "▶" indicando conteúdo expansível; toda a área do update é clicável para expandir ou minimizar. O painel permanece aberto após envio de mensagens.
      - Dados persistidos dentro do array weeklyUpdates[] de cada projeto via saveP(), sem criar nova chave no localStorage.

10. Filtro por Projeto no Changelog e Botão "View Comments":
      - Nova caixa de seleção "All Projects" no header do Changelog, sincronizada com o filtro de PM: ao selecionar um PM (L1), a lista de projetos se atualiza automaticamente para exibir apenas os projetos daquele PM.
      - Cada update na lista do modal de edição (Projects > Edit > Weekly Updates) ganhou um botão "💬 View Comments" à direita, com contagem de comentários quando existentes. Ao clicar, fecha o modal, navega ao Changelog e aplica automaticamente o filtro do projeto (e do PM, para L1).

--------------------------------------------------------------------------------
⚙️ VALIDAÇÃO E TERMOS DE CONFORMIDADE TÉCNICA
--------------------------------------------------------------------------------
- Assegurado o funcionamento idêntico da persistência de dados em localStorage.
- Nenhuma função protegida ("⚠️ Cuidado" / "⚠️ Não altere") como saveP(), saveT() ou renderOrgChart() foi adulterada, respeitando os riscos listados no mapa frontend.
- Todas as funcionalidades adicionadas em refinamento pós-entrega respeitam as mesmas restrições do Mapa de Funções, sem remover, simplificar ou alterar qualquer funcionalidade existente.
- O arquivo continua sendo um único .html sem dependências externas adicionais.
================================================================================
