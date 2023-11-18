# Guia de Instalação: Apache + PHP + MariaDB

Bem-vindo ao repositório dedicado à instalação e configuração do ambiente Apache, PHP e MariaDB no sistema operacional __LINUX__. Este guia abrangente e detalhado foi criado para simplificar o processo de configuração dessas poderosas ferramentas, permitindo que você crie um ambiente de desenvolvimento robusto e eficiente em pouco tempo.

## Objetivo do repositório

O objetivo principal deste repositório é fornecer um conjunto claro de instruções para você instalar e configurar o Apache como servidor web, o PHP como linguagem de script do lado do servidor e o MariaDB como sistema de gerenciamento de banco de dados.

## Sobre o MariaDB

O MariaDB é um sistema de gerenciamento de banco de dados relacional (SGBDR) de código aberto, que se originou como um "fork" do MySQL. Um fork é um ramo independente de desenvolvimento de um software existente, muitas vezes criado quando há divergências ou preocupações em relação à direção futura do projeto original. O MariaDB foi criado pelo criador original do MySQL, Michael "Monty" Widenius, em resposta a preocupações sobre a aquisição do MySQL pela Oracle Corporation em 2009.

No Linux, o MariaDB é frequentemente acessado através do cliente de linha de comando chamado mysql. Isso acontece porque o mysql é um cliente genérico para sistemas de gerenciamento de banco de dados MySQL e MariaDB. Ambos, MySQL e MariaDB, compartilham muita semelhança em termos de protocolo de comunicação e comandos SQL, devido às origens comuns do MariaDB como um fork do MySQL.

A decisão de manter a compatibilidade com o mysql foi tomada para garantir que os usuários pudessem migrar facilmente de um sistema para o outro, sem ter que fazer muitas alterações em seus scripts ou comandos existentes. Dessa forma, os usuários que estão acostumados a trabalhar com o MySQL podem continuar a utilizar o mesmo cliente (mysql) ao migrar para o MariaDB.

É importante notar que, embora o mysql seja frequentemente utilizado para interagir com o MariaDB, existem também clientes específicos do MariaDB, como o mariadb-client, que oferecem funcionalidades adicionais e podem ser mais apropriados em certos contextos. No entanto, devido à compatibilidade, muitas vezes você verá instruções e documentação que referenciam o uso do cliente mysql ao interagir com bancos de dados MariaDB no Linux.

Neste tutorial é utilizado `mysql` como instrução de comando para manipulação dos bancos de dados.

## Como usar este guia

Se você está começando agora, siga as instruções passo a passo para configurar seu ambiente de desenvolvimento local.

Sua contribuição é bem-vinda! Se você encontrar melhorias possíveis, problemas ou tiver sugestões, sinta-se à vontade para abrir uma issue ou enviar um __pull request__. Juntos, podemos tornar este guia uma referência valiosa para a comunidade de desenvolvedores aprendizes.

## Pré-requisitos

Para facilitar a instalação e configuração em servidores remotos, este guia inclui um tópico adicional sobre como realizar todas as etapas utilizando __SSH__. Isso é especialmente útil para ambientes de produção ou servidores de hospedagem em nuvem.

### Conexão SSH

Certifique-se de ter acesso SSH ao servidor onde deseja configurar o ambiente. Use o seguinte comando para se conectar ao seu servidor a partir da sua máquina.

```bash
ssh seu_usuario@seu_servidor
```

Este método via SSH oferece flexibilidade e segurança, permitindo que você gerencie e configure seu ambiente de desenvolvimento ou produção de qualquer lugar do mundo. Isso permite que você execute comandos no servidor remoto como se estivesse na sua máquina.

### Atualização do Linux

O comando abaixo irá atualizar os __índices__ do sistema.

```bash
sudo apt update
```

O comando abaixo irá atualizar os __pacotes__ atualizáveis.

```bash
sudo apt upgrade
```

### Instalação de ferraments essenciais

Vamos instalar um conjunto de utilitários de linha de comando no sistema operacional Linux, usado para diagnosticar e solucionar problemas relacionados à rede. Ele inclui várias ferramentas que permitem visualizar e configurar parâmetros de rede.

```bash
sudo apt install net-tools
```

### Instalando o servidor Apache + PHP

