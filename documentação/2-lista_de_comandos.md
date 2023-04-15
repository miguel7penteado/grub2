# Lista de Comandos

`acpi [OPÇÕES] ARQUIVO1 [ARQUIVO2 ...]`

## Carregar tabela ACPI

Os sistemas BIOS modernos geralmente implementam ACPI e definem várias tabelas para descrever a interface entre um sistema operacional e firmware compatível com ACPI. Em alguns casos, as tabelas fornecidas por padrão estão disponíveis apenas em determinados sistemas operacionais, podendo ser necessário substituir algumas delas.

Normalmente, esse comando substituirá o ponteiro de descrição do sistema raiz (RSDP) na área de dados estendida do BIOS para apontar para a nova tabela. Se a opção --no-ebda for usada, apenas o GRUB obtém a nova tabela, mas a emulação EFI do GRUB pode usar a nova tabela.

```bash
# não carrega a lista
--exclude=TABLE1,TABLE2,…, -x 

#lista de carregamento
--load-only=TABLE1,TABLE2,…, -n 

# Importar tabelas da versão 1 para o sistema operacional
--v1, -1 

# Importar as tabelas das versões 2 e 3 para o sistema operacional
--v2, -2 

# definir OEMID para RSDP, XSDT e RSDT
--oemid=STRING, -o 

# set OEMTABLE ID para RSDP, XSDT e RSDT
--oemtable=STRING, -t 

# define a versão OEMTABLE de RSDP, XSDT e RSDT
--oemtablerev=n, -r 

# Define o criador OEMTABLE para RSDP, XSDT e RSDT.
--oemtablecreator=STRING, -c 

# Define a versão do criador OEMTABLE para RSDP, XSDT e RSDT.
--oemtablecreatorrev=n, -d 

# Não atualiza o EBDA. Pode evitar pânico parcial do BIOS, não tem efeito no sistema operacional que não pode receber RSDP do GRUB.
--no-ebda, -e 

# Carrega como SLIC, modifica automaticamente OEMID e OEMTABLE ID.
--slic, -s 

# mostra/carrega tabelas MSDM
--msdm 

# usa arquivo BMP como logotipo de inicialização
--bgrt 
```

`alias NOME COMANDO [RESUMO]`
define um apelido

`appleloader cmdline`
Carregador de boot herdado da Apple.

`authenticate [userlist]`
​ Verifique se o usuário está na lista de usuários ou listado no valor da variável "superusuários"

​ Este comando retorna verdadeiro se "superusuário" estiver vazio.

`background_color COLOR`
​ Defina a cor de fundo do terminal ativo

A cor de fundo só pode ser alterada ao usar "gfxterm". Este comando define a cor da área em branco sem texto, a cor de fundo do texto é controlada pelas variáveis ​​de ambiente color_normal, color_highlight, menu_color_normal, menu_color_highlight.

`background_image [OPTIONS] [FILE]`
​ Defina a imagem de fundo para o terminal ativo

Por padrão, a imagem será esticada para preencher a tela inteira (--mode=stretch)

​ Se não houver nenhum parâmetro, exclua a imagem de fundo atualmente carregada.

--mode=stretch/normal, -m define o modo de imagem de fundo para esticar ou normal

`backtrace`
Imprimir informações de rastreamento

`badram ADDR1,MASK1[,ADDR2,MASK2[,…]]`
Mascarar memória errada

Este comando informa ao gerenciador de memória que a região especificada da RAM deve ser filtrada. Contanto que o kernel carregado obtenha seu mapa de memória do GRUB, ele ainda funcionará depois que o kernel for carregado. Os kernels que suportam esse recurso geralmente incluem Linux, GNU Mach, kernels FreeBSD e kernels de inicialização múltipla.

A sintaxe é a mesma fornecida pelo Memtest86+: uma lista de pares endereço/máscara. Dado um endereço alinhado à página e um par endereço base/máscara, se todos os bits do endereço alinhado à página ativado pela máscara corresponderem ao endereço base, isso significa que a página será filtrada.

`blocklist [OPTIONS] FILE`

Imprimir lista de bloqueio de arquivo

--set=VAR, -s salva na variável
--disk, -d calcula setores iniciais com base em discos em vez de partições

`blscfg FILE`
​ Importar configuração BootLoaderSpec (BLS)

`bls_import FILE`
O mesmo que "blscfg"

`boot`
​ Inicie o sistema operacional carregado

`btrfs-info DEVICE`
Exiba as informações da partição btrfs do dispositivo

`btrfs-mount-subvol DEVICE DIRECTORY SUBVOL`
Defina o diretório DIRECTORY do dispositivo btrfs como o ponto de montagem do subvolume SUBVOL

`btrfs-list-subvols [OPTIONS] DEVICE`
​ Exibir todos os subvolumes no dispositivo DEVICE

--output=VARIÁVEL, -o salva saída como variável
--path-only, -p mostra apenas caminhos para subvolumes
--id-only, -i mostra apenas IDs de subvolume

`btrfs-get-default-subvol [OPTIONS] DEVICE`
Exiba o subvolume padrão no dispositivo DEVICE

Os parâmetros são os mesmos que btrfs-list-subvols

`cat [OPTIONS] FILE`
Exibe o conteúdo do arquivo de texto

--dos permite quebras de linha no formato DOS (CR-LF)
--set=VARIÁVEL, -s salva o conteúdo na variável

`chainloader [–force|–bpb] FILE [ADDR]`
Inicie outro bootloader, o endereço de carregamento padrão é 0x7c00

`chainloader [OPTIONS] FILE CMDLINE`
Inicie o executável EFI

AVISO : Usar este comando pode causar problemas de segurança

--alt, -a usa o carregador EFI integrado do GRUB 2
--text, -t muda para o modo de texto antes de iniciar o EFI
--boot, -b executa a inicialização imediatamente

`checktime minute hour day month day_of_week`
 Verifique se a hora atual atende aos requisitos, se sim, retorne 0, caso contrário, retorne 1. A sintaxe é semelhante ao cron no unix.
 
 | símbolo | significado                                    | exemplo  |
