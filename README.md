Em decorrencia das aulas de Adm. de sistemas abertos, foi feito um fork do repostório do Matheus Manuel para que pudessemos entender como funciona o GitHub.

Segue o passo a passo do script que fizemos com o terminal do linux:

  Passo 1: entrar no terminal linux e criar o arquivo com o sudo nano (nome do arquivo).sh
  
  Passo 2: declarar que o arquivo é um script com o #! /bin/bash na primeira linha do arquivo
  
  Passo 3: vamos verificar na maquina com a programação se já temos o apache2 instalado com a condição if, com o [ ! -x /etc/init.d/apache2 ]; (! -x é a negação que indica a não execução do apache2. no caso de não instalado.)
  
  Passo 4: caso o apache não seja encontrado, echo "Apache não encontrado. Iniciando a instalação..." e vamos entrar com os comandos normais de instalação do apache2: sudo apt-get update (atualizar os repositorios) e o sudo apt-get install apache2 -y (comando de instalação do apache2 + a confirmação automatica da instalação
  
  Passo 5: entramos com o else para caso o oposto seja verdade (já tivermos o apache2 instalado na maquina) damos um echo "Apache já instalado" e finalizamos a condicional.
  
  Passo 6: criamos um diretorio para salvar os arquivos que vamos utilizar no nosso 
site quando abrirmos no navegador: sudo mkdir -p /var/www/nome.do.site/public_html   (-p cria uma raiz caso não tenha algum diretorio) 

  Passo 7: entramos com o comando de acesso ao diretorio: cd /var/www/nome.do.site/public_html
  
  Passo 8: entramos no github que queremos usar como base para o nosso site (Obrigado Manuel Matheus), copiamos o link e colamos no comando git clone *link do repositorio*
  
  Passo 9: copiamos tudo do diretorio do Matheus para dentro do public html com o sudo cp -r e renomeamos com o nome da pagina, sendo o nome do arquivo que copiamos (-r copia de forma recursiva)
  
  Passo 10: para não ter redundancia de arquivos, excluimos o arquivo que baixamos com o sudo rm -rf e inserimos o nome do site.
  
  Passo 12: agora vamos configurar os arquivos de configuração do apache. Acessamos o diretorio com cd /etc/apache2/sites-available/ e criamos um arquivo para passar algumas configurações. Podemos copiar do .conf que já tem ou criando um novo arquivo usando o sudo tee (nome do arquivo).conf <<EOF
<VirtualHost *:80>
  
  Passo 13: salvamos o arquivo nano com ctrl + x e entramos com o cd /etc/apache2/sites-available/ e copiamos os dados do .conf que já tem (caso já tenha).
  
  Passo 14: No nosso caso, fizemos do 0, copiamos o seguinte codigo:
sudo tee ifrn.conf<<EOF
<VirtualHost *:80>
    ServerAdmin admin@ifrn
    
    ServerName ifrn
    
    ServerAlias www.ifrn
    
    DocumentRoot /var/www/ifrn/public_html
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    
</Virtualhost>
EOF

*nomes meramente ilustrativos*

  Passo 15: apos isso, habilitamos nosso site com o sdo a2ensite (nome do arquivo).conf e depois podemos inserir as informaçoes para acessar de maneira mais facil o site, pelo nome dele mesmo, usando o sudo echo "127.0.0.1 aluno" e jogamos isso pro arquivo de host usando o sudo tee -a /etc/hosts
  
  Passo 16: e por fim, fazemos o restart do apache2 usando o sudo /etc/init.d/apache2 restart
  
  Passo 17 ("bonus"): verificando com o comando ls -la apos o salvamento do arquivo, vemos que ele não tem permissão de escrita, mas ele tem que ter, então usamos o comando sudo chmod +x (nome do arquivo).sh

  Depois disso tudo, verificamos no terminal linux se de fato vai instalar. 

  ./(nome do arquivo).sh

  Caso haja erros, corrija-os!
  
  
