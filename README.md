# CPiscineShell00

File Management -> cp, mv, rm, mkdir
Navigation -> cd, pwd, ls
Text Processing -> cat
Permissions and Ownership -> chmod
Networking - > wget
Compression and Archiving - > tar

[Basic Shell Commands for File and Directory Management]

Command	| Description	                                          | Example
ls	    | Lists files and directories	                          | ls
cd	    | Changes the current directory	                        | cd /home/user/Documents
pwd	    | Displays the current directory path                   | pwd
mkdir	  | Creates a new directory	                              | mkdir new_directory
rm	    | Removes files or directories	                        | rm file.txt
cp	    | Copies files or directories	                          | cp file1.txt file2.txt
mv	    | Moves or renames files and directories                | mv old_name new_name
touch   | Creates an empty file or updates file timestamps      | touch newfile.txt
__________________________________________________________________________________________________________

Command	| Description	                                          | Example
cat	    | Displays the contents of a file	                      | cat file.txt
__________________________________________________________________________________________________________

Command	| Description	                                          | Example
chmod	  | Changes file permissions	                            | chmod 755 file.txt
__________________________________________________________________________________________________________

Command	| Description	                                          | Example
wget    |	Retrieves files from the web	                        | wget http://example.com///file.zip
__________________________________________________________________________________________________________

Command	| Description	                                          | Example
tar	    | Archives files into a tarball (.tar) or extracts them	| tar -cvf archive.tar file1.txt file2.txt
__________________________________________________________________________________________________________

==========================================
==========================================
==========================================
==========================================
Exercício 03: SSH me!
Cria a tua própria chave SSH. Uma vez criada:
◦ Acrescente ao repositório a sua chave pública num ficheiro chamado id_rsa_pub
◦ Atualize a sua chave SSH na intra. Isto vai permitir enviar o seu repositório
para o nosso servidor git.

#Solucao

Aceder:

    cd ~/.ssh

    cat id_rsa.pub

  Copy the key:
  ssh-rsa (...) 42porto.com


==========================================

Exercício 06: gitignore

    nano git_ignore.sh

#!/bin/sh
git ls-files --other --ignored --exclude-standard

git ls-files = Comando base que mostra arquivos que o Git conhece — normalmente os que estão no índice (staging area).
--other = Mostra os arquivos não rastreados (também chamados de untracked). Ou seja, arquivos que estão no diretório, mas que o Git nunca viu.
--ignored = Mostra os arquivos que estão sendo ignorados pelo Git, com base nas regras de .gitignore, etc.
--exclude-standard = Diz ao Git para usar as regras de ignore "padrão", que incluem: #O arquivo .gitignore do repositório, #O arquivo .git/info/exclude (específico do repositório), #O arquivo global de ignore (~/.gitignore_global, se configurado)

Resumo do que o comando retorna:
  Esse comando lista todos os arquivos que o Git não está rastreando, sejam eles:
  
  Arquivos novos, que você criou e ainda não deu git add
  
  Arquivos que o Git está ignorando por estarem em .gitignore

==========================================

Exercício 07: dif

wget <url>


patch [options] [originalfile [patchfile]]

Criar ficheiro b com a diferenca:

    patch a -o b sw.diff

-o outfile  or  --output=outfile
          Send output to outfile instead of patching files in place.  Do not use this option if outfile is one of the files to be patched.  When outfile is -, send output to standard output, and  send  any
          messages that would usually go to standard output to standard error.

==========================================

+++++++++++++++++++++++++++++++++++++++++++
# CPiscineShell01
Exercício 01: print_groups

Escreva uma linha de comando que determine e mostre a lista de grupos dos quais
o login especificado na environment variable FT_USER é membro, separando-os
por vírgulas sem espaços.


groups, é um comando no Linux que, quando executado, mostra os grupos dos quais o usuário atual pertence.

Se você passar um nome de usuário como argumento (groups username), ele mostra os grupos desse usuário específico.

groups nours


#Solucao
man id

aceder aos grupos
cut -d: -f1 /etc/passwd


Resolucao:
1. Create file with nano command:
  #!/bin/sh
  id -G -n "$FT_USER" | tr ' ' ','

[How to:]
id - print real and effective user and group IDs
         -G, --groups
                print all group IDs
         -n, --name
                print a name instead of a number
|, the value you receive is sent to the next command (tr):
  tr, is a Unix/Linux command that stands for translate.
    It is used to replace or remove individual characters.

==========================================
Exercício 02: find_sh
Escreva uma linha de comando que procure, na pasta atual e em todas as suas
subpastas, todos os ficheiros cujos nomes terminam com .sh e que só exiba os seus
nomes, sem o .sh

[Exemplo:]

      $>./find_sh.sh | cat -e
      find_sh$
      file1$
      file2$
      file3$
      $>

#Solucao
1. Criar ficheiro sh:
  nano find_sh.sh
2. Adicionar comando: (Os exercícios de shell devem ser executados com /bin/sh)
  #!/bin/sh
  find . -name "*.sh" | sed 's/\.[^.]*$//'
3. Atribuir permissões:
  chmod +x find_sh.sh

[How to:]
(find) para procurar ficheiros e diretórios.
(find .) procura na pasta atual e em todas as subpastas
(-name "*.sh") procura ficheiros cujo nome termina com .sh
(sed) para substituições de texto (alternativa ao basename)
(s) s/regexp/replacement/ comando de substituição do sed (substitui o padrão encontrado por outro texto).
  (/) delimitador do comando s (separador entre padrão e substituição)
  
  [Regex:] \.[^.]*$
  (\.) casa com o ponto antes do sh. corresponde a um ponto literal (.) é preciso escapar com a barra invertida (\.) para indicar que é um ponto real.
  ([ ^ . ]*) casa com sh (letras que não são ponto).
  ($) indica que é o final da linha/string.

  (//) substitui o padrão encontrado por nada (remove).


==========================================
Exercício 03: count_files
Escreva uma linha de comando que conta o número de ficheiros e de pastas dentro
da pasta atual e todas as suas subpastas, incluindo o . da pasta inicial.

[Exemplo:]

    $>./count_files.sh | cat -e
    42$
    $>

#Solucao
1. Criar ficheiro sh:
  nano count_files.sh
2. Adicionar comando: (Os exercícios de shell devem ser executados com /bin/sh)
  #!/bin/sh
  find . | wc -l
3. Atribuir permissões:
  chmod +x count_files.sh

==========================================
Exercício 04: MAC
Escreva uma linha de comando que mostre os endereços MAC da sua máquina.
Cada endereço deve ser seguido de uma quebra de linha.


#Solucao
1. Criar ficheiro sh:
  nano MAC.sh
2. Adicionar comando: (Os exercícios de shell devem ser executados com /bin/sh)
  #!/bin/sh
  ifconfig | grep ether | awk '{print $2}'
3. Atribuir permissões:
  chmod +x MAC.sh

==========================================
Exercício 05: Consegue criar?
Crie um arquivo contendo apenas 42 e nada mais.


#Solucao
1. Criar ficheiro com conteudo 42 com nome específico:
  printf "42" > "\"\\?\$*'MaRViN'*\$?\\\""
2. Testar outcome:
  ls -lRa *MaRV* | cat -e

Resultado do outcome: 
-rw-r--r-- 1 pmiguel2 2025_porto 2 Jul 16 14:22 "\?$*'MaRViN'*$?\"$


Resultado correto esperado:
"\?$*'MaRViN'*$?\"$

==========================================



