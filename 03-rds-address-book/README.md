# Lab — Amazon RDS and Address Book

[English](#english) · [Português](#português)

---

## English

## Objective

The objective of this lab was to practice creating and configuring a relational database using Amazon RDS and integrating it with a web application.

Building on the network infrastructure created in the previous lab, a dedicated Security Group for the database, a DB Subnet Group, and an Amazon RDS for MySQL instance with a Multi-AZ deployment were configured.

At the end of the lab, the Address Book application was configured to use the RDS database and tested through a web browser.

## Architecture

The lab uses the network infrastructure previously created in the `Lab VPC`, which contains public and private subnets distributed across two Availability Zones.

The two private subnets were used for the database:

* Private Subnet 1 — `10.0.1.0/24`
* Private Subnet 2 — `10.0.3.0/24`

Both subnets were associated with the `DB Subnet Group`, allowing Amazon RDS to use the selected network resources across different Availability Zones.

The `DB Security Group` was created and configured to allow MySQL connections on port `3306` only from resources associated with the `Web Security Group`.

The RDS instance was configured without public access and using the `DB Security Group`.

The Multi-AZ deployment was configured with two database instances across Availability Zones, providing a primary and standby database environment.

The application hosted on the EC2 instance communicates with the RDS database through port `3306`.

In simplified form:

```mermaid
flowchart TD
    VPC["Lab VPC"]

    VPC --> PUBLIC["Public Subnets"]
    VPC --> PRIVATE["Private Subnets"]

    PUBLIC --> EC2["Web Server / EC2"]

    PRIVATE --> SUB1["Private Subnet 1<br/>10.0.1.0/24"]
    PRIVATE --> SUB2["Private Subnet 2<br/>10.0.3.0/24"]

    SUB1 --> DBGROUP["DB Subnet Group"]
    SUB2 --> DBGROUP

    EC2 -->|"Port 3306"| RDS["Amazon RDS<br/>MySQL / Multi-AZ"]

    DBGROUP --> RDS
```

## Services and Resources Used

* **Amazon RDS** — creation and operation of the MySQL database
* **DB Subnet Group** — definition of the private subnets used by RDS
* **Security Groups** — control of application and database traffic
* **Amazon VPC** — virtual network where the lab resources are configured
* **Amazon EC2** — server hosting the web application
* **Address Book** — application used to validate database connectivity and data persistence

## Steps Performed

### 1. Database Security Group Creation

The `DB Security Group` was created in the `Lab VPC`.

An inbound rule was configured to allow **MySQL/Aurora traffic on port `3306`**, with the `Web Security Group` specified as the source.

This configuration restricts inbound database connections to resources associated with the `Web Security Group`.

![Database Security Group](./db-security-group.png)

### 2. DB Subnet Group Creation

The `DB Subnet Group` was created in the `Lab VPC`.

The group was configured using private subnets distributed across two Availability Zones:

* Private Subnet 1 — `10.0.1.0/24`
* Private Subnet 2 — `10.0.3.0/24`

This configuration provides Amazon RDS with the selected private subnets for database deployment.

![DB Subnet Group Details](./subnet-group-details.png)

### 3. RDS Instance Creation and Configuration

The `lab-db` instance was created using **Amazon RDS for MySQL**.

The main configuration settings were:

* **Engine:** MySQL
* **Template:** Dev/Test
* **Deployment:** Multi-AZ DB instance deployment — 2 instances
* **DB instance identifier:** `lab-db`
* **Master username:** `main`
* **Instance class:** `db.t3.medium`
* **Storage type:** General Purpose SSD (gp3)
* **Allocated storage:** `20 GiB`
* **VPC:** `Lab VPC`
* **DB Subnet Group:** `DB Subnet Group`
* **Public access:** No
* **Security Group:** `DB Security Group`
* **Initial database name:** `lab`

The instance was created without public access and configured to use the dedicated database Security Group.

After the instance was created, its status was monitored until it became available. The instance endpoint was then obtained to configure the application.

![RDS Database Running](./db.png)

### 4. Address Book Application Configuration and Testing

The web application hosted on the EC2 instance was accessed through a browser and configured to use the previously created RDS instance.

The following information was provided in the application:

* **Endpoint:** endpoint of the `lab-db` instance
* **Database:** `lab`
* **Username:** `main`

After the configuration was submitted, the application began using the RDS database to store Address Book information.

![Address Book Application Running](./running-application.png)

## Result

At the end of the lab, an Amazon RDS for MySQL database was configured using a Multi-AZ deployment, a DB Subnet Group with private subnets distributed across two Availability Zones, and a dedicated Security Group to control database access.

The Address Book application was successfully configured to use the RDS database, demonstrating communication between an application running on EC2 and a database running on Amazon RDS.

The lab provided hands-on experience with the following concepts:

* Amazon RDS
* MySQL on AWS
* DB Subnet Groups
* Security Groups
* Private database access
* Application-to-database communication
* Multi-AZ environments
* Data persistence
* Integration between AWS services

---

## Português

## Objetivo

Este laboratório teve como objetivo praticar a criação e configuração de um banco de dados relacional utilizando o Amazon RDS e sua integração com uma aplicação web.

A partir da infraestrutura de rede criada no laboratório anterior, foram configurados um Security Group específico para o banco de dados, um DB Subnet Group e uma instância Amazon RDS for MySQL com implantação Multi-AZ.

Ao final do laboratório, a aplicação Address Book foi configurada para utilizar o banco de dados RDS e testada através de um navegador.

## Arquitetura

O laboratório utiliza a infraestrutura de rede criada anteriormente na `Lab VPC`, que possui subnets públicas e privadas distribuídas em duas Availability Zones.

Para o banco de dados, foram utilizadas as duas subnets privadas:

* Private Subnet 1 — `10.0.1.0/24`
* Private Subnet 2 — `10.0.3.0/24`

As duas subnets foram associadas ao `DB Subnet Group`, permitindo que o Amazon RDS utilize os recursos de rede selecionados em diferentes Availability Zones.

Foi criado o `DB Security Group`, configurado para permitir conexões MySQL na porta `3306` somente a partir de recursos associados ao `Web Security Group`.

A instância RDS foi configurada sem acesso público e utilizando o `DB Security Group`.

A implantação Multi-AZ foi configurada com duas instâncias de banco de dados distribuídas entre Availability Zones, proporcionando um ambiente com instância primária e standby.

A aplicação hospedada na instância EC2 se comunica com o banco de dados RDS através da porta `3306`.

De forma simplificada:

```mermaid
flowchart TD
    VPC["Lab VPC"]

    VPC --> PUBLIC["Public Subnets"]
    VPC --> PRIVATE["Private Subnets"]

    PUBLIC --> EC2["Web Server / EC2"]

    PRIVATE --> SUB1["Private Subnet 1<br/>10.0.1.0/24"]
    PRIVATE --> SUB2["Private Subnet 2<br/>10.0.3.0/24"]

    SUB1 --> DBGROUP["DB Subnet Group"]
    SUB2 --> DBGROUP

    EC2 -->|"Port 3306"| RDS["Amazon RDS<br/>MySQL / Multi-AZ"]

    DBGROUP --> RDS
```

## Serviços e Recursos Utilizados

* **Amazon RDS** — criação e execução do banco de dados MySQL
* **DB Subnet Group** — definição das subnets privadas utilizadas pelo RDS
* **Security Groups** — controle do tráfego da aplicação e do banco de dados
* **Amazon VPC** — rede virtual onde os recursos do laboratório estão configurados
* **Amazon EC2** — servidor que hospeda a aplicação web
* **Address Book** — aplicação utilizada para validar a conexão com o banco de dados e a persistência dos dados

## Etapas Realizadas

### 1. Criação do Security Group do Banco de Dados

Foi criado o `DB Security Group` na `Lab VPC`.

Foi configurada uma regra de entrada para permitir tráfego **MySQL/Aurora na porta `3306`**, tendo como origem o `Web Security Group`.

Essa configuração restringe as conexões de entrada ao banco de dados aos recursos associados ao `Web Security Group`.

![Security Group do banco de dados](./db-security-group.png)

### 2. Criação do DB Subnet Group

Foi criado o `DB Subnet Group` na `Lab VPC`.

O grupo foi configurado utilizando subnets privadas distribuídas em duas Availability Zones:

* Private Subnet 1 — `10.0.1.0/24`
* Private Subnet 2 — `10.0.3.0/24`

Essa configuração fornece ao Amazon RDS as subnets privadas selecionadas para a implantação do banco de dados.

![Detalhes do DB Subnet Group](./subnet-group-details.png)

### 3. Criação e Configuração da Instância RDS

Foi criada a instância `lab-db` utilizando o **Amazon RDS for MySQL**.

As principais configurações utilizadas foram:

* **Engine:** MySQL
* **Template:** Dev/Test
* **Deployment:** Multi-AZ DB instance deployment — 2 instances
* **DB instance identifier:** `lab-db`
* **Master username:** `main`
* **Instance class:** `db.t3.medium`
* **Storage type:** General Purpose SSD (gp3)
* **Allocated storage:** `20 GiB`
* **VPC:** `Lab VPC`
* **DB Subnet Group:** `DB Subnet Group`
* **Public access:** No
* **Security Group:** `DB Security Group`
* **Initial database name:** `lab`

A instância foi criada sem acesso público e configurada para utilizar o Security Group específico do banco de dados.

Após a criação, a instância foi acompanhada até ficar disponível para utilização. Em seguida, o endpoint da instância foi obtido para configurar a aplicação.

![Banco de dados RDS em execução](./db.png)

### 4. Configuração e Teste da Aplicação Address Book

A aplicação web hospedada na instância EC2 foi acessada através do navegador e configurada para utilizar a instância RDS criada anteriormente.

Foram informados na aplicação:

* **Endpoint:** endpoint da instância `lab-db`
* **Database:** `lab`
* **Username:** `main`

Após o envio das configurações, a aplicação passou a utilizar o banco de dados RDS para armazenar as informações do Address Book.

![Address Book funcionando](./running-application.png)

## Resultado

Ao final do laboratório, foi possível configurar um banco de dados Amazon RDS for MySQL utilizando uma implantação Multi-AZ, um DB Subnet Group com subnets privadas distribuídas em duas Availability Zones e um Security Group específico para controlar o acesso ao banco de dados.

A aplicação Address Book foi configurada com sucesso para utilizar o banco de dados RDS, demonstrando a comunicação entre uma aplicação executada em uma instância EC2 e um banco de dados executado no Amazon RDS.

O laboratório proporcionou experiência prática com os seguintes conceitos:

* Amazon RDS
* MySQL na AWS
* DB Subnet Groups
* Security Groups
* Acesso privado ao banco de dados
* Comunicação entre aplicação e banco de dados
* Ambientes Multi-AZ
* Persistência de dados
* Integração entre serviços AWS