|:-------:|------------------------------------------------|----------|
|    \*   | Qualquer valor (observe o escape do asterisco) | \*       |
|    ,    | listar vários valores                          | 10,20,30 |
|    -    | valor do intervalo                             | 5-45     |
|    /    | valor do passo                                 | 5/10     |

`clear`
Limpa a tela

Nota: Antes de usar este comando, você precisaunset debug

`clear_menu`
Limpar o menu atual

Aviso : certifique-se de desativar o ESC antes de usar este comandoexport grub_disable_esc=1

`cmosclean byte:bit`
Limpe o valor do bit CMOS localizado em byte:bit

Disponível apenas em plataformas que suportam CMOS.

`cmosdump`
Exibir dados brutos CMOS

`cmostest byte:bit`
Teste o valor do CMOS em byte:bit

Retorna verdadeiro (0) se o bit estiver definido, diferente de zero caso contrário.

`cmp FILE1 FILE2`
Comparar dois arquivos

​ Se os tamanhos dos dois arquivos forem diferentes, os tamanhos serão exibidos separadamente. Se o tamanho for o mesmo, mas os dados forem diferentes, exiba a primeira posição e os dados diferentes. Se forem idênticos, não há saída. Um valor de retorno de 0 significa que os arquivos são iguais, caso contrário, os arquivos são diferentes.

--quiet, -q não exibe informações


`commandline`
Digite a linha de comando do GRUB

`configfile FILE`
Carregar o arquivo de configuração do GRUB2

`crc32 FILE [VARIABLE]`
​ Calcule o código de verificação CRC32 do arquivo

`cpuid [OPTIONS] | EAX EAX_VAR EBX_VAR ECX_VAR EDX_VAR`
Detectar características da CPU

​ Se nenhum parâmetro for adicionado, o parâmetro padrão é -l. Retorna 0 se a CPU suportar esse recurso.

--set=VARIÁVEL, -s salva o resultado do teste na variável
--long-mode, -l Verifica se a CPU suporta o modo longo de 64 bits
--pae, -p Verifica se a CPU suporta extensão de endereço físico (PAE)
--vendor, -v obtém o ID do fornecedor da CPU
--vme detecta se a CPU suporta extensões 8086 virtuais
--pse detecta se a CPU suporta extensão de tamanho de página
--tsc Verifica se a CPU suporta TSC
--msr Verifica se a CPU suporta MSR
--mtrr Verifica se a CPU suporta MTRR
--mmx Verifica se a CPU suporta MMX
--sse Verifica se a CPU suporta SSE
--sse2 Verifique se a CPU suporta SSE2
--sse3 Verifica se a CPU suporta SSE3
--vmx detecta se a CPU oferece suporte a extensões de máquina virtual
--vmsign obtém a assinatura da máquina virtual
--hypervisor verifica se a máquina virtual existe
--dts Verifica se a CPU suporta DTS
--emax, -e Obtém o valor máximo de entrada da função estendida que o CPUID pode aceitar
--brand, -b obtém o nome da CPU

`cputemp [VARIABLE]`
Leia a temperatura da CPU (suporta apenas algumas CPUs Intel)

`cryptomount DEVICE | -u UUID | -a | -b`
Monte o dispositivo criptografado (suporte LUKS/geli), em alguns casos é necessário inserir a senha interativamente

--uuid, -u monta dispositivo por UUID
--all, -a monta todos os dispositivos
--boot, -b monta todos os dispositivos marcados com "boot"

`cutmem FROM[K|M|G] TO[K|M|G]`
Exclua todas as regiões de memória dentro do intervalo especificado


`date [OPTIONS] [[year-]month-day] [hour:minute[:second]]`
​ Exibir/ajustar a hora atual

--set=VARIÁVEL, -s economiza tempo para a variável
--human, -h Salvar na variável no formato Kedu

`decrement VARIABLE`
Diminuir o valor de uma variável em um

`devicetree FILE`
Carregar blob da árvore de dispositivos (.dtb)

`dd OPTIONS`
Escreva um arquivo/string/número hexadecimal em um arquivo

AVISO : O USO DESTE COMANDO PODE CAUSAR PERDA DE DADOS

--if=FILE, -i especifica o arquivo de entrada
--str=STRING, -s especifica a string de entrada
--hex=HEX, -h especifica o número hexadecimal de entrada
--of=FILE, -o especifica o arquivo de saída
--bs=BYTES, -b especifica o tamanho do bloco
--count=n, -c especifica o número de blocos
--skip=n pula os primeiros n blocos de entrada
--seek=n pula os primeiros n blocos de saída

`distrust PUBKEY_ID`
 Remova PUBKEY_ID da lista de confiança

`dp FILE/DEVICE`
Dispositivo UEFI Caminho do dispositivo ou arquivo de saída

`drivemap [OPTIONS] FROM_DEVICE TO_DEVICE`
Troque a ordem do disco do BIOS

--list, -l lista os mapeamentos de disco atuais
--reset, -r redefine todos os mapeamentos para os padrões
--swap, -s executa o mapeamento do disco

`dump ADDR [SIZE]`
Exibe o conteúdo da memória

`echo [OPTIONS] STRING …`
seqüência de exibição

​ Se a opção -n não for adicionada, ela será agrupada automaticamente. Os escapes de barra invertida suportam as seguintes sequências:

​ \\ – barra invertida \a – alarme (BEL) \c – suprime nova linha à direita \f – alimentação de formulário

​ \n – nova linha\r – retorno de carro\t – tabulação horizontal \v – tabulação vertical

​ \e0xBF -- define a cor do caractere

-n não envolve automaticamente
-e ativa a análise de escape de barra invertida

`efi-export-env VARIABLE`
Salve a variável GRUB na variável de ambiente EFI GRUB_ENV

AVISO : O uso deste comando modifica as variáveis ​​de ambiente UEFI

`efi-load-env`
Leia as variáveis ​​da variável de ambiente EFI GRUB_ENV

`efiload [OPTIONS] FILE`
Carregar driver UEFI

