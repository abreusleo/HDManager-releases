# HDManager — como instalar e usar

O HDManager mostra para onde foi o espaço do seu disco: quais pastas e arquivos ocupam mais, o que cada pasta é ("o que é isso?") e o que provavelmente sobrou de programas desinstalados, projetos parados e jogos que você não abre há meses. **Ele não apaga nada por conta própria**: na tela **Limpeza** você escolhe quais caches e temporários mandar para a Lixeira (ou apagar de vez), na tela **Duplicados** quais cópias repetidas mandar para a Lixeira, na tela **Programas** quais jogos e programas compactar, e para desinstalar um programa ou jogo ele abre o desinstalador oficial.

## Instalar

1. Baixe o arquivo `HDManager_<versão>_x64-setup.exe` da versão mais nova em https://github.com/abreusleo/HDManager-releases/releases/latest (em **Assets**).
2. O Windows pode mostrar **"O Windows protegeu o computador"** (SmartScreen). Isso acontece porque o app não tem assinatura digital paga. Clique em **Mais informações** e depois em **Executar assim mesmo**.
3. Aceite o pedido de permissão de administrador. Ele aparece na instalação e **toda vez que você abrir o HDManager** — não é só na primeira vez. O app precisa dele para ler o índice do disco (a MFT do NTFS) — é o mesmo método do WizTree e do Everything, e é o que faz a leitura levar segundos em vez de minutos.
   - Se você clicar em **Não**, o Windows simplesmente não abre o app. É o comportamento esperado; abra de novo e aceite.
4. Se o seu Windows não tiver o WebView2 (componente da Microsoft usado pela janela do app), o instalador baixa sozinho.

## Usar

- **Primeira vez:** escolha um disco. Num SSD a leitura leva poucos segundos; num HD ou pendrive, mais.
- **Painel:** a rosca mostra o uso por categoria (Jogos, Apps, Dev, Sistema, Cache…). Os cards mostram órfãos, arquivos esquecidos, lixo de desenvolvimento, jogos não jogados e itens do sistema. Clique num card para ver os itens. O card **Lixeira** mostra quanto ela ocupa e tem **Esvaziar** (o Windows pede a confirmação).
- **Explorador:** árvore à esquerda, visual à direita (Treemap, Sunburst, Por categoria ou **Por tipo**, que soma por extensão: `.mp4`, `.iso`… — clique numa para buscar no disco). Clique duplo entra na pasta; Backspace volta. A faixa de baixo explica o item selecionado e tem **Abrir no Explorer** e **Copiar caminho**; em itens do sistema (memória virtual, pontos de restauração…) também tem o botão que abre a tela certa do Windows.
- **Programas:** programas e jogos instalados, do maior para o menor, com o botão **Desinstalar**. Ele abre o desinstalador do próprio programa, a Steam ou a Epic (para jogos) ou as Configurações do Windows (para programas instalados só para o seu usuário). Anti-cheats (Vanguard, Easy Anti-Cheat…) não têm botão: desinstale pelo jogo. Durante um jogo, nada é desinstalado. Quando termina, aparece quanto espaço foi liberado.
- **Buscar:** `Ctrl K` em qualquer tela. Aceita `*` e `?` (ex.: `*.mp4`) e filtros: `tamanho:>1gb`, `ext:mp4,mkv`, `modificado:<2024`, `modificado:>30d` (há mais de 30 dias), `tipo:pasta`. Com a busca vazia, mostra os 1000 maiores arquivos do disco.
- **Limpeza:** temporários, cache de navegadores e de apps (marcados por padrão), cache de shaders, caches de pacotes de dev e lixo de dev de projetos parados (opcionais). Escolha mandar para a **Lixeira** (dá para desfazer; o espaço volta ao esvaziar a Lixeira) ou **apagar de vez**. Arquivos em uso são pulados e listados. Nada é limpo durante um jogo.
- **Duplicados:** acha arquivos com o mesmo conteúdo nas suas pastas (ou no disco todo), sem olhar jogos, programas, o Windows e o AppData. Compara primeiro o tamanho, depois o começo e o fim, e só lê por inteiro o que empatou; roda em segundo plano, pausa sozinha durante um jogo e não baixa arquivos do OneDrive que estão só na nuvem. Você marca as cópias (ou usa "Manter a mais antiga"/"Manter a mais recente"); sempre fica pelo menos uma, e elas vão para a **Lixeira**.
- **Compactar (tela Programas):** jogos e programas grandes ganham o botão **Compactar**, que usa a compressão do próprio Windows (a mesma do `compact /EXE:XPRESS8K`). É transparente: o jogo abre e roda igual, e o conteúdo dos arquivos não muda. Antes, o app mostra quanto deve liberar (costuma ser de 20% a 50%). Roda em segundo plano, pausa se um jogo abrir e dá para cancelar. Jogos com anti-cheat (Easy Anti-Cheat, BattlEye, Vanguard) pedem uma confirmação a mais. Depois de uma atualização do jogo, os arquivos novos chegam sem compactar: o botão vira **Compactar o resto**. **Descompactar** desfaz tudo.
- **Histórico:** o que cresceu nas últimas 24 h, 7 dias, 30 dias ou desde o início — por categoria e por pasta, com o gráfico do espaço usado. O HDManager guarda uma foto do disco a cada 6 horas enquanto está aberto, então o histórico começa no dia em que você instala. O Painel também mostra "+X GB nos últimos 7 dias".
- **Aviso de pouco espaço:** quando um disco fica com menos de 10% livre (ajuste em Configurações; 0 desliga), o Windows mostra uma notificação, no máximo uma vez por dia — nunca durante um jogo.
- **Exportar CSV:** as listas (busca, filtros, Programas e Insights) têm **Exportar CSV**, que abre no Excel.
- **Voltar e avançar:** os botões laterais do mouse (ou **Alt + ←** e **Alt + →**) voltam e avançam como no navegador, entre telas e entre as pastas do Explorador.
- **● ao vivo:** o índice se atualiza sozinho enquanto você usa o PC. **● estático** quer dizer que o disco não permite isso (pendrive, rede) — use **Reescanear** quando quiser atualizar.

