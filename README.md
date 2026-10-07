# Cloud Labs

[English](#english) · [Português](#português)

---

## English

This repository contains hands-on Cloud Computing labs developed during my AWS and Cloud learning journey.

The labs document practical exercises involving AWS infrastructure, identity and access management, databases, command-line tools, instance management, static website deployment, and cloud troubleshooting.

Each lab includes the resources used, the steps performed, relevant configurations, and the results obtained during the exercise.

## Labs

### 01. VPC, Subnets, Security Groups, and EC2

Hands-on lab focused on creating and configuring basic AWS network infrastructure and launching an EC2 instance in a public subnet to host a web server.

**Services and Resources Used:**

* Amazon VPC
* Amazon EC2
* Subnets
* Security Groups
* Internet Gateway
* NAT Gateway
* Route Tables

[View Documentation](./01-vpc-ec2-webserver/)

---

### 02. IAM, Users, Groups, and Policies

Hands-on lab focused on AWS Identity and Access Management (IAM), including password policies, users, groups, managed policies, inline policies, and permission testing with Amazon S3 and Amazon EC2.

**Services and Resources Used:**

* AWS Identity and Access Management (IAM)
* Amazon S3
* Amazon EC2

[View Documentation](./02-iam-users-groups-policies/)

---

### 03. Amazon RDS and Address Book

Hands-on lab focused on creating and configuring an Amazon RDS MySQL database and connecting it to an Address Book application running on EC2.

The lab included the configuration of a DB Subnet Group and a Security Group for database access.

**Services and Resources Used:**

* Amazon RDS
* MySQL
* DB Subnet Groups
* Security Groups
* Amazon VPC
* Amazon EC2

[View Documentation](./03-rds-address-book/)

---

### 04. AWS CLI, EC2, and IAM

Hands-on lab focused on installing and configuring the AWS Command Line Interface (AWS CLI) on an EC2 instance and using it to interact with IAM resources.

The lab included querying IAM users and policies and retrieving a policy version through the command line.

**Services and Resources Used:**

* AWS Command Line Interface (AWS CLI)
* Amazon EC2
* AWS Identity and Access Management (IAM)
* SSH

[View Documentation](./04-cli-install-config/)

---

### 05. AWS Systems Manager

Hands-on lab focused on using AWS Systems Manager to manage and interact with an EC2 instance without relying on a traditional SSH session.

The lab included inventory collection, Run Command, Parameter Store, Session Manager, and application configuration.

**Services and Resources Used:**

* AWS Systems Manager
* Fleet Manager
* Run Command
* Parameter Store
* Session Manager
* Amazon EC2
* Amazon VPC

[View Documentation](./05-systems-manager/)

---

### 06. Creating a Website on Amazon S3

Hands-on lab focused on using the AWS CLI from an EC2 instance to create and configure an Amazon S3 bucket and deploy a static website.

The lab included IAM user configuration, S3 access settings, website hosting, object uploads, and a Bash script for repeating website updates.

**Services and Resources Used:**

* Amazon S3
* AWS Command Line Interface (AWS CLI)
* AWS Identity and Access Management (IAM)
* Amazon EC2
* AWS Systems Manager Session Manager
* S3 Static Website Hosting
* S3 Bucket ACLs
* Bash

[View Documentation](./06-s3-website/)

---

### 07. EC2 CLI Troubleshooting

Hands-on lab focused on deploying a LAMP-based Café Web Application on Amazon EC2 using the AWS CLI and troubleshooting intentional configuration issues.

The lab included identifying an AMI and Region mismatch, troubleshooting HTTP connectivity with `nmap`, correcting Security Group ingress rules, and validating the application and database functionality.

**Services and Resources Used:**

* Amazon EC2
* Amazon VPC
* Subnets
* Security Groups
* AWS Command Line Interface (AWS CLI)
* Linux
* Apache
* PHP
* MariaDB
* Bash
* `nmap`
* EC2 User Data / cloud-init

[View Documentation](./07-ec2-cli-troubleshooting/)

---

## Português

Este repositório reúne laboratórios práticos de Cloud Computing desenvolvidos durante minha jornada de aprendizado em AWS e Cloud.

Os laboratórios documentam exercícios práticos envolvendo infraestrutura na AWS, gerenciamento de identidade e acesso, bancos de dados, ferramentas de linha de comando, gerenciamento de instâncias, deploy de websites estáticos e troubleshooting em Cloud.

Cada laboratório apresenta os recursos utilizados, as etapas realizadas, as principais configurações e os resultados obtidos durante o exercício.

## Labs

### 01. VPC, Subnets, Security Groups e EC2

Laboratório prático focado na criação e configuração de uma infraestrutura básica de rede na AWS e no lançamento de uma instância EC2 em uma subnet pública para hospedar um web server.

**Serviços e Recursos Utilizados:**

* Amazon VPC
* Amazon EC2
* Subnets
* Security Groups
* Internet Gateway
* NAT Gateway
* Route Tables

[Ver Documentação](./01-vpc-ec2-webserver/)

---

### 02. IAM, Usuários, Grupos e Políticas

Laboratório prático focado no AWS Identity and Access Management (IAM), incluindo políticas de senha, usuários, grupos, políticas gerenciadas, políticas inline e testes de permissões com Amazon S3 e Amazon EC2.

**Serviços e Recursos Utilizados:**

* AWS Identity and Access Management (IAM)
* Amazon S3
* Amazon EC2

[Ver Documentação](./02-iam-users-groups-policies/)

---

### 03. Amazon RDS e Address Book

Laboratório prático focado na criação e configuração de um banco de dados MySQL no Amazon RDS e na conexão com uma aplicação Address Book executada em uma instância EC2.

O laboratório incluiu a configuração de um DB Subnet Group e de um Security Group para acesso ao banco de dados.

**Serviços e Recursos Utilizados:**

* Amazon RDS
* MySQL
* DB Subnet Groups
* Security Groups
* Amazon VPC
* Amazon EC2

[Ver Documentação](./03-rds-address-book/)

---

### 04. AWS CLI, EC2 e IAM

Laboratório prático focado na instalação e configuração da AWS Command Line Interface (AWS CLI) em uma instância EC2 e na utilização da ferramenta para interagir com recursos do IAM.

O laboratório incluiu consultas de usuários e políticas do IAM e a recuperação de uma versão de política por meio da linha de comando.

**Serviços e Recursos Utilizados:**

* AWS Command Line Interface (AWS CLI)
* Amazon EC2
* AWS Identity and Access Management (IAM)
* SSH

[Ver Documentação](./04-cli-install-config/)

---

### 05. AWS Systems Manager

Laboratório prático focado na utilização do AWS Systems Manager para gerenciar e interagir com uma instância EC2 sem depender de uma sessão SSH tradicional.

O laboratório incluiu coleta de inventário, Run Command, Parameter Store, Session Manager e configuração de uma aplicação.

**Serviços e Recursos Utilizados:**

* AWS Systems Manager
* Fleet Manager
* Run Command
* Parameter Store
* Session Manager
* Amazon EC2
* Amazon VPC

[Ver Documentação](./05-systems-manager/)

---

### 06. Criação de um Website no Amazon S3

Laboratório prático focado na utilização da AWS CLI a partir de uma instância EC2 para criar e configurar um bucket Amazon S3 e realizar o deploy de um website estático.

O laboratório incluiu a configuração de usuário e permissões no IAM, configurações de acesso do S3, hospedagem do website, upload de objetos e criação de um script Bash para repetir as atualizações do website.

**Serviços e Recursos Utilizados:**

* Amazon S3
* AWS Command Line Interface (AWS CLI)
* AWS Identity and Access Management (IAM)
* Amazon EC2
* AWS Systems Manager Session Manager
* S3 Static Website Hosting
* S3 Bucket ACLs
* Bash

[Ver Documentação](./06-s3-website/)

---

### 07. Troubleshooting de EC2 via AWS CLI

Laboratório prático focado no deploy de uma Café Web Application baseada em LAMP em uma instância Amazon EC2 utilizando a AWS CLI e na resolução de problemas de configuração inseridos intencionalmente.

O laboratório incluiu a identificação de uma incompatibilidade entre AMI e Região, troubleshooting de conectividade HTTP utilizando `nmap`, correção de regras de entrada do Security Group e validação do funcionamento da aplicação e do banco de dados.

**Serviços e Recursos Utilizados:**

* Amazon EC2
* Amazon VPC
* Subnets
* Security Groups
* AWS Command Line Interface (AWS CLI)
* Linux
* Apache
* PHP
* MariaDB
* Bash
* `nmap`
* EC2 User Data / cloud-init

[Ver Documentação](./07-ec2-cli-troubleshooting/)