--nc, -n apenas carrega o driver, não vincula


`efiusb DEVICE`
Imprimir informações USB

`eval STRING …`
concatena argumentos com um único espaço como delimitador e executa o resultado como uma sequência de comandos do GRUB.

`exit`
Sair do GRUB

`export VARIABLE[=VALUE] …`
Defina a variável como uma variável de ambiente global

`expr [OPTIONS] EXPRESSION`
​ Calcular expressões matemáticas, suporte + - * \ % operadores

Aviso : Dividir por zero pode causar condições inesperadas, como congelamentos ou reinicializações

--set=VARIÁVEL, -s salva o resultado na variável

`fakebios`
​ Crie uma estrutura do tipo Legacy-BIOS para compatibilidade com sistemas existentes

`false`
retorna falso

`file OPTIONS FILE`
Detectar tipo de arquivo

--is-i386-xen-pae-domu
--is-x86_64-xen-domu
--is-x86-xen-dom0
--is-x86-multiboot
--is-x86-multiboot2
--is-arm-linux
--is-arm64-linux
--is-ia64-linux
--is-mips-linux
--is-mipsel-linux
--is-sparc64-linux
--is-powerpc-linux
--is-x86-linux
--is-x86-linux32
--is-x86-kfreebsd
--is-i386-kfreebsd
--is-x86_64-kfreebsd
--is-x86-knetbsd
--is-i386-knetbsd
--is-x86_64-knetbsd
--is-i386-efi
--is-x86_64-efi
--is-ia64-efi
--is-arm64-efi
--is-arm-efi
--is-riscv32-efi
--is-riscv64-efi
--is-hibernate-hiberfil
--is-x86_64-xnu
--is-i386-xnu
--is-xnu-hibr
--is-x86-bios-bootsector

`fixmmap`
Corrija o erro "BlInitializeLibrary failed 0xc000009a" ao iniciar o Windows em alguns computadores

`fix_video`
Corrigir problemas de exibição de imagem

`fucksb [OPTIONS]`
Ocultar o estado de inicialização segura do firmware durante a fase do carregador de inicialização. Se não houver parâmetro, retorna se habilita esta função, e retorna 1 se habilitada.

--install, -i habilita o mascaramento
--on, -y disfarça o estado de inicialização segura como on
--off, -n disfarça o estado de inicialização segura como desativado

`fwsetup`
Reinicie para entrar nas configurações de firmware UEFI

`getargs OPTIONS STRING VARIABLE`
Obtenha argumentos da linha de comando recebida do arquivo GRUB 2 EFI

​ Retorna 0 se o comando for executado com sucesso (o parâmetro/valor existe).

--key, -k Obtém se deve definir este parâmetro
--value, -v Obtém o valor do parâmetro

`getenv [OPTIONS] EFI_ENV VARIABLE`
Obtenha variáveis ​​de ambiente UEFI

--guid=GUID, -g Define o GUID da variável a ser consultada, o padrão é uma variável global
--type=string/wstring/uint8/hex, -t especifica o tipo de variável como string/string larga/inteiro não assinado de 8 bits/dados hexadecimais, o padrão é dados hexadecimais

`getkey [-n] [VARIABLE]`
Aguarde uma tecla e emita o código de digitalização do teclado

`gettext STRING`
Traduzir uma string para o idioma atual

O código do idioma atual é armazenado na variável "lang" no ambiente GRUB. Arquivos de tradução no formato MO são lidos de "locale_dir", geralmente /boot/grub/locale.

`gptprio.next OPTIONS [DEVICE]`
 Selecione a próxima partição para inicializar a partir do disco GPT

--set-device=VARIÁVEL, -d salva o nome da partição na variável
--set-uuid=VARIÁVEL, -u salva o UUID da partição na variável

`gptrepair DEVICE`
​ Verifique e repare a tabela de partições GPT do dispositivo

Aviso : usar este comando pode causar perda de dados

`gptsync DEVICE [PARTITION[+/-[TYPE]]] …`
Modifique a tabela de partição compatível com MBR do disco rígido da tabela de partição GPT

TYPE é o código do tipo de partição MBR. "+" significa ativar a partição e "-" significa desativar a partição.

`halt [–no-apm]`
Desligue o computador

​ Se o parâmetro "--no-apm" for adicionado, a chamada do APM BIOS não será executada. Caso contrário, o computador será desligado usando APM.

`hashsum -h HASH [OPTIONS] [-c FILE [-p PREFIX]] [FILE1 [FILE2 …]]`
Calcule ou verifique o valor do hash e retorne 0 se a verificação do hash for bem-sucedida.

--hash=HASH, -h especifica o tipo de valor hash, suporta 'adler32', 'crc64', 'crc32', 'crc32rfc1510', 'crc24rfc2440', 'md4', 'md5', 'ripemd160', 'sha1' , 'sha224', 'sha256', 'sha512', 'sha384', 'tiger192', 'tiger', 'tiger2', 'whirlpool'
--check=FILE, -c especifica o arquivo de lista de hash (gerado usando md5sum no UNIX)
--prefix=PREFIX, -p especifica o diretório do arquivo
--keep-going, -k Não interrompe a inspeção após o primeiro erro e interrompe a inspeção sem esta opção
--uncompress, -u descompacta arquivos antes da validação

`hdparm [OPTIONS] DISK`
Obter/definir parâmetros de disco ATA

--apm=n, -B define o gerenciamento avançado de energia (APM), 1=baixo, ..., 254=alto, 255=desligado
--power, -C mostra o modo de energia
--security-freeze, -F Congela as configurações de segurança do ATA até redefinir
--health, -H mostra o status de integridade SMART
--aam=n, -M define gerenciamento automático de ruído (AAM), 0=desligado, 128=silencioso, ..., 254=rápido
--standby-timeout=n, -S Define o tempo limite de espera, 0=desligado, 1=5s, 2=10s, ..., 240=20m, 241=30m, ...
--standby, -y definido para o modo de espera
--sleep, -Y definido para o modo de suspensão
--identify, -i exibe a identificação e as configurações do dispositivo
--dumpid, -I exibe o conteúdo bruto do setor ATA IDENTIFY
--smart=n desativar/ativar SMART (0/1)
--quiet, -q não exibe informações


