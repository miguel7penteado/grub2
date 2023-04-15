# Equipamentos e documentos

# DEVICE ( ou equipamento)

A sintaxe para um dispositivo está na forma

```grub
(device[,partmap-name1part-num1[,partmap-name2part-num2[,...]]])
```

No BIOS e UEFI, os nomes dos dispositivos de disco rígido, disquete e disco óptico são "hd", "fd", "cd" mais números (começando em 0), como "hd0", "fd1", "cd0" . Se inicializar a partir de um CD no BIOS, o nome do dispositivo pode ser "cd".

partmap-namepart-nume representam o nome da tabela de partições e o número da partição (começando em 1) respectivamente. Por exemplo (hd0,msdos1), representa a primeira partição da tabela de partições do disco rígido 0 MBR (msdos) e (hd1,gpt3)representa a terceira partição da tabela de partições do disco rígido 1 GPT.

# DOCUMENTOS

O GRUB oferece suporte a representações de arquivo, como caminhos absolutos e listas de bloqueio.

`caminho absoluto`
Semelhante aos sistemas Unix, o GRUB usa uma barra "/" como separador de pastas.

EXEMPLO:
```grub
(hd1,msdos2)/boot/grub/grub.cfg
```

`caminho relativo`
Se o caminho do arquivo omitir o nome do dispositivo, o padrão será o arquivo no dispositivo raiz (raiz).

EXEMPLO:
```grub
set root=hd0,1
```
então /efi/boot/bootx64.efié equivalente a (hd0,1)/efi/boot/bootx64.efi.

`lista de bloqueio`
Por exemplo [offset]+length[,[offset]+length], pode ser usado para se referir a arquivos que não existem no sistema de arquivos, como o registro mestre de inicialização de um disco.

EXEMPLO
```grub
(hd0)0+100,200+1,300+300
```
Isso significa que o GRUB lê os blocos 0 a 99, o bloco 200 e os blocos 300 a 599. Se o deslocamento for omitido, será assumido o deslocamento 0. A lista de bloqueio de um arquivo pode ser visualizada com blocklisto comando .

`arquivo de memória`
Por exemplo mem:addr:size:num, uma determinada seção da memória pode ser lida como um arquivo.

EXEMPLO
```grub
mem:0x1234:size:567
```

`tratar o dispositivo como arquivo`
GRUB suporta a leitura de um disco ou partição diretamente como um arquivo

EXEMPLO
```grub
(hd1) (hd0,msdos1) (memdisk) (http)
```