## Jogos e anti-cheat

- No dia a dia, o HDManager só lê nomes, tamanhos e datas dos arquivos. O conteúdo de arquivos só é lido quando você pede: na busca de Duplicados (só nas suas pastas, nunca em jogos) e para Compactar um jogo, sempre com o jogo fechado. Ele nunca abre o processo de um jogo, não instala driver e não lê a memória de nenhum programa.
- Enquanto um jogo está aberto (ou um app em tela cheia), ele entra em **modo jogo**: não começa varreduras completas e quase para o modo ao vivo. A varredura pedida fica "aguardando o jogo fechar". Limpeza, Duplicados e Compactar não começam, e se já estiverem rodando, param ou pausam até o jogo fechar.
- Antes de cada versão ser publicada, ele é validado aberto e escaneando junto com Riot Vanguard e Easy Anti-Cheat.

## Assistente (opcional)

Se você tem o **Claude Code** instalado e logado neste PC, dá para tirar dúvidas em linguagem natural: "como libero 50 GB?", "posso apagar essa pasta?". Ative em **Configurações → Assistente**; aparece um botão de conversa no canto inferior direito. Com uma pasta ou arquivo selecionado no Explorador, a pergunta leva os dados dele junto.

- As perguntas e os dados do disco (nomes, caminhos, tamanhos e categorias) vão para a Anthropic pelo seu Claude Code, usando a sua conta. O conteúdo dos arquivos nunca é enviado.
- O assistente só conversa: ele não apaga, não move e não abre nada.
- Sem o Claude Code, o assistente simplesmente não aparece.

## Privacidade

- O app só se conecta à internet para verificar atualizações (no GitHub) e, se você ativar o assistente, pelo seu Claude Code.
- Tudo o que o app grava fica em `%LOCALAPPDATA%\HDManager` (índice do disco, configurações e logs).

## Atualizações

Quando sair uma versão nova aparece um aviso discreto no canto da janela. Ela só é instalada se você clicar em **Instalar e reiniciar**.

## Desinstalar

Configurações do Windows → **Aplicativos** → **HDManager** → Desinstalar. Para apagar também o índice e os logs, apague a pasta `%LOCALAPPDATA%\HDManager`.

## Deu problema?

Me mande o arquivo de log mais recente da pasta `%LOCALAPPDATA%\HDManager\logs` (cole esse caminho na barra de endereço do Explorer).