`help [PATTERN …]`
Exiba informações de ajuda para comandos integrados. Se nenhum argumento for fornecido, todos os comandos disponíveis serão exibidos.

`hexdump [OPTIONS] FILE/DEVICE [VARIABLE]`
Exiba os dados hexadecimais de um arquivo ou dispositivo. (mem) é o dispositivo de memória.

--skip=n, -s pula os primeiros n bytes
--length=n, -n define o número de bytes lidos
--quiet, -q não imprime a saída

`hiddenentry “TITLE” [OPTIONS] [arg …] { COMMAND; … }`
​ Adicione um menu oculto, válido apenas para gfxmenu

​ Os parâmetros são os mesmos que "menuentry"


`inb [OPTIONS] PORT`
Leia o valor de 8 bits da porta

-v=VARIÁVEL Escreve o valor lido na variável

`increment VARIABLE`
Incrementar o valor de uma variável em um

`ini_get [OPTIONS] FILE [SECTION:]KEY`
Obtenha dados do arquivo ini

--set=VARIÁVEL, -s salva os dados na variável

`initrd FILE …`
Carregue o disco de memória inicial do Linux, usado após o linux

`initrd16 FILE …`
 Carregue o disco de memória inicial do Linux, usado após linux16

`initrdefi FILE`
Carregue o disco de memória inicial do Linux, use-o após o linuxefi

`inl [OPTIONS] PORT`
Leia um valor de 32 bits da porta, os parâmetros são os mesmos que "inb"

`insmod MODULE`
Carregar o módulo GRUB2

`inw [OPTIONS] PORT`
Leia um valor de 16 bits da porta, os parâmetros são os mesmos que "inb"

`isotools OPTIONS FILE [VARIABLE]`
Ferramentas relacionadas à ISO El Torito

--offset, -o deslocamento da imagem UEFI El Torito (em setores)
--length, -l tamanho da imagem UEFI El Torito (em setores)
--ventoy, -v Verifica se a imagem ISO contém informações compatíveis com Ventoy

`keymap FILE`
Carregar layout de teclado

`keystatus [OPTIONS]`
​ Retorna 0 se a tecla Shift/Ctrl/Alt for pressionada

Apenas algumas plataformas suportam a detecção do status da chave modificadora. Se nenhum parâmetro for adicionado, este comando é usado para detectar se o status da chave modificadora é suportado.

--shift, -s detecta tecla shift
--ctrl, -c detecta a tecla Ctrl
--alt, -a detecta a tecla Alt

`kfreebsd [OPTIONS] FILE [CMDLINE]`
​ Carregue o kernel do FreeBSD

`kfreebsd_loadenv FILE`
Carregar variáveis ​​de ambiente do FreeBSD

`kfreebsd_module FILE [CMDLINE]`
Carregando módulos do FreeBSD

`kfreebsd_module_elf FILE [CMDLINE]`
Carregando módulos FreeBSD (ELF)

`knetbsd [OPTIONS] FILE [CMDLINE]`
Carregar o kernel do NetBSD

`knetbsd_module FILE [CMDLINE]`
Carregando módulos do NetBSD

`knetbsd_module_elf FILE [CMDLINE]`
Carregando módulos NetBSD (ELF)

`kopenbsd [OPTIONS] FILE [CMDLINE]`
Carregar o kernel do OpenBSD

`kopenbsd_ramdisk FILE`
​ Monte o ramdisk do OpenBSD

`linuxefi FILE [CMDLINE]`
Carregar o kernel do Linux

`list_env [OPTIONS]`
Liste todas as variáveis ​​no arquivo de bloco do ambiente

--file=FILE, -f especifica o nome do arquivo, o nome do arquivo padrão é ${prefix}/grubenv
--skip-sig, -s ignora a verificação de assinatura de arquivos de ambiente

`list_trusted`
Liste a lista de chaves confiáveis

`load_env [OPTIONS] [VARIABLE …]`
​ Carregue as variáveis ​​do arquivo de bloco do ambiente, os parâmetros são os mesmos de "list_env"

`loadbios BIOS_DUMP [INT10_DUMP]`
Carregar despejo de BIOS

`loadfile [OPTIONS] FILE`
Carregar o arquivo na memória

--skip=n, -k pula n bytes no cabeçalho do arquivo
--length=n, -l especifica o número de bytes a serem lidos
--addr=ADDR, -a especifica o endereço de memória para carregar
--nodecompress, -n não descompacta arquivos automaticamente
--set=VARIÁVEL, -s salva o nome do arquivo de memória na variável

`loopback [OPTIONS] DEVICE FILE`
 Monte o arquivo como um disco virtual

--delete, -d exclui o disco virtual especificado
--mem, -m copia o arquivo para a memória e monta, permite operações de gravação

`ls [OPTIONS] [FILE …]`
listar dispositivos ou arquivos

​ Se não houver parâmetros, todos os dispositivos são listados. Se o argumento for um nome de dispositivo entre parênteses, imprima o nome do sistema de arquivos do dispositivo. Se o argumento for um diretório especificado como um nome de arquivo absoluto, o conteúdo desse diretório será listado.

--long, -l mostra informações mais detalhadas
--legível por humanos, -h exibe o tamanho do arquivo em formato legível por humanos (KB, MB ...)
--all, -a lista todos os arquivos

`lsacpi [OPTIONS]`
Exibir informações ACPI

--v1, -1 mostra apenas tabelas ACPI da versão 1

--v2, -2 mostra apenas as tabelas ACPI das versões 2 e 3

`lspci [OPTIONS]`
Listar dispositivos PCI

--iospace, -i mostra o espaço de E/S

`lsefi`
Mostrar identificador EFI

`lsefienv`
Liste todas as variáveis ​​de ambiente EFI

`lsefimmap`
Mostrar mapa de memória EFI

