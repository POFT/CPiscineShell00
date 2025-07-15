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
Exercício 00: Z
Crie um ficheiro chamado z que retorna "Z", seguido por uma quebra de linha quando o comando cat é usado no ficheiro.


#Solucao_A
Para criar um ficheiro chamado z que retorna a letra "Z" seguida de uma quebra de linha quando o comando cat for usado, basta seguir estas etapas no terminal:
  1.Crie o ficheiro z:
  echo "Z" > z
  2. Agora, inserir o comando cat no ficheiro, ele irá exibir "Z" seguido por uma quebra de linha:
  cat z

Isso é simples e direto. 
A função do comando echo é escrever "Z" no ficheiro z, e a quebra de linha é automaticamente incluída após a string, já que o comando echo adiciona uma nova linha ao final por padrão.

#Solucao_B
Outra alternativa é usar o comando printf para escrever diretamente no ficheiro, garantindo que a quebra de linha seja inclusa. A diferença do echo é que o printf oferece mais controle sobre o formato da saída.
  1. inserir o comando:
  printf "Z\n" > z
  2. Agora, inserir o comando cat no ficheiro, ele irá exibir "Z" seguido por uma quebra de linha:
  cat z

Esse método é útil especialmente quando você precisa de um controle mais preciso sobre o formato da string.

==========================================
Exercício 01: testShell00
Crie o ficheiro testShell00 dentro da pasta de entrega ex01/.
Deve garantir que a informação output corresponde ao exemplo seguinte (excepto
a linha "total 1"):
  %> ls -l
  total XX
  -r--r-xr-x 1 XX XX 40 Jun 1 23:42 testShell00
  %>
Após resolver o exercício, execute o comando tar -cf testShell00.tar testShell00
para criar o ficheiro que será entregue.


#Solucao
1. Criar a pasta ex01: 
  mkdir -p ex01
2. Criar o ficheiro testShell00 dentro da pasta ex01:
  touch testShell00
3. Altere as permissões do ficheiro para garantir que o ls -l mostre algo similar:
  chmod 455 testShell00
                  [Análise das permissões:]
                  Primeira parte (r--): Permissões para o proprietário (usuário):
                  r (leitura) = 4
                  - (sem permissão de escrita) = 0
                  - (sem permissão de execução) = 0
                  Total para o proprietário: 4
                  Segunda parte (r-x): Permissões para o grupo:
                  r (leitura) = 4
                  - (sem permissão de escrita) = 0
                  x (execução) = 1
                  Total para o grupo: 5
                  Terceira parte (r-x): Permissões para outros (público):
                  r (leitura) = 4
                  - (sem permissão de escrita) = 0
                  x (execução) = 1
                  Total para outros: 5
                  Código numérico final:
                  Proprietário: 4
                  Grupo: 5
                  Outros: 5
                  Então, o código numérico correspondente a -r--r-xr-x é 455.
4. Alterar tamanho do ficheiro para "40", abra o ficheiro com o nano:
  nano testShell00
    Escreve o texto com 40 caracteres (Lorem ipsum dolor sit amet, consectetur)
      Pressione CTRL + X para sair.
      Depois, pressione Y para confirmar as alterações.
      Pressione Enter para salvar o ficheiro com as mudanças.
6. Alterar a data de modificação para algo específico (se você deseja uma data exata, como "Jun 1 23:42")
Para isso, você pode usar o comando touch com a opção -t para definir uma data e hora específica:
  touch -t 202506012342 testShell00
7. Para criar o arquivo .tar contendo o ficheiro testShell00, você pode usar o comando tar com a opção -cf, que significa:
-c: Criar um novo arquivo tar.
-f: Especificar o nome do arquivo tar a ser criado.
  tar -cf testShell00.tar testShell00
(Este comando criará um arquivo chamado testShell00.tar no diretório atual, contendo o ficheiro testShell00 localizado dentro da pasta ex01.)

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
1. Criar directory:
  mkdir test0
  ...
2. Criar Ficheiro:
  touch test1
  ...
3. Criar link test6 para test0
  ln -s test0 test6
4. Alterar Permissoes:
  chmod () test...
  drwx--xr-x (504)
  -rwx--xr-- (714)
  dr-x---r-- (504)
  -r-----r-- (404)
  -rw-r----x (641)
  -r-----r-- (404)
  lrwxrwxrwx (777)
5. Usar truncate para reduzir o tamanho do ficheiro:
  truncate -s 1 test3
  ...
6. Alterar a data de modificação para algo específico.
Para isso, você pode usar o comando touch com a opção -t para definir uma data e hora específica:
  touch -t 202506012047 test0
  ...
   
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

Environment variables are defined using the syntax VARIABLE_NAME="value". For instance, EDITOR="vim" sets the EDITOR variable to "vim". 



