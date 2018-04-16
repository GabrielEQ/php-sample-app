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

Doc . do Mysql: https://hub.docker.com/_/mysql/

Build:
docker build . -t db:0.0.1

Run:
docker run -d -e MYSQL_DATABASE='demo'  -e MYSQL_ALLOW_EMPTY_PASSWORD='yes' --name backend db:0.0.1

Logs:
docker logs backend -f

Testando a conexão no banco:
docker exec -ti backend mysql -u root -p