`lsefisystab`
​ Mostrar tabelas do sistema EFI

`lua [OPTIONS] [FILE]`
Executar script Lua

--execute, -e executa instrução Lua de linha única
--load=NAME, -l carregar biblioteca
--interactive, -i entra no modo interativo
--version, -v exibe informações da versão


`map [OPTIONS] FILE [DEVICE]`
Criar disco virtual UEFI

--mem, -m carrega na memória
--rt especifica RESERVED_MEMORY_TYPEo tipo de
--blocklist, -l converte em disco do tipo lista de bloqueio, isso acelerará a leitura do disco virtual e permitirá a gravação
--type=CD/HD/FD, -t especifica o tipo de disco como CD/HD/FD
--ro, -o desativa a gravação no disco virtual
--eltorito=DISK, -e também especifica a letra da unidade para montar o espelho El Torito
--nb, -n não inicia este disco virtual
--unmap=DISK, -x desmapear um disco
--first, -f torna o disco virtual o primeiro na lista de discos para resolver problemas de inicialização do Windows
--no_g4d, -g não grava informações de mapeamento de disco compatível com GRUB4DOS na memória
--no_vt, -v Não grava informações de compatibilidade do Ventoy


`md5sum arg …`
​ Ou seja, "hashsum –hash md5 arg ..."

`menuentry “TITLE” [OPTIONS] [arg …] { COMMAND; … }`
 Defina o item de menu GRUB, o nome do menu é TITLE

​ Quando o item de menu é selecionado e executado, se --id for especificado, o valor da variável de ambiente escolhida será definido como o valor de --id. Os comandos dentro das chaves serão executados.Se o último comando for executado com sucesso e o kernel tiver sido carregado, o comando boot será executado automaticamente.

Todos os parâmetros (arg ...), incluindo TITLE, serão passados ​​como parâmetros posicionais e TITLE será atribuído a $1.

--class=STRING classifica itens de menu, exibe ícones por diferentes categorias
--users=UESR[,USER] lista usuários com permissão para executar este menu
--hotkey=TECLA definir tecla de atalho
--source=STRING Use STRING como corpo de entrada do menu.
--id=STRING Associa um identificador exclusivo ao item de menu. id não pode começar com um número, apenas alfanuméricos ASCII, sublinhados e hífens são suportados
--unrestricted permite que todos os usuários executem este menu
--help-msg=TEXT definir o texto de ajuda do menu
--hidden ocultar itens de menu
--submenu suporta itens de submenu definidos internamente
Teclas de atalho especiais:

tecla backspace backspace
tabulação tecla tabulação
excluir tecla excluir
inserir inserir chave
tecla de saída esc
teclas de função f1~f12
Você também pode usar códigos-chave na forma de números hexadecimais, por exemplo0x46

`nes FILE [PIXEL_SIZE WAIT_KEY_TIME]`
emulador de NES

`normal [FILE]`
Entre no modo normal e exiba o menu GRUB

No modo normal, comandos, módulos do sistema de arquivos e módulos de criptografia são carregados automaticamente e o analisador de script GRUB completo está disponível. Outros módulos podem ser carregados explicitamente usando insmod.

Se o arquivo for fornecido, os comandos serão lidos desse arquivo. Caso contrário, eles são lidos de $prefix/grub.cfg (se presente).

normal pode ser chamado novamente de dentro do modo normal, criando ambientes aninhados. Para isso, geralmente é usado um arquivo de configuração.

`normal_exit`
Sair do modo normal

Se esta instância normal não estiver aninhada em outra instância, retorne ao modo de recuperação.

`ntboot [OPTIONS] FILE`
Inicie NT6+ VHD/VHDX/WIM

--gui, -g ativa mensagens gráficas de inicialização
--pause, -p pausa antes de iniciar
--vhd, -v especifica o tipo de arquivo como VHD/VHDX
--wim, -w especifica o tipo de arquivo como WIM
--win, -n inicia o Windows no disco
--efi=FILE, -e especifica o caminho bootmgfw.efi, o padrão é /efi/microsoft/boot/bootmgfw.efi
--sdi=FILE, -s especifica o caminho boot.sdi, o padrão é /boot/boot.sdi
--dll=FILE, -d especifica o caminho de bootvhd.dll
--testmode=sim/não modo de teste (testsigning)
--highest=yes/no força a resolução mais alta
--nx=OptIn/OptOut/AlwaysOff/AlwaysOn especifica a política NX
--pae=Padrão/Ativar/Desativar especificar política PAE
--detecthal=sim/não detecta HAL e kernel
--winpe=yes/no inicializa no modo WinPE (/MININT)
--imgoffset=n especifica o deslocamento do disco de memória RamOS VHD
--timeout=n define o tempo limite
--novesa=sim/não desabilita as chamadas VESA BIOS
--novga=sim/não desabilita o modo VGA
--loadoptions=XXX especifica os parâmetros de carregamento do kernel do NT
--winload=\WIN32_PATH especifica o caminho winload
--sysroot=\WIN32_PATH especifica o diretório raiz do sistema

`nthibr FILE`
​ Detecta se o hiberfil.sys do NTFS está em hibernação

`ntversion (hdx,y) VARIABLE`
Obtenha as informações da versão do Windows NT instalado na partição do disco (hdx,y)

`outb PORT VALUE [MASK]`
Escreva um valor de 8 bits na porta

`outl PORT VALUE [MASK]`
​ Escreva um valor de 32 bits na porta

`outw PORT VALUE [MASK]`
Escreva um valor de 16 bits na porta

`partnew OPTIONS DISK PARTNUM`
Crie uma partição primária para o disco da tabela de partições msdos

Aviso : usar este comando pode causar perda de dados

--active, -a ativa a partição
--file=FILE, -f usa arquivo como conteúdo de partição
--type=HEX, -t especifica o tipo de partição, 0x00 é o tipo de partição detectado automaticamente (suporta FAT, exFAT, NTFS, EXT), 0x10 é detectado automaticamente e definido como uma partição oculta.
--start=n, -s especifica o endereço inicial (a unidade é o setor)
--length=n, -l especifica o comprimento (a unidade é o setor)

