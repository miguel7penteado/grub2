# Linguagem LUA para Grub


## Carregar módulo LUA

```grub
​insmod lua
```

## Entre no modo de programação interativa Lua

Pra entrar no console da linguagem lua, digite:

```grub
lua
```

## Executar scripts Lua

Para execexecutar scripts lua, digite "lua" e passe o caminho do script:
​
```grub
lua /path/to/script.lua
```

## Biblioteca do GRUB

| Funções, parâmetros e retorno                                                                    | Descrição:                                                                                                                                                                                                            |
|--------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| grub.run (string command)                                                                        | Execute o comando GRUB, se a execução for bem-sucedida, retorna zero, caso contrário, retorna um valor diferente de zero.                                                                                             |
| grub.script (string script)                                                                      | Executa um script GRUB de uma linha, retornando zero se o script for executado com sucesso.                                                                                                                           |
| grub.getenv (string variable)                                                                    | Obtenha o valor da variável de ambiente GRUB, se a variável de ambiente existir, retorne o valor da variável, caso contrário, retorne nil.                                                                            |
| grub.setenv (string variable, string value)                                                      | Defina o valor da variável de ambiente GRUB. O primeiro parâmetro é o nome da variável e o segundo parâmetro é o conteúdo da variável.                                                                                |
| grub.exportenv (string variable[, string value])                                                 | Defina o valor da variável de ambiente global GRUB. O primeiro parâmetro é o nome da variável e o segundo parâmetro é opcional, que é o conteúdo da variável.                                                         |
| grub.enum_device (function (string device[, string fs, string uuid, string label, string size])) | Enumera os dispositivos de disco do GRUB. O parâmetro é a função para enumerar e executar, que pode obter o **nome do dispositivo**, **sistema de arquivos**, **UUID** e **rótulo de volume**.                        |
| grub.enum_file (function (string filename[, int isdir]))                                         | Enumerar arquivos e pastas em um diretório (incluindo .e ..)                                                                                                                                                          |
| userdata file = grub.file_open (string filename[, string flag])                                  | Abra o arquivo, o valor de retorno é um identificador de arquivo do tipo `userdata` . O primeiro parâmetro é o nome do arquivo. O segundo parâmetro é o método de abertura, se for "w", será aberto em modo gravável. |
| grub.file_close (userdata file)                                                                  | Feche o arquivo.                                                                                                                                                                                                      |
| grub.file_seek (userdata file, integer offset)                                                   | Defina o deslocamento de posição para leitura e gravação do identificador de arquivo e o valor de retorno é o deslocamento.                                                                                           |
| grub.file_read (userdata file, integer length)                                                   | Leia o arquivo, o comprimento é "comprimento" e retorne o conteúdo do arquivo.                                                                                                                                        |
| grub.file_write (userdata file, string data)                                                     | Escreva a string "dados" no arquivo.                                                                                                                                                                                  |
| grub.file_getline (userdata file)                                                                | Leia uma linha de texto do arquivo e retorne esse texto.                                                                                                                                                              |
| grub.file_getsize (userdata file)                                                                | Retorna o tamanho do arquivo.                                                                                                                                                                                         |
| grub.file_getpos (userdata file)                                                                 | Retorna o deslocamento atual do arquivo.                                                                                                                                                                              |
| grub.file_eof (userdata file)                                                                    | Determine se o arquivo foi lido até o fim.                                                                                                                                                                            |
| grub.file_exist (string filename)                                                                | Determine se o arquivo existe.                                                                                                                                                                                        |
| string buf, string hex = grub.hexdump (userdata file, integer skip, integer length)              | Obtenha os dados hexadecimais na posição especificada no arquivo.                                                                                                                                                     |
| grub.add_menu (string source, string title[, …])                                                 | Adicione um item de menu, o conteúdo do menu é "fonte" e o título é "título".                                                                                                                                         |
| grub.add_icon_menu (string icon, string source, string title[, …])                               | Adicione um item de menu com um ícone (–class).                                                                                                                                                                       |
| grub.add_hidden_menu (string hotkey, string source, string title[, …])                           | Adicione um item de menu oculto com tecla de atalho como "tecla de atalho".                                                                                                                                           |
| grub.clear_menu (nil)                                                                            | Limpe o menu.                                                                                                                                                                                                         |
| grub.cls (nil)                                                                                   | Limpar tela.                                                                                                                                                                                                          |
| grub.setcolorstate (integer state)                                                               |                                                                                                                                                                                                                       |
| grub.refresh (nil)                                                                               | executar a função `grub_refresh`                                                                                                                                                                                      |
| string text = grub.gettext (string src)                                                          | Traduza a string.                                                                                                                                                                                                     |
| integer rand = grub.random (integer m)                                                           | Retorna um número aleatório menor que "m".                                                                                                                                                                            |
| grub.enum_block (function (string block)[, int part_start])                                      | Enumera a lista de bloqueio do arquivo, na forma de setor+tamanho. Se houver part_startum parâmetro , o número do setor é calculado com base no setor inicial da partição.                                            |

## Biblioteca do INI


| Funções, parâmetros e retorno                                    | Descrição:                              |
|------------------------------------------------------------------|-----------------------------------------|
| userdata inifile = ini.load (string filename)                    | Carregue o arquivo de configuração ini. |
| ini.free (userdata inifile)                                      | Libere o arquivo de configuração ini.   |
| string ini.get (userdata inifile, [string section, ] string key) | Leia os itens de configuração do ini.   |

## Biblioteca INPUT

