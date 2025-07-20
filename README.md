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
Exercício 02: Sim, de novo...
Crie todos estes ficheiros e pastas. Faça o que for necessário para que a visualização
de um ls-l na sua pasta fique da seguinte forma:
  %> ls -l
  total XX
  drwx--xr-x 2 XX XX XX Jun 1 20:47 test0
  -rwx--xr-- 1 XX XX 4 Jun 1 21:46 test1
  dr-x---r-- 2 XX XX XX Jun 1 22:45 test2
  -r-----r-- 2 XX XX 1 Jun 1 23:44 test3
  -rw-r----x 1 XX XX 2 Jun 1 23:43 test4
  -r-----r-- 2 XX XX 1 Jun 1 23:44 test5
  lrwxrwxrwx 1 XX XX 5 Jun 1 22:20 test6 -> test0
  %>
Após resolver o exercício, execute o comando tar -cf exo2.tar * para criar o
ficheiro que será entregue.


#Solucao
1. Criar directorios/(pastas):
  
        mkdir test0
        mkdir test2

2. Criar ficheiros:
  
        touch test1
        touch test3
        touch test4

3. Criar link de test6 para a directorio/(pasta) test0:

        ln -s test0 test6

4. Criar link simbólico de test3 para test5:

        ln test3 test5

5. Usar truncate para reduzir o tamanho dos ficheiros:
  
        truncate -s 4 test1
        truncate -s 1 test3
        truncate -s 2 test4
        truncate -s 1 test5


6. Alterar Permissoes:
  
        chmod 715 test0
        chmod 714 test1
        chmod 504 test2
        chmod 404 test3
        chmod 641 test4
        chmod 404 test5
        chmod 777 test6

  drwx--xr-x (715)
  -rwx--xr-- (714)
  dr-x---r-- (504)
  -r-----r-- (404)
  -rw-r----x (641)
  -r-----r-- (404)
  lrwxrwxrwx (777)

6. Alterar a data de modificação para algo específico:
  Para isso, podes usar o comando touch com a opção -t para definir uma data e hora específica:
  
        touch -t 202506012047 test0
        touch -t 202506012146 test1
        touch -t 202506012245 test2
        touch -t 202506012344 test3
        touch -t 202506012343 test4
        touch -t 202506012344 test5
        touch -h -t 202506012220 test6

7. Criar o ficheiro .tar para entrega:

          tar -cf exo2.tar test0 test1 test2 test3 test4 test5 test6
   
==========================================
Exercício 03: SSH me!
Cria a tua própria chave SSH. Uma vez criada:
◦ Acrescente ao repositório a sua chave pública num ficheiro chamado id_rsa_pub
◦ Atualize a sua chave SSH na intra. Isto vai permitir enviar o seu repositório
para o nosso servidor git.

INCOMPLETE


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



