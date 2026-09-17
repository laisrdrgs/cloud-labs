# Lab — Amazon RDS

## Objetivo

Este laboratório teve como objetivo praticar a criação e configuração de um banco de dados utilizando o Amazon RDS, além da configuração dos recursos necessários para permitir a comunicação entre o banco de dados e uma aplicação.

Ao final, a aplicação Address Book foi executada e utilizada para validar o funcionamento da solução com o banco de dados configurado.

## Arquitetura

A infraestrutura utiliza o Amazon RDS como serviço gerenciado para hospedagem do banco de dados.

Para a configuração do RDS, foram utilizados um DB Subnet Group e um Security Group, responsáveis, respectivamente, pela definição das subnets utilizadas pelo banco e pelo controle do tráfego de rede.

A aplicação Address Book foi utilizada para validar a comunicação com o banco de dados e o funcionamento da solução.

De forma simplificada:

```text
Address Book
     |
     v
Amazon RDS
     |
     +----------------------+
     |                      |
DB Subnet Group       Security Group
```

## Serviços utilizados

* **Amazon RDS** — criação e execução do banco de dados
* **DB Subnet Group** — definição das subnets utilizadas pelo RDS
* **Security Group** — controle do tráfego de rede relacionado ao banco de dados
* **Address Book** — aplicação utilizada para validar o funcionamento da solução

## Etapas realizadas

### 1. Configuração do Security Group

Foi configurado um Security Group para controlar o tráfego de rede relacionado ao banco de dados utilizado pelo laboratório.

A configuração realizada pode ser visualizada abaixo.

[Security Group do banco de dados](screenshots/db-security-group.png) ([image](screenshots/db-security-group.png))

### 2. Configuração do DB Subnet Group

Foi configurado um DB Subnet Group para definir as subnets que podem ser utilizadas pela instância do Amazon RDS.

Os detalhes da configuração podem ser visualizados abaixo.

[Detalhes do DB Subnet Group](screenshots/subnet-group-details.png) ([image](screenshots/subnet-group-details.png))

### 3. Criação e execução do banco de dados

Foi criada uma instância de banco de dados utilizando o Amazon RDS.

Após a criação, a instância foi colocada em execução e utilizada pela aplicação do laboratório.

[Banco de dados RDS em execução](screenshots/db.png) ([image](screenshots/db.png))

### 4. Execução e teste da aplicação

Após a configuração do banco de dados e dos recursos necessários, a aplicação Address Book foi executada para validar o funcionamento da solução.

A aplicação foi acessada através do navegador e apresentou funcionamento conforme esperado.

[Address Book funcionando](screenshots/running-application.png) ([image](screenshots/running-application.png))

## Resultado

Ao final do laboratório, foi possível criar e configurar uma instância de banco de dados utilizando o Amazon RDS, configurar um DB Subnet Group e um Security Group e validar o funcionamento da aplicação Address Book.

O laboratório permitiu praticar conceitos relacionados à utilização de bancos de dados gerenciados na AWS, configuração de rede e segurança e integração entre uma aplicação e um banco de dados.