| Funções, parâmetros e retorno                                       | Descrição:                                                                                      |
|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| integer ascii_code, integer scan_code = input.getkey ( nil)         | Aguarde até que o usuário pressione uma tecla e retorne o código ASCII e o código de varredura. |
| integer ascii_code, integer scan_code = input.getkey_noblock( nil)  | Retorna o código ASCII e o scancode (usado no loop).                                            |
| string line = input.read (nil)                                      | Aguarde até que o usuário digite uma linha de string.                                           |

## Biblioteca VIDEO

| Funções, parâmetros e retorno                                                                                              | Descrição:                                                      |
|----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| video.swap_buffers(nil)                                                                                                    |                                                                 |
| video.fill_rect(table color{integer r, integer g, integer b, integer a}, integer x, integer y, integer w, integer h)       | Desenha um retângulo no local especificado.                     |
| video.draw_string(string text, string font, table color{integer r, integer g, integer b, integer a}, integer x, integer y) | Exibe uma string na posição especificada.                       |
| string video_mode = video.info(nil)                                                                                        | Obtenha uma lista de modos de imagem.                           |
| video.draw_pixel(table color{integer r, integer g, integer b, integer a}, integer x, integer y)                            | Desenhe um pixel na posição especificada.                       |
| integer x, integer y = video.get_info(nil)                                                                                 | Obtenha a largura e a altura do modo de exibição atual.         |
| userdata bitmap = video.bitmap_load(string filename)                                                                       | Carregue arquivos de imagem (suporte bmp, jpg, jpeg, png, tga). |
| video.bitmap_close(userdata bitmap)                                                                                        | Feche o arquivo de imagem.                                      |
| integer x, integer y = video.bitmap_info(userdata bitmap)                                                                  | Obtenha a largura e a altura da imagem.                         |
| video.bitmap_blit(userdata bitmap, integer x, integer y, integer offset_x, integer offset_y, integer w, integer h)         | Exibe a imagem na posição especificada.                         |
| userdata scaled_bitmap = video.bitmap_rescale(userdata bitmap, integer w, integer h)                                       | Dimensiona a imagem especificada.                               |



## Biblioteca GBK

| Funções, parâmetros e retorno                   | Descrição:                                                                           |
|-------------------------------------------------|--------------------------------------------------------------------------------------|
| string gbk_str = gbk.fromutf8(string utf8_str)  | Converter string UTF-8 em string codificada em GBK.                                  |
| string utf8_str = gbk.toutf8(string gbk_str)    | Converta uma string codificada em GBK em uma string UTF-8.                           |
| string utf8_simp = gbk.tosimp(string utf8_trad) | Converter string UTF-8 em chinês tradicional em string UTF-8 em chinês simplificado. |


## Biblioteca DISK

| Funções, parâmetros e retorno                                                         | Descrição:                                                                      |
|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| userdata dev = disk.open (string diskname)                                            | Abra o disco, o valor de retorno é um identificador de disco do userdatatipo .  |
| disk.close (userdata dev)                                                             | Feche o disco.                                                                  |
| string buf = disk.read (userdata dev, integer sector, integer offset, integer length) | Leia os dados do setor/deslocamento especificado do disco e retorne uma string. |
| disk.write (userdata dev, integer sector, integer offset, integer length, string buf) | gravar no disco.                                                                |
| string partmap = disk.partmap (userdata dev)                                          | Obtenha o nome da tabela de partições.                                          |
| string driver = disk.driver (userdata dev)                                            | Obtenha o nome da unidade de disco.                                             |
| string fs = disk.fs (userdata dev)                                                    | Obtenha o nome do sistema de arquivos.                                          |
| string uuid = disk.fsuuid (userdata dev)                                              | Obtenha o UUID do sistema de arquivos.                                          |
| string label = disk.label (userdata dev)                                              | Obtenha o rótulo do disco.                                                      |
| string size = disk.size (userdata dev[, flag])                                        | Obtenha o tamanho do disco.                                                     |
| boolean boot = disk.bootable (userdata dev)                                           | Determine se a partição possui um sinalizador inicializável.                    |


## Biblioteca FAT

| Funções, parâmetros e retorno | Descrição: |
|-------------------------------|------------|
| fat.mount                     |            |
| fat.umount                    |            |
| fat.disk_status               |            |
| fat.get_label                 |            |
| fat.set_label                 |            |
| fat.mkdir                     |            |
| fat.rename                    |            |
| fat.unlink                    |            |
| fat.open                      |            |
| fat.close                     |            |
| fat.read                      |            |
| fat.write                     |            |
| fat.lseek                     |            |
| fat.tell                      |            |
| fat.eof                       |            |
| fat.size                      |            |
| fat.truncate                  |            |


## Biblioteca MEMRW

| Funções, parâmetros e retorno                  | Descrição:                                           |
|------------------------------------------------|------------------------------------------------------|
| integer value = memrw.read_byte(integer addr)  | Lê um byte de dados de um endereço de memória.       |
| integer value = memrw.read_word(integer addr)  | Ler dados de byte duplo de um endereço de memória.   |
| integer value = memrw.read_dword(integer addr) | Lê dados de palavra dupla do endereço de memória.    |
| memrw.write_byte(integer addr, integer value)  | Escreva um byte de dados no endereço de memória.     |
| memrw.write_word(integer addr, integer value)  | Grava dados de byte duplo no endereço de memória.    |
| memrw.write_dword(integer addr, integer value) | Grava dados de palavra dupla no endereço de memória. |

