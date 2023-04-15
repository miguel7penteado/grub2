# Variáveis de ambiente:

O GRUB oferece suporte a variáveis ​​de ambiente do tipo Unix. Algumas dessas variáveis ​​têm um significado especial para o GRUB.

`color_normal`
Especifique a cor de primeiro plano e a cor de fundo do terminal no caso de "normal", separadas por uma barra, e as seguintes cores são suportadas:

black
blue
green
cyan
red
magenta
brown
light-gray
dark-gray
light-blue
light-green
light-cyan
light-red
light-magenta
yellow
white

O valor padrão é "light-gray/black".

`color_highlight`
Especifique as cores de foreground e background do terminal no caso de "highlight", o mesmo que "color_normal".

`debug`
Essa variável é usada para exibir informações de depuração.

`default`
Define o item de menu selecionado por padrão. Os itens de menu podem ser números (começando em 0) ou IDs de menu.

`enable_progress_indicator`
Defina se deseja exibir o progresso e a velocidade ao ler arquivos. Um valor 0de desativa a exibição do progresso, caso contrário, ativa a exibição do progresso.

NOTA: Este recurso entra em conflito com os temas do modo gráfico, se estiver usando um tema, desative a exibição de progresso e ative-o apenas quando necessário.

*export enable_progress_indicator=0*

`fallback`
Se o item padrão falhar ao iniciar, selecione este item de menu.

`gfxmode`
Define a resolução do terminal "gfxterm". Várias resoluções podem ser especificadas, separadas por vírgulas ou ponto e vírgula, e cada modo deve estar na forma de "auto", "largura x altura" ou "largura x altura x profundidade de cor". ex *set gfxmode=1024x768,640x480,auto*.


`gfxpayload`
Defina o modo de exibição quando o kernel do Linux for iniciado. Se for definido como "text", forçará a entrada no modo caractere, e se for definido como "keep", manterá o mesmo modo de exibição do "gfxmode".

Se você tiver problemas durante a inicialização, tente configurá-lo para "texto".

`grub_build_date`
Data de construção do GRUB.

`grub_cpu`
O tipo de CPU selecionado quando o GRUB foi criado, como "i386", "x86_64", etc.

`grub_detect_floppies`
Defina se a unidade de disquete deve ser detectada no Legacy BIOS. O padrão é 0, que ignora as unidades de disquete.

`grub_disable_console`
Defina se deseja desabilitar o pressionamento da Ctecla para entrar no console do GRUB.

`grub_disable_edit`
Defina se deseja proibir o pressionamento Eda tecla para editar os itens do menu.

`grub_disable_esc`
Defina se deseja desabilitar a tecla *ESC* para retornar ao menu anterior. O padrão é 0, o que permite pressionar ESC para retornar.

`grub_draw_border`
Defina se deseja desenhar a borda do menu. Um valor de 1 desenha a borda do menu.

`grub_enable_menu_hotkey`
Defina se deseja exibir atalhos de menu em itens de menu.

`grub_enable_menu_jump`
Defina se deseja ativar pressionando a tecla *A~Z* para pular para o próximo item de menu correspondente à primeira letra.

`grub_frame_speed`
Taxa de quadros do tema da animação, em milissegundos/quadro, o valor recomendado é 110.

Se esta variável for definida, o recurso de tema dinâmico será ativado.

`grub_fs_case_sensitive`
Defina se o nome do arquivo diferencia maiúsculas de minúsculas. Um valor de 1 torna o nome do arquivo sensível a maiúsculas e minúsculas.

`grub_normal_menu_title`
Especifica o conteúdo de texto do título do menu sem um tema.

`grub_pkg_version`
Número da versão principal do GRUB.

`grub_platform`
O tipo de plataforma selecionado quando o GRUB é criado, como "pc", "efi", "emu" etc.

`grub_prompt`
Prompt de comando do GRUB, o padrão é "grub>".

`grub_sound_speed`
Velocidade de reprodução do som da campainha, em milissegundos/nota, o valor recomendado é 110.

Se esta variável for configurada, a função de reprodução do buzzer será habilitada.

`grub_sound_select`
Personalize os efeitos sonoros das teclas para cima e para baixo para selecionar o menu, "freq1 freq2 freq3 ...", onde freq1, freq2, freq3 ... são frequências em Hertz.

O valor padrão é "880 0 880 0 880 698 1046".

`grub_sound_start`
Personalize o loop para tocar música, na forma de "freq1 freq2 freq3...", onde freq1, freq2, freq3... são frequências em Hertz.

O valor padrão é "220 277 330 440 185 220 277 370 294 370 440 587 330 415 494 659".

`grub_uefi_version`
Versão do firmware UEFI.

`icondir`
Especifica a pasta onde os ícones estão localizados quando o tema é exibido.

`lang`
Defina o código do idioma de localização, como "zh_CN".

`locale_dir`
Defina a pasta onde os arquivos de tradução estão localizados, geralmente "/boot/grub/locale".

`menu_color_highlight`
Especifica as cores do primeiro plano e do plano de fundo dos itens de menu realçados.

`menu_color_normal`
Especifica as cores de primeiro e segundo plano dos itens de menu não realçados.

`pager`
Se for definido como 1, será exibido em páginas e fará uma pausa e aguardará a entrada do teclado.

`prefix`
Especifica o caminho padrão para o carregamento do módulo/tema/menu do GRUB. Esta variável deve ser definida corretamente, caso contrário, o GRUB não funcionará corretamente.

`root`
Especifica o dispositivo raiz. Esta variável deve ser definida corretamente, caso contrário, o GRUB não funcionará corretamente.

`theme`
Define a pasta onde o tema está localizado.

`timeout`
Defina o tempo de espera.

`timeout_style 
Defina o método de temporização "timeout". Se for "contagem regressiva" ou "oculto", o tempo será executado antes da exibição do menu. Se for definido como "menu", o tempo será executado após a exibição do menu.

## configurações variáveis

`set` listar todas as variáveis

`set variable=value`defina o valor da variável

`export variable` tornar variável global

`export variable=value`definir o valor de uma variável global

`unset variable`variável não definida


