# Lab — Creating a Website on Amazon S3

[English](#english) · [Português](#português)

---

## English

## Objective

The objective of this lab was to practice using the **AWS Command Line Interface (AWS CLI)** from an Amazon EC2 instance to create and configure an Amazon S3 bucket and deploy a static website.

During the lab, AWS CLI commands were used to create an S3 bucket, create and configure an IAM user with full access to Amazon S3, configure the bucket for static website hosting, upload website files, and create a Bash script to make future website updates repeatable.

The lab also provided practical experience with S3 access controls, object permissions, static website hosting, and basic Bash scripting.

## Architecture

The infrastructure used in this lab consisted of an Amazon Linux EC2 instance used as the command-line environment and an Amazon S3 bucket configured to host the static website.

The EC2 instance was accessed through **AWS Systems Manager Session Manager** and used to execute AWS CLI commands for managing IAM and Amazon S3 resources.

The architecture can be represented as follows:

```mermaid
flowchart LR
    A["AWS Management Console"] --> B["AWS Systems Manager"]
    B --> C["EC2 Instance"]

    C --> D["AWS CLI"]
    D --> E["AWS IAM"]
    D --> F["Amazon S3"]

    E --> G["awsS3user"]
    F --> H["Static Website"]
    H --> I["Website Clients"]

    C --> J["Website Source Files"]
    J --> D
    D --> F
```

## Services and Resources Used

* **Amazon EC2** — Linux instance used as the command-line environment for the lab
* **AWS Systems Manager Session Manager** — used to access the EC2 instance through a browser-based shell
* **AWS CLI** — used to manage IAM and Amazon S3 resources from the EC2 instance
* **AWS IAM** — used to create and configure a dedicated IAM user for Amazon S3 access
* **Amazon S3** — used to store the website files and host the static website
* **S3 Static Website Hosting** — used to make the website available through the S3 website endpoint
* **S3 Bucket ACLs** — used to grant public read access to the uploaded website files
* **Bash** — used to create a repeatable website update script

## Steps Performed

### 1. Connecting to the EC2 Instance with Session Manager

The first task was to connect to the Amazon Linux EC2 instance through **AWS Systems Manager Session Manager**.

A browser-based Session Manager session was started using the `InstanceSessionUrl` provided by the lab environment.

After connecting to the instance, the user and home directory were changed to `ec2-user`:

```bash
sudo su -l ec2-user
```

The current working directory was then verified:

```bash
pwd
```

This provided the command-line environment used throughout the remaining tasks.

### 2. Configuring the AWS CLI

The AWS CLI was already installed on the Amazon Linux instance.

The `aws configure` command was used to configure the AWS CLI with the credentials provided by the lab environment:

```bash
aws configure
```

The following configuration values were entered:

```text
AWS Access Key ID: AccessKey
AWS Secret Access Key: SecretKey
Default region name: us-west-2
Default output format: json
```

This allowed the EC2 instance to authenticate requests made through the AWS CLI and interact with the AWS services used throughout the lab.

### 3. Creating an S3 Bucket with the AWS CLI

The next step was to create an Amazon S3 bucket using the AWS CLI.

The bucket was created in the `us-west-2` Region:

```bash
aws s3api create-bucket --bucket laisrdrgs17 --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2
```

The command returned a JSON response containing the location of the newly created bucket.

The bucket was then used as the storage location for the static website files.

### 4. Creating and Configuring an IAM User

A new IAM user named `awsS3user` was created using the AWS CLI:

```bash
aws iam create-user --user-name awsS3user
```

A console login profile was then created for the user:

```bash
aws iam create-login-profile --user-name awsS3user --password <lab-password>
```

The AWS account ID provided by the lab environment was used to sign in to the AWS Management Console as the new IAM user.

To identify the AWS managed policies related to Amazon S3, the following command was executed:

```bash
aws iam list-policies --query "Policies[?contains(PolicyName,'S3')]"
```

The policy that grants full access to Amazon S3 was then attached to the `awsS3user` user:

```bash
aws iam attach-user-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --user-name awsS3user
```

This allowed the newly created IAM user to access and manage Amazon S3 resources through the AWS Management Console.

### 5. Adjusting S3 Bucket Permissions

The S3 bucket permissions were then modified so that the bucket could serve the website publicly.

In the Amazon S3 console, **Block all public access** was disabled for the bucket.

The change was confirmed through the AWS Management Console.

The bucket's **Object Ownership** configuration was also modified to enable ACLs.

The following settings were configured:

```text
Block all public access: Disabled
Object Ownership: ACLs enabled
```

These changes allowed the website objects to use ACL-based public read permissions when uploaded to the bucket.

### 6. Extracting the Website Files

The website files provided by the lab were stored in the `static-website-v2.tar.gz` archive.

The archive was extracted using:

```bash
cd ~/sysops-activity-files
tar xvzf static-website-v2.tar.gz
cd static-website
```

The contents of the directory were then verified with:

```bash
ls
```

The extracted files included:

```text
css
images
index.html
```

![Extracted static website files](./static-website-files.png)

The `index.html` file contained the main page of the Café website, while the `css` and `images` directories contained the resources required by the page.

### 7. Deploying the Website to Amazon S3

The S3 bucket was configured for static website hosting by defining `index.html` as the index document:

```bash
aws s3 website s3://laisrdrgs17/ --index-document index.html
```

The website files were then uploaded recursively to the bucket:

```bash
aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://laisrdrgs17/ --recursive --acl public-read
```

The `--recursive` option ensured that the complete website directory structure was uploaded, while `--acl public-read` granted public read access to the uploaded objects.

The contents of the bucket were verified using:

```bash
aws s3 ls s3://laisrdrgs17/
```

The bucket's **Bucket website endpoint** was then used to access the deployed website.

The Café website was successfully displayed in the browser:

![Café website](./cafe-website.png)

This demonstrated that the static website had been successfully deployed and made accessible through Amazon S3.

### 8. Creating a Script to Update the Website

The final task was to create a Bash script that could be used to repeat the website upload process whenever the local website files were modified.

The command history was first reviewed to identify the S3 upload command:

```bash
history
```

A new script file was created in the EC2 user's home directory:

```bash
cd ~
touch update-website.sh
```

The file was then opened using the `vi` editor:

```bash
vi update-website.sh
```

The script was configured with the Bash interpreter declaration and the S3 upload command:

```bash
#!/bin/bash
aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://laisrdrgs17/ --recursive --acl public-read
```

The file was made executable:

```bash
chmod +x update-website.sh
```

The script could then be executed with:

```bash
./update-website.sh
```

This created a simple deployment mechanism that could be reused whenever the website source files were updated.

### 9. Modifying the Website Locally

To demonstrate the use of the deployment script, the local `index.html` file was modified using the `vi` editor:

```bash
vi sysops-activity-files/static-website/index.html
```

The background colors defined in the HTML were changed to create a revised version of the website.

The colors were updated as follows:

```text
aquamarine → gainsboro
orange → cornsilk
aquamarine → gainsboro
```

The edited HTML file was then saved.

![Editing the website HTML file](./index-html.png)

After the modification, the updated website files were uploaded again by executing the deployment script:

```bash
./update-website.sh
```

The Café website could then be refreshed in the browser to display the updated version.

This demonstrated how a simple Bash script can be used to make the deployment process repeatable instead of manually entering the complete AWS CLI upload command each time.

## Result

At the end of the lab, it was possible to deploy and manage a static website on Amazon S3 using the AWS CLI from an Amazon EC2 instance.

The lab included:

* accessing an Amazon Linux EC2 instance through AWS Systems Manager Session Manager;
* configuring the AWS CLI with the credentials provided by the lab environment;
* creating an Amazon S3 bucket in the `us-west-2` Region;
* creating an IAM user with full access to Amazon S3;
* configuring S3 public access and object ACL settings;
* extracting the static website files;
* configuring S3 static website hosting;
* uploading the website files through the AWS CLI;
* accessing the deployed Café website through the S3 website endpoint;
* creating a Bash script to make website deployments repeatable;
* modifying the website source code and deploying the updated version to Amazon S3.

The lab provided practical experience with **Amazon S3, AWS IAM, AWS CLI, EC2, Session Manager, S3 permissions, static website hosting, and Bash scripting**, demonstrating how a simple static website can be deployed and updated using AWS command-line tools.

---

## Português

## Objetivo

Este laboratório teve como objetivo praticar a utilização da **AWS Command Line Interface (AWS CLI)** a partir de uma instância Amazon EC2 para criar e configurar um bucket Amazon S3 e realizar o deploy de um website estático.

Durante o laboratório, foram utilizados comandos da AWS CLI para criar um bucket S3, criar e configurar um usuário IAM com acesso completo ao Amazon S3, configurar o bucket para hospedagem de website estático, realizar o upload dos arquivos do website e criar um script Bash para tornar as futuras atualizações do website repetíveis.

O laboratório também proporcionou experiência prática com controles de acesso do S3, permissões de objetos, hospedagem de websites estáticos e criação de scripts básicos em Bash.

## Arquitetura

A infraestrutura utilizada neste laboratório consistiu em uma instância EC2 com Amazon Linux utilizada como ambiente de linha de comando e um bucket Amazon S3 configurado para hospedar o website estático.

A instância EC2 foi acessada por meio do **AWS Systems Manager Session Manager** e utilizada para executar comandos da AWS CLI responsáveis pelo gerenciamento dos recursos do IAM e do Amazon S3.

A arquitetura pode ser representada da seguinte forma:

```mermaid
flowchart LR
    A["AWS Management Console"] --> B["AWS Systems Manager"]
    B --> C["Instância EC2"]

    C --> D["AWS CLI"]
    D --> E["AWS IAM"]
    D --> F["Amazon S3"]

    E --> G["awsS3user"]
    F --> H["Website Estático"]
    H --> I["Clientes"]

    C --> J["Arquivos do Website"]
    J --> D
    D --> F
```

## Serviços e Recursos Utilizados

* **Amazon EC2** — instância Linux utilizada como ambiente de linha de comando do laboratório
* **AWS Systems Manager Session Manager** — utilizado para acessar a instância EC2 por meio de um shell disponibilizado no navegador
* **AWS CLI** — utilizada para gerenciar recursos do IAM e do Amazon S3 a partir da instância EC2
* **AWS IAM** — utilizado para criar e configurar um usuário dedicado ao acesso ao Amazon S3
* **Amazon S3** — utilizado para armazenar os arquivos e hospedar o website estático
* **S3 Static Website Hosting** — utilizado para disponibilizar o website por meio do endpoint de website do S3
* **S3 Bucket ACLs** — utilizados para conceder acesso público de leitura aos arquivos enviados
* **Bash** — utilizado para criar um script reutilizável de atualização do website

## Etapas Realizadas

### 1. Acesso à Instância EC2 com Session Manager

A primeira etapa consistiu em acessar a instância Amazon Linux por meio do **AWS Systems Manager Session Manager**.

Foi iniciada uma sessão baseada no navegador utilizando o valor `InstanceSessionUrl` fornecido pelo ambiente do laboratório.

Após estabelecer a conexão com a instância, o usuário e o diretório inicial foram alterados para `ec2-user`:

```bash
sudo su -l ec2-user
```

Em seguida, o diretório atual foi verificado:

```bash
pwd
```

Esse ambiente de linha de comando foi utilizado durante as demais etapas do laboratório.

### 2. Configuração da AWS CLI

A AWS CLI já estava instalada na instância Amazon Linux.

O comando `aws configure` foi utilizado para configurar a AWS CLI com as credenciais fornecidas pelo ambiente do laboratório:

```bash
aws configure
```

Foram configurados os seguintes valores:

```text
AWS Access Key ID: AccessKey
AWS Secret Access Key: SecretKey
Default region name: us-west-2
Default output format: json
```

Essa configuração permitiu que a instância EC2 realizasse chamadas autenticadas por meio da AWS CLI e interagisse com os serviços utilizados durante o laboratório.

### 3. Criação do Bucket S3 com a AWS CLI

A próxima etapa consistiu em criar um bucket Amazon S3 utilizando a AWS CLI.

O bucket foi criado na região `us-west-2`:

```bash
aws s3api create-bucket --bucket laisrdrgs17 --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2
```

O comando retornou uma resposta em formato JSON contendo a localização do bucket criado.

O bucket passou a ser utilizado como local de armazenamento dos arquivos do website estático.

### 4. Criação e Configuração de um Usuário IAM

Foi criado um novo usuário IAM denominado `awsS3user` utilizando a AWS CLI:

```bash
aws iam create-user --user-name awsS3user
```

Em seguida, foi criado um perfil de login para permitir o acesso do usuário ao AWS Management Console:

```bash
aws iam create-login-profile --user-name awsS3user --password <senha-do-lab>
```

O Account ID fornecido pelo ambiente do laboratório foi utilizado para realizar o login no AWS Management Console como o novo usuário IAM.

Para identificar as políticas gerenciadas pela AWS relacionadas ao Amazon S3, foi executado:

```bash
aws iam list-policies --query "Policies[?contains(PolicyName,'S3')]"
```

A política que concede acesso completo ao Amazon S3 foi então associada ao usuário `awsS3user`:

```bash
aws iam attach-user-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --user-name awsS3user
```

Dessa forma, o usuário IAM criado passou a ter acesso aos recursos do Amazon S3 utilizados no laboratório.

### 5. Ajuste das Permissões do Bucket S3

Em seguida, foram ajustadas as configurações de acesso do bucket para permitir que o website pudesse ser disponibilizado publicamente.

No console do Amazon S3, a opção **Block all public access** foi desabilitada.

A alteração foi confirmada pelo AWS Management Console.

Também foi modificada a configuração de **Object Ownership** para habilitar ACLs.

As seguintes configurações foram utilizadas:

```text
Block all public access: Disabled
Object Ownership: ACLs enabled
```

Essas alterações permitiram que os objetos do website utilizassem ACLs para conceder acesso público de leitura.

### 6. Extração dos Arquivos do Website

Os arquivos do website fornecidos pelo laboratório estavam armazenados no arquivo `static-website-v2.tar.gz`.

O arquivo foi extraído utilizando:

```bash
cd ~/sysops-activity-files
tar xvzf static-website-v2.tar.gz
cd static-website
```

Em seguida, o conteúdo do diretório foi verificado com:

```bash
ls
```

Os arquivos e diretórios extraídos incluíam:

```text
css
images
index.html
```

![Arquivos do website estático extraídos](./static-website-files.png)

O arquivo `index.html` continha a página principal do website Café, enquanto os diretórios `css` e `images` continham os recursos necessários para a exibição da página.

### 7. Deploy do Website no Amazon S3

O bucket S3 foi configurado para hospedagem de website estático, definindo `index.html` como documento principal:

```bash
aws s3 website s3://laisrdrgs17/ --index-document index.html
```

Em seguida, os arquivos do website foram enviados recursivamente para o bucket:

```bash
aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://laisrdrgs17/ --recursive --acl public-read
```

A opção `--recursive` permitiu realizar o upload de toda a estrutura de diretórios do website, enquanto `--acl public-read` concedeu acesso público de leitura aos objetos enviados.

O conteúdo do bucket foi então verificado utilizando:

```bash
aws s3 ls s3://laisrdrgs17/
```

O website foi acessado por meio do **Bucket website endpoint** disponibilizado pelo Amazon S3.

O Café website foi carregado com sucesso no navegador:

![Café website](./cafe-website.png)

Essa etapa demonstrou que o website estático havia sido publicado com sucesso e podia ser acessado por meio do Amazon S3.

### 8. Criação de um Script para Atualização do Website

A etapa final consistiu na criação de um script Bash para tornar repetível o processo de upload do website sempre que os arquivos locais fossem modificados.

Primeiramente, o histórico de comandos foi consultado para localizar o comando de upload para o S3:

```bash
history
```

Um novo arquivo de script foi criado no diretório inicial do usuário:

```bash
cd ~
touch update-website.sh
```

Em seguida, o arquivo foi aberto utilizando o editor `vi`:

```bash
vi update-website.sh
```

O script foi configurado com a declaração do interpretador Bash e o comando de upload para o Amazon S3:

```bash
#!/bin/bash
aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://laisrdrgs17/ --recursive --acl public-read
```

O arquivo foi então marcado como executável:

```bash
chmod +x update-website.sh
```

Depois disso, o script pôde ser executado utilizando:

```bash
./update-website.sh
```

Dessa forma, foi criado um mecanismo simples e reutilizável para realizar novos deployments do website.

### 9. Modificação Local do Website

Para demonstrar a utilização do script de atualização, o arquivo local `index.html` foi modificado utilizando o editor `vi`:

```bash
vi sysops-activity-files/static-website/index.html
```

As cores de fundo definidas no HTML foram alteradas para gerar uma nova versão do website.

As alterações realizadas foram:

```text
aquamarine → gainsboro
orange → cornsilk
aquamarine → gainsboro
```

O arquivo HTML modificado foi então salvo.

![Edição do arquivo HTML do website](./index-html.png)

Após a alteração, os arquivos atualizados foram enviados novamente para o Amazon S3 por meio do script de deployment:

```bash
./update-website.sh
```

Após a execução do script, o website foi atualizado no bucket e pôde ser recarregado no navegador para visualizar as modificações.

Essa etapa demonstrou como um script Bash simples pode tornar o processo de deployment repetível, evitando a necessidade de digitar manualmente todo o comando de upload a cada atualização.

## Resultado

Ao final do laboratório, foi possível realizar o deployment e o gerenciamento de um website estático no Amazon S3 utilizando a AWS CLI a partir de uma instância Amazon EC2.

O laboratório incluiu:

* acesso a uma instância Amazon Linux EC2 por meio do AWS Systems Manager Session Manager;
* configuração da AWS CLI com as credenciais fornecidas pelo ambiente do laboratório;
* criação de um bucket Amazon S3 na região `us-west-2`;
* criação de um usuário IAM com acesso completo ao Amazon S3;
* configuração do acesso público e das ACLs dos objetos do bucket;
* extração dos arquivos do website estático;
* configuração da hospedagem de website estático no Amazon S3;
* upload dos arquivos do website utilizando a AWS CLI;
* acesso ao Café website por meio do endpoint de website do S3;
* criação de um script Bash para tornar os deployments repetíveis;
* modificação do código-fonte do website e publicação da versão atualizada no Amazon S3.

O laboratório proporcionou experiência prática com **Amazon S3, AWS IAM, AWS CLI, Amazon EC2, Session Manager, permissões do S3, hospedagem de websites estáticos e Bash scripting**, demonstrando como um website estático pode ser publicado e atualizado utilizando ferramentas de linha de comando da AWS.
