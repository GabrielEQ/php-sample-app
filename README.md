# Sistemas para Internet - SecDevOps

***nac:*** Criação de uma aplicação no formato "CRUD" executada em containers com base na linguagem "PHP" e no banco de dados "MySQL";

---

***Importante:***

Instruções sobre modelo de execução e entregáveis podem ser obtidas no [diretório de documentação](https://github.com/fiapsecdevops/php-sample-app/tree/master/docs) ou no portal do aluno;

Duvidas podem ser enviadas para <profhelder.pereira@fiap.com.br>

Esta app foi adaptada do exemplo contido [neste artigo](https://www.tutorialrepublic.com/php-tutorial/php-mysql-crud-application.php)

A estrutura foi criada com base nas seguintes tags:

- frontend-0.1: Versão de testes SEM conexão com o banco para a primeira parte da NAC;
- stable:  Versão COM as linhas de conexão com o banco configuradas, será necessário que o MySQL esteja operante para testes faltando apenas a criação do Dockerfile da aplicação/mysql;


---

# Sistemas para Internet - SecDevOps

***nac:*** Criação de uma aplicação no formato "CRUD" executada em containers com base na linguagem "PHP" e no banco de dados "MySQL";

---

***Importante:***

Instruções sobre modelo de execução e entregáveis podem ser obtidas no [diretório de documentação](https://github.com/fiapsecdevops/php-sample-app/tree/master/docs) ou no portal do aluno;

Duvidas podem ser enviadas para <profhelder.pereira@fiap.com.br>

Esta app foi adaptada do exemplo contido [neste artigo](https://www.tutorialrepublic.com/php-tutorial/php-mysql-crud-application.php)

A estrutura foi criada com base nas seguintes tags:

- frontend-0.1: Versão de testes SEM conexão com o banco para a primeira parte da NAC;
- stable:  Versão COM as linhas de conexão com o banco configuradas, será necessário que o MySQL esteja operante para testes faltando apenas a criação do Dockerfile da aplicação/mysql;


---

#CRUD em PHP utilizando docker

***Observações:***
Certifique-se de que ja tenha o docker e o GIT instalado em sua máquina. 
Caso ainda não tenha, acesse os segintes links e faça a instalação conforme as instruções:

[instalar o git](https://git-scm.com/) 

[instalar Docker](https://www.docker.com/get-docker) 



Agora abra o Terminal se estiver em um MAC ou Linux, caso esteja utilizando Windows o Prompt de comando ou Git bash e clone o projeto:

```bash
$ git clone https://github.com/GabrielEQ/php-sample-app
```

* Dentro da pasta frontend crie um arquivo chamado **Dockerfile**

*Esse é o arquivo que passará as instruções para a execução da aplicação em container com o Docker.*

Antes de escrever as instruções, acesse o [Docker hub](https://hub.docker.com/_/php/) e escolha a versão do PHP que será utilizada no projeto. Nessa aplicação utilizaremos a ``7.2-apache`` 


* No arquivo **Dockerfile** primeiramente informe a linguagem e a versão que irá ser utilizada, no caso a  7.2 com o Apache. 

```Docker
FROM php:7.2-apache
```

* Depois informe o diretório será trabalhado

```Docker
WORKDIR /var/www/html/
```

* Agora copie os arquivos do diretório. *O ponto serve para informar que é apartir da raiz do projeto*

```Docker
COPY . /var/www/html/
```

Agora abra o terminal do Docker e faça o pull do da versão do PHP para o container

```Docker
$ docker pull php:7.2-apache
```

Após terminar o processo é hora de fazer o build da imagem
No comando que será executado precisamos informar o ponto para definir o diretório raiz, o parâmetro `-t` e difinir uma tag

Build:

```Docker
$ docker build . -t frontend-php
```

Execute a imagem passando o `run`, `-d` para rodar em background, `-p` para apontar a porta em que a aplicação estará rodando. Nesse caso utilizaremos a porta padrão do navegador a 80 `--rm` para remover se já houver alguma aplicalçao, ```--name``` para definir um nome e por ultimo a versão:

```Docker
$ docker run -d -p 80:80 --rm --name front front-php:0.1
```

---

Agora precisamos criar uma outra imagem para o Banco de dados
===

* Dentro da pasta backend, crie outro arquivo Dockerfile e 

Acesse o Docker hub novamente, agora na página do [Mysql](https://hub.docker.com/_/mysql/) 

Precisamos realizar o build do banco de dados:

```Docker
$ docker build . -t db:0.0.1
```

Para rodar o banco precisamos passar alguns parâmetros como, nome do banco e senha. 

```Docker
$ docker run -d -e MYSQL_DATABASE='demo'  -e MYSQL_ALLOW_EMPTY_PASSWORD='yes' --name backend db:0.0.1
```

Para conferir se o banco está rodando:

```Docker
$ docker logs backend -f
```

Para conectar o backend no frontend precisamos conectar o no através de uma instrução no dockerfile do frontend:

```Docker
$ RUN docker-php-ext-install mysqli
```

Para testar a conexão digite: 

```Docker
$ docker exec -ti backend mysql -u root -p
```