`parttool PARTITION COMMANDS`
Modifique a tabela de partição (atualmente suporta apenas tabela de partição mbr)

Aviso : usar este comando pode causar perda de dados

​ Cada comando é uma opção booleana, caso em que deve ser seguido de '+' ou '-' (sem espaço intermediário) para habilitar ou desabilitar essa opção, ou então leva um valor no formato 'comando = valor '.

Opções disponíveis:

boot (boolean) Quando ativado, faz com que a partição selecionada seja a partição ativa (inicializável) em seu disco, limpando o sinalizador ativo em todas as outras partições.Este comando é limitado a partições primárias.

type (value) Altera o tipo de uma partição existente.O valor deve ser um número no intervalo 0-0xFF (prefixo com '0x' para digitá-lo em hexadecimal).

hidden (booleano) Quando ativado, oculta a partição selecionada definindo o bit oculto em seu código de tipo de partição; quando desativado, exibe a partição selecionada limpando este bit. Isso é útil apenas ao inicializar o DOS ou o Windows e existem várias partições FAT primárias em um disco.Veja também DOS/Windows.


`password USER clear-password`
​ Defina um usuário chamado user com senha clear-password.

`password_pbkdf2 USER hashed-password`
Defina um usuário chamado user com senha hash hash-password. Use grub-mkpasswd-pbkdf2 para gerar hashes de senha.

`pcidump OPTIONS`
​ mostra um despejo bruto do espaço de configuração PCI

-d [fornecedor]:[dispositivo] seleciona o dispositivo por fornecedor e ID do dispositivo
-s [barramento]:[slot][.func] seleciona o dispositivo com base em sua posição no barramento

`play FILE | TEMPO [PITCH1 DURATION1] [PITCH2 DURATION2] …`
Use o alto-falante do PC para tocar músicas

​ Se o parâmetro for um arquivo, toque a música gravada no arquivo.

`pop_env VARIABLE …`
 Passe as variáveis ​​do submenu para o menu superior

`probe OPTIONS DEVICE`
Informações do equipamento de detecção

--set=VARIÁVEL, -s define o valor de retorno para a variável
--driver, -d detecta driver
--partmap, -p detecta o tipo de tabela de partição
--fs, -f detecta o tipo de sistema de arquivos
--fs-uuid, -u detecta UUID do sistema de arquivos
--label, -l detecta rótulo de volume do sistema de arquivos
--partuuid, -g detecta partição UUID (tabela de partições GPT)
--bootable, -b Verifica flags inicializáveis
--quiet, -q não exibe erros

`rand [OPTIONS] VARIABLE`
Gerar números pseudo-aleatórios

--from=n, -f define o limite inferior do número aleatório
--to=n, -t define o limite superior do número aleatório

`rdmsr [OPTIONS] ADDR`
Leia um registro específico do modelo no endereço ADDR.

Observe que em sistemas SMP, a leitura de um MSR que tem um escopo por encadeamento de hardware implica que o valor retornado se aplica apenas à CPU/núcleo/encadeamento específico que executa o comando.

Além disso, se você especificar um endereço MSR reservado ou não implementado, isso causará uma exceção de proteção geral (que não está sendo tratada no momento) e o sistema será reinicializado.

-v VARIÁVEL salvar valor na variável

`read [VARIABLE] [hide | asterisk]`
Leia uma linha de entrada do usuário

`read_byte [OPTIONS] ADDR`
Leia o valor de 8 bits do ADDR

-v VARIÁVEL salvar valor na variável

`read_dword [OPTIONS] ADDR`
Leia um valor de 32 bits do ADDR, os parâmetros são os mesmos que "read_byte"

`read_file FILE VARIABLE …`
Leia o arquivo e defina o conteúdo do arquivo como uma variável linha por linha

`read_word [OPTIONS] ADDR`
Leia o valor de 16 bits do ADDR, os parâmetros são os mesmos que "read_byte"

`reboot`
Reinicie o computador

`regexp [OPTIONS] ‘REGEXP’ “STRING”`
Testa se a expressão regular REGEXP corresponde à string STRING

As expressões regulares suportadas são expressões regulares estendidas POSIX.2.

Se a opção --set for fornecida, armazene a primeira subexpressão correspondente na variável var. As subexpressões são numeradas a partir de 1 de acordo com seus parênteses de abertura. O número padrão é 1.

--set=[NÚMERO:][VARIÁVEL], -s salva a enésima string correspondente em uma variável

`reset [OPTIONS]`
Reinicie o computador

--shutdown, -s executa o desligamento
--warm, -w executa uma inicialização a quente
--cold, -c executa uma inicialização a frio
--fwui, -f retorna à interface do usuário de configuração do firmware na próxima inicialização

`save_env [OPTIONS] VARIABLE …`
​ Salve as variáveis ​​do ambiente GRUB no arquivo de bloco do ambiente, os parâmetros são os mesmos de "load_env"

`sbpolicy [OPTIONS]`
 Instale uma política de segurança que contorne o Secure Boot. Habilite esse recurso para carregar programas EFI não assinados com inicialização segura habilitada.

AVISO : Usar este comando pode causar problemas de segurança

--install, -i instala política de segurança
--uninstall, -u desinstala a política de segurança
--status, -s mostra o status da política de segurança

`search OPTIONS STRING`
Disco de Pesquisa