O Apache HTTP Server, comumente conhecido como Apache, é um servidor web de código aberto amplamente utilizado. Ele desempenha um papel fundamental no fornecimento de conteúdo da web na Internet.

```bash
sudo apt-get install apache2 php libapache2-mod-php
```

### Testando a Instalação do Apache

```bash
sudo systemctl status apache2
```
Verifique se __Active__ está como __$\color{lime}{active (running)}$__</span> na cor verde.

### Testando a Instalação do PHP

```bash
php --version
```

O resultado será semelhante ao apresentado a seguir.

```html
PHP 8.1.2-1ubuntu2.14 (cli) (built: Aug 18 2023 11:41:11) (NTS)
Copyright (c) The PHP Group Zend Engine v4.1.2, Copyright (c) Zend Technologies
with Zend OPcache v8.1.2-1ubuntu2.14, Copyright (c), by Zend Technologies
```

### Instalando Módulos Adicionais

A seguir vamos habilitar os módulos opcache (aceleração), gd (imagens), sqlite3 (banco de dados), pgsql (PostgreSQL) e mysql (MySQL).

```bash
sudo apt-get install php-soap php-xml php-curl php-opcache php-gd php-sqlite3 php-mbstring php-pgsql php-mysql
```

### Habilitando Outros Módulos

Habilitando os módulos do Apache, com destaque para o prefork:

```bash
a2dismod mpm_event
a2dismod mpm_worker
a2enmod  mpm_prefork
a2enmod  rewrite
a2enmod  php8.1
```

### Reinicializando o servidor Apache para integrar o PHP

```bash
sudo systemctl restart apache2
```

