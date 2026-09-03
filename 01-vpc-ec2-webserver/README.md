# Lab 01 — VPC, Subnet, Security Group e EC2

## Objetivo

Criar uma infraestrutura básica na AWS utilizando uma VPC, subnet, security group e uma instância EC2, configurando a EC2 para hospedar um web server e disponibilizar uma página web para acesso através do navegador.

## Arquitetura

A infraestrutura desenvolvida neste laboratório é composta por:

* VPC
* Subnet
* Security Group
* Instância EC2
* Web Server

O fluxo da infraestrutura é:

**Internet → VPC → Subnet → Security Group → EC2 → Web Server**

## Serviços utilizados

* Amazon VPC
* Amazon EC2
* Security Groups

## Etapas realizadas

### 1. Criação da VPC

Foi criada uma VPC para servir como rede virtual da infraestrutura.

### 2. Configuração da Subnet

Foi criada uma subnet dentro da VPC para hospedar a instância EC2.

### 3. Configuração do Security Group

Foi configurado um Security Group para controlar o tráfego de entrada da instância EC2.

### 4. Criação da EC2

Foi criada uma instância EC2 dentro da subnet configurada anteriormente.

### 5. Configuração do Web Server

A instância EC2 foi configurada para hospedar um web server.

### 6. Teste de acesso

Após a configuração, foi realizado um teste de acesso ao web server através do navegador.

## Evidências

### VPC

![Configuração da VPC](./imagens/vpc.png)

### Web Server hospedado na EC2

![Web Server](./imagens/web-server.png)

## Resultado

Ao final do laboratório, foi possível criar uma infraestrutura básica de rede na AWS e utilizar uma instância EC2 para hospedar um web server, permitindo o acesso à página através do navegador.