--arquivo, -f pesquisa por arquivo
--label, -l pesquisa por rótulo de volume do sistema de arquivos
--fs-uuid, -u pesquisa por UUID do sistema de arquivos
--part-label, -L pesquisa por rótulo de partição
--part-uuid, g busca por partição UUID (GPT)
--disk-uuid, pesquisa U por disco UUID (GPT)
--set=VARIÁVEL, -s salva o primeiro dispositivo encontrado na variável
--no-floppy, -n não detecta disquete
--quiet, -q não mostra erro se não houver correspondência
--hint=HINT, -h Especifica para iniciar a pesquisa de um dispositivo primeiro, se terminar com uma vírgula, também pesquisará subpartições
--hint-ieee1275=DICA Se estiver executando no ambiente IEEE1275, especifique para iniciar a pesquisa de um determinado dispositivo primeiro
--hint-bios=DICA Se estiver executando no ambiente BIOS, especifique para iniciar a pesquisa de um determinado dispositivo primeiro
--hint-baremetal=DICA Se estiver executando no ambiente baremetal, especifique para iniciar a pesquisa de um determinado dispositivo primeiro
--hint-efi=DICA Se estiver executando no ambiente EFI, especifique para iniciar a pesquisa de um determinado dispositivo primeiro
--hint-arc=DICA Se estiver executando no ambiente ARC, especifique para iniciar a pesquisa de um determinado dispositivo primeiro

`serial [OPTIONS]`
Configurar a porta serial

`setenv [OPTIONS] EFI_ENV VALUE`
Escrever variáveis ​​de ambiente UEFI

AVISO : O uso deste comando modifica as variáveis ​​de ambiente UEFI

AVISO : Usar este comando pode causar problemas de segurança

--guid=GUID, -g define o GUID para gravar na variável, o padrão é uma variável global
--type=string/wstring/uint8/hex, -t especifica o tipo de variável como string/string larga/inteiro não assinado de 8 bits/dados hexadecimais, o padrão é dados hexadecimais

`setkey OPTIONS NEW_KEY USA_KEY`
 Mapeie uma tecla (USA_KEY) de um teclado americano para outra tecla (NEW_KEY)

Suporta até 255 conjuntos de relacionamentos de mapeamento ao mesmo tempo.

--reset, -r redefine o relacionamento de mapeamento
--enable, -e habilita o mapeamento de teclas
--disable, -d desativa o mapeamento de teclas
--status, -s mostra o mapa de teclado atual

`setpci [OPTIONS] REGISTER[=VALUE[:MASK]]`
Operar dispositivos PCI

-d [fornecedor]:[dispositivo] seleciona o dispositivo por fornecedor e ID do dispositivo
-s [barramento]:[slot][.func] seleciona o dispositivo com base em sua posição no barramento
-v VARIABLE salvar dados na variável

`setup_var offset [setval]`
Deslocamento (byte) específico de leitura/gravação da variável de configuração.

AVISO : O uso deste comando modifica as variáveis ​​de ambiente UEFI

AVISO : Usar este comando pode causar problemas de segurança

`sha1sum arg …`
Ou seja, "hashsum –hash sha1 arg ..."

`sha256sum arg …`
Ou seja, "hashsum –hash sha256 arg ..."

`sha512sum arg …`
​ Ou seja, "hashsum –hash sha512 arg ..."

`shell [OPTIONS] CMDLINE`
Iniciar Shell UEFI

--nostartup não executa o script de inicialização padrão
--noconsoleout não exibe a saída do terminal
--noconsolein não aceita entrada do usuário
--delay=n define o tempo de espera antes de executar o script de inicialização
--nomap não exibe a lista de mapeamento de dispositivos
--noversion não exibe informações de versão
--startup executa o script de inicialização padrão
--nointerrupt Desabilita a interrupção do processo de execução
--exit Sai automaticamente após a execução do comando
--device=DEVICE especifica o caminho padrão do dispositivo

`sleep [OPTIONS] n`
aguarde n segundos
​ Retorna 0 se a contagem regressiva terminar. Retorna 1 se a contagem regressiva for interrompida por ESC.

--verbose, -v mostra a contagem regressiva dos segundos
--interruptible, -i permite que a contagem regressiva seja interrompida usando ESC

`smbios [OPTIONS]`
Recuperar informações SMBIOS

--type=TYPE, -t Corresponde a estruturas com o tipo fornecido.
--handle=HANDLE, -h Combina as estruturas com o identificador fornecido.
--match=MATCH, -m Selecione uma estrutura quando houver várias correspondências.
--get-byte=OFFSET, -b Obtém o valor do byte no deslocamento fornecido.
--get-word=OFFSET, -w Obtém o valor de dois bytes no deslocamento fornecido.
--get-dword=OFFSET, -d Obtém o valor de quatro bytes no deslocamento fornecido.
--get-qword=OFFSET, -q Obtém o valor de oito bytes no deslocamento fornecido.
--get-string=OFFSET, -s Obtém a string especificada no deslocamento dado.
--get-uuid=OFFSET, -u Obtém o valor do UUID no deslocamento fornecido.
--set=VARIABLE salvar dados na variável

`stat [OPTIONS] FILE`
Exibir informações do arquivo e do sistema de arquivos

--set=VARIÁVEL, -s define o valor de retorno para a variável
--size, -z mostra o tamanho do arquivo
--human, -m exibe tamanhos de arquivo de maneira legível por humanos
--offset, -o mostra o deslocamento do arquivo no disco
--fs, -f exibe informações do sistema de arquivos
--ram, -r mostra o tamanho da memória em MiB
--contig, -c verifica se o arquivo é contíguo
--quiet, -q não imprime a saída

`strconv [OPTIONS] STRING`
Conversão de codificação de string UTF-8/GBK

--gbk, -g UTF-8 -> GBK
--utf8, -u GBK -> UTF-8 (padrão)
--set=VARIÁVEL, -s define o valor de retorno para a variável

`submenu “TITLE” [OPTIONS] { MENU … }`
 Defina um submenu. Quando este item for selecionado e executado, um novo menu contendo os itens do menu entre chaves será exibido

​ Os parâmetros são os mesmos que "menuentry"

`submenu_exit`
​ Sair do submenu atual

`terminfo [OPTIONS] [TERM]`
Definir tipo de terminal

`test EXPRESSION`
 Calcula uma expressão, retorna zero se o resultado for verdadeiro, caso contrário, retorna um status diferente de zero

Suporta as seguintes expressões

sequência1 ==sequência2

as cordas são iguais

sequência1 !=sequência2

as cordas não são iguais

sequência1 <sequência2

string1 é lexicograficamente menor que string2

sequência1 <=sequência2

string1 é lexicograficamente menor ou igual a string2

sequência1 >sequência2

string1 é lexicograficamente maior que string2

sequência1 >=sequência2

string1 é lexicograficamente maior ou igual a string2

inteiro1 -eqinteiro2

integer1 é igual a integer2

inteiro1 -geinteiro2

integer1 é maior ou igual a integer2

inteiro1 -gtinteiro2

integer1 é maior que integer2

inteiro1 -leinteiro2

integer1 é menor ou igual a integer2

inteiro1 -ltinteiro2

integer1 é menor que integer2

inteiro1 -neinteiro2

integer1 não é igual a integer2

prefixinteger1 -pgtprefixinteger2

integer1 é maior que integer2 após remover o prefixo não numérico comum.

prefixinteger1 -pltprefixinteger2

integer1 é menor que integer2 após remover o prefixo não numérico comum.

arquivo1 -ntarquivo2

file1 é mais recente que file2 (tempo de modificação). Opcionalmente, o viés numérico pode ser anexado diretamente, -ntcaso em que é adicionado ao primeiro horário de modificação do arquivo.

arquivo1 -otarquivo2

arquivo1 é mais antigo que arquivo2 (tempo de modificação). Opcionalmente, o viés numérico pode ser anexado diretamente, -otcaso em que é adicionado ao primeiro tempo de modificação do arquivo.

-darquivo

arquivo existe e é um diretório

-earquivo

o arquivo existe

-farquivo

arquivo existe e não é um diretório

-sarquivo

o arquivo existe e tem um tamanho maior que zero

-ncorda

o comprimento da string é diferente de zero

corda

cadeia é equivalente a-n string

-zcorda

o comprimento da corda é zero

(expressão)

expressão é verdadeira

!expressão

expressão é falsa

expressão1 -aexpressão2

Expressão1 e expressão2 são verdadeiras

expressão1 expressão2

Expressão1 e expressão2 são verdadeiras.Esta sintaxe não é compatível com POSIX e não é recomendada.

expressão1 -oexpressão2

A expressão1 ou a expressão2 é verdadeira

`testspeed [OPTIONS] FILE`
Teste a velocidade de leitura do arquivo

--size=n, -s especifica o tamanho de cada leitura

`tetris`
Jogo Tetris. Por favor, faça isso primeiro `terminal_output console`.

`tr [OPTIONS] [SET1] [SET2] [STRING]`
 Substitua o caractere SET1 na string STRING por SET2

​ Se dois parâmetros forem inseridos, a string de entrada deve ser especificada pela opção --set.

--set=VARIÁVEL, -s salva o valor de retorno na variável
--upcase, -U converte para maiúsculas
--downcase, -D converte para minúsculas

`true`
retorna diretamente VERDADEIRO (0)

Usado em instruções if ou while.

`trust [OPTIONS] PUBKEY_FILE`
Adicione PUBKEY à lista de chaves confiáveis

--skip-sig, -s pula a verificação de assinatura do arquivo de chave pública

`type COMMAND`
Verifique se o comando existe e retorne se existir0

`unalias NAME`
Desdefinir alias

`uuid4 VARIABLE`
Gerar string UUID

`vboot harddisk=FILE floppy=FILE cdrom=FILE boot=harddisk/floppy/cdrom`
​ Execute a inicialização do vboot, especifique a imagem do disco rígido/imagem do disquete/imagem do CD e o dispositivo de inicialização padrão.

Você deve primeiro executar vbootinsmod para carregar vbootcore.mod.

O disco rígido precisa conter o arquivo vboot.

O caminho padrão do vboot é /vboot/vboot, modifique a variável vbootloader para especificar o caminho.

`vbootinsmod FILE`
Carregar arquivo vboot core vbootcore.mod

`verify_detached [OPTIONS] FILE SIGNATURE_FILE [PUBKEY_FILE]`
​ Verifique a assinatura destacada.

Os parâmetros são os mesmos que "confiança"

`version`
Exibir informações da versão do GRUB

`videoinfo [WxH[xD]]`
lista modos de exibição disponíveis

`vbeinfo [WxH[xD]]`
O mesmo que 'videoinfo'

`videomode [OPTIONS] VARIABLE`
Obtenha o modo de exibição atual/disponível e salve-o em uma variável

--list, -l lista os modos de exibição disponíveis
--current, -c obtém o modo de exibição atual

`wimboot [OPTIONS] @:NAME:FILE`
Iniciar arquivo WIM

--gui, -g ativa mensagens gráficas de inicialização
--rawbcd, -b desativa a modificação automática do BCD (.exe para .efi)
--rawwim, -w desativa a modificação automática do WIM
--index=n, -i especifica o número do volume WIM para iniciar
--pause, -p pausa antes de iniciar
--inject=WIN32_PATH, -j especifica a pasta de injeção, o padrão é \Windows\Syatem32
--testmode=sim/não modo de teste (testsigning)
--highest=yes/no força a resolução mais alta
--nx=OptIn/OptOut/AlwaysOff/AlwaysOn especifica a política NX
--pae=Padrão/Ativar/Desativar especificar política PAE
--detecthal=sim/não detecta HAL e kernel
--winpe=yes/no inicializa no modo WinPE (/MININT)
--timeout=n define o tempo limite
--novesa=sim/não desabilita as chamadas VESA BIOS
--novga=sim/não desabilita o modo VGA
--loadoptions=XXX especifica os parâmetros de carregamento do kernel do NT
--winload=\WIN32_PATH especifica o caminho winload
--sysroot=\WIN32_PATH especifica o diretório raiz do sistema

`wimtools OPTIONS FILE [WIN32_PATH]`
Ferramenta de análise WIM

--index=n, -i especifica o número do volume WIM
--exist, -e verifica se o arquivo existe
--is64, -a Verifica se o sistema interno do WIM é de 64 bits (x86_64)

`write_bytes ADDR VALUE …`
Escreva uma série de valores de 8 bits para endereçar ADDR

AVISO : Usar este comando pode causar problemas de segurança