Verifique se está tudo OK e se não há nenhuma informação sobre erros. Teste no navegador o funcionamento com a url: [http://localhost](http://localhost). Se estiver em um servidor em nuvem ou com abertura para a internet, troque o `localhost` pelo IP da máquina.

Se tudo estiver "OK", será mostrada uma página com as informações da Apache.

### Testando o Funcionamento do Servidor Apache com o PHP

Digite no Terminal do Linux o comando a seguir para criar um arquivo que mostrará as configurações atuais do PHP no navegador.

```bash
echo '<?php phpinfo(); ?>' | sudo tee -a /var/www/html/phpinfo.php > /dev/null
```

Teste no navegador o funcionamento com a url: [http://localhost/phpinfo.php](http://localhost/phpinfo.php)

Se tudo estiver "OK", será mostrada uma página com as informações do PHP.

Exclua o arquivo criado com o seguinte comando:

```bash
sudo rm /var/www/html/phpinfo.php
```

### Instalando o Servidor de Banco de Dados MariaDB (MySQL)

```bash
sudo apt install mariadb-server mariadb-client
```

### Verificando o *status* da instalação do MariaDB

```bash
sudo systemctl status mariadb
```

* Verifique se __Active__ está como __$\color{lime}{active (running)}$__</span> na cor verde.
* Se o comando não finalizar, pressione ```CTRL+C``` para sair.

### Protegendo o MariaDB

```bash
sudo mysql_secure_installation
```

Como não existe uma senha de __root__ definida para o banco de dados, você deve simplesmente pressionar ```Enter``` quando receber a seguinte mensagem: ```Enter current password for root (enter for none):```

Na próxima pergunta, digite __Y__ para definir uma senha de __root__ (*__mantenha-a segura e protegida!__*), digite novamente __Y__ e siga as orientações, informando a senha.

Para as próximas perguntas, você pode pressionar ```Enter``` para cada um dos itens.

### Acessando o MariaDB via CLI (*Command Line*)

Digite o seguinte comando:

```bash
sudo mysql
```

Você terá na tela algo semelhante a:

```bash
MariaDB [(none)]>
```

### Criação de usuário no MariaDB

Criando um usuário __admin__ padrão no banco de dados diferente de __root__.

Para isso, digite as linhas abaixo (__uma linha por vez__) e pressione ```ENTER``` para executá-la. __Não esqueça__ de colocar o ponto-e-vírgula "__```;```__" no final de cada linha.

```sql
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';
FLUSH PRIVILEGES;
quit;
```

### Acessando o MariaDB

Para acessar o MariaDB com o novo usuário criado, digite o comando a seguir e informe a senha definida anteriormente (__admin__) quando solicitado:

```bash
sudo mysql -u admin -p
```

### Criando um banco de dados no MariaDB

```sql
CREATE DATABASE bd_teste;
```

### Selecionando o banco ```bd_teste```

```sql
USE bd_teste;
```

### Criando uma tabela de dados

```sql
CREATE TABLE tb_teste (
    id int primary key not null auto_increment, 
    nome varchar(50)
);
```

### Inserindo registros na tabela (tb_teste)

```sql
INSERT INTO tb_teste (nome) VALUES ("Primeiro Nome");
INSERT INTO tb_teste (nome) VALUES ("Segundo Nome");
```

### Verificando as inclusões realizadas

```sql
SELECT * FROM tb_teste;
```

O resultado deverá ser igual ao mostrado abaixo.

```sql
+----+---------------+
| id | nome          |
+----+---------------+
|  1 | Primeiro Nome |
|  2 | Segundo Nome  |
+----+---------------+
2 rows in set (0.000 sec)
```

### Sair do MariaDB

```sql
quit;
```

### Testando a conexão do PHP com o banco de dados MariaDB

Criando um diretório para colocar um arquivo de teste de conexão do PHP com o banco de dados criado anteriormente __bd_teste__.

```bash
sudo mkdir /var/www/html/teste
```

### Acessando o diretório criado

```bash
cd /var/www/html/teste
```

Execute o comando ```ls -la``` para realizar a listagem do diretório e verificar se ele está vazio. O resultado deste comando é similar ao mostrado abaixo.

```bash
drwxr-xr-x 2 root root 4096 ago  8 21:22 .
drwxr-xr-x 3 root root 4096 ago  8 21:22 ..
```

### Criando um arquivo PHP+MariaDB

Para criar o ```script PHP``` (programa) e fazer a conexão com o banco de dados __bd_teste__, vamos utilizar a biblioteca PDO de acesso a dados. Para isso, digite o seguinte comando para abrir o editor de textos (```Nano```):

```bash
sudo nano index.php
```

Digite as instruções a seguir no arquivo aberto:

```php
<?php
try {
    $conn = new PDO('mysql:host=localhost;dbname=bd_teste', 'admin', 'admin');
    
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    $data = $conn->query('SELECT * FROM tb_teste');

    foreach($data as $key => $value) {
        print("Id: " . $value[0] . "</br>");
        print("Nome: " . $value[1] . "</br>");
        print("</br></br>");
    }
} catch(PDOException $e) {
    echo 'ERROR: ' . $e->getMessage();
}
```

Para salvar o arquivo, pressione as teclas ```CTRL+X``` simultaneamente, depois digite ```Y``` e, por fim, pressione ```ENTER``` para fechar o editor de textos.

Execute novamente o comando ```ls -la``` para realizar a listagem do diretório e verificar se o arquivo foi criado corretamente. O resultado é parecido com o que pode ser visualizado abaixo, mostrando o arquivo ```index.php```.

```bash
drwxr-xr-x 2 root root 4096 ago  8 21:27 .
drwxr-xr-x 3 root root 4096 ago  8 21:22 ..
-rw-r--r-- 1 root root  469 ago  8 21:27 index.php
```

### Testando o funcionamento do programa

Acesse novamente o navegador e digite: [http://localhost/teste](http://localhost/teste), ou o IP da máquina remota. Se tudo ocorreu como o esperado, deverá ser mostrado no navegador os dados cadastrados anteriormente no banco de dados.

Agora é só estudar e desenvolver suas aplicações!

## Como citar este conteúdo

```latex
Souza, Edson Melo de. (2023, November 18). Guia de Instalação: Apache + PHP + MariaDB.
Available in: https://github.com/EdsonMSouza/Apache-PHP-MariaDB
```

Ou BibTeX para LaTeX:

```latex
@misc{Souzaem2023LAMP,
  author = {Souza, Edson Melo de},
  title = {Guia de Instalação: Apache + PHP + MariaDB},
  url = {https://github.com/EdsonMSouza/Apache-PHP-MariaDB},
  year = {2023},
  month = {November}
}
```

### License

[![CC BY-SA 4.0][cc-by-sa-shield]][cc-by-sa]

This work is licensed under a
[Creative Commons Attribution-ShareAlike 4.0 International License][cc-by-sa].

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

[cc-by-sa]: http://creativecommons.org/licenses/by-sa/4.0/
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
[cc-by-sa-shield]: https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg
