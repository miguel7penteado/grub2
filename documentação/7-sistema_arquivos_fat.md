# Sistema de arquivos FAT no GRUB


Função de leitura e gravação de arquivos `FAT/exFAT`.

## Carregar módulo FatFs

```grub
insmod fatfs
```

## Formato do caminho:

FatFs suporta a montagem de até 10 partições ao mesmo tempo.

Os usuários podem montar até 9 partições, as letras da unidade são 1:, 2:, 3:, ..., 9:. Letra da unidade 0: Reservado para o sistema.

​O caminho é expresso como X:/caminho/para/arquivo, como 2:/EFI/BOOT/bootx64.efi, e não diferencia maiúsculas de minúsculas.

## Montagem de Partição:

```grub
mount PARTITION NUM[1-9]
```

## Montagem de Partição:

Exemplo: ​Monte a partição (hd0,1) para 2

```grub
mount (hd0,1) 2
```


## Desmontagem de Partição:

umount NUM[1-9]

Exemplo: ​desmonte a partição 2

```grub
umount 2
```


## Exibir o status de montagem da partição:

```grub
mount status
```

## Criar pasta

mkdir PATH

exemplo:

```grub
mkdir 1:/caminho/para/arquivo
```

## Copiar arquivos

cp SRC_FILE DST_FILE

O arquivo de origem pode ser um caminho de arquivo GRUB ou um caminho de arquivo FatFs
Exemplo:
```grub
cp 1:/foo/bar/sys.vhd 2:/boot.vhd

​cp (hd0,2)/foo/bar/sys.vhd 2:/boot.vhd
```


## Renomear arquivo/pasta

​rename SRC_FILE DST_FILE

O arquivo de destino deve estar no mesmo disco que o arquivo de origem, o que equivale a mover arquivos para o mesmo disco.
Exemplo:
```grub
rename 1:/foo/bar.tar.gz 1:/abc.gz
```

## Excluir arquivo/pasta

​rm FILE

Não é possível excluir pastas não vazias.
Exemplo:
```grub
rm 1:/caminho/arquivo.txt
```


## Mover arquivos
​mv SRC_FILE DST_FILE

Se o arquivo de destino estiver no mesmo disco que o arquivo de origem, é equivalente a renamer o arquivo.
Exemplo:
```grub
mv 1:/foo/bar.tar.gz 2:/abc.gz
```

## Criar arquivo/modificar tempo de acesso ao arquivo
​touch FILE [YEAR MONTH DAY HOUR MINUTE SECOND]

Se nenhuma hora for especificada, o carimbo de data/hora do arquivo é modificado para a hora atual. Se o arquivo não existir, um arquivo vazio será criado.
Exemplo:
```grub
​touch 1:/foo/bar.txt
​touch 1:/foo/bar.txt 2000 1 1
```

## Modificar arquivo
​write_file FILE STRING [OFFSET]

Escreva uma string para o arquivo em bytes de deslocamento de arquivo OFFSET. Se o tamanho do arquivo for insuficiente, o tamanho do arquivo será expandido automaticamente.
Exemplo:
```grub
​write_file 1:/diretorio/arquivo.txt "Escrevendo uma frase."

​write_file 1:/diretorio/arquivo.txt "Modificando a frase." 0x786
```

