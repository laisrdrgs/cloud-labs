# Lab — AWS CLI, EC2, and IAM

[English](#english) · [Português](#português)

---

## English

## Objective

The objective of this lab was to practice installing and configuring the **AWS Command Line Interface (AWS CLI)** on an EC2 instance.

At the end of the lab, the AWS CLI was configured to access the AWS account used during the lab and was used to query **AWS Identity and Access Management (IAM)** resources, including users and policies.

The `lab_policy` policy was also retrieved through the AWS CLI using its default version, and the result was saved to a JSON file.

## Architecture

The lab used an EC2 instance accessed remotely through SSH.

The AWS CLI was installed and configured on the EC2 instance to interact with AWS IAM. The CLI was then used to query IAM users, policies, and policy versions.

```mermaid
flowchart LR
    A["Local Computer"] -->|SSH| B["EC2 Instance"]
    B --> C["AWS CLI"]
    C -->|"AWS API"| D["AWS IAM"]

    D --> E["Users"]
    D --> F["Policies"]
    D --> G["Policy Versions"]
```

## Services and Resources Used

* **Amazon EC2** — instance used to run the AWS CLI
* **AWS CLI** — command-line tool used to interact with AWS services
* **AWS IAM** — service used to query users and policies
* **SSH** — protocol used for remote access to the EC2 instance

## Steps Performed

### 1. Connecting to the EC2 Instance

An SSH connection was established to the EC2 instance provided by the lab.

After authentication, the instance terminal was accessed and the commands required for the lab activities were executed.

![SSH connection to the instance](./login.png)

### 2. Installing the AWS CLI

The AWS CLI was installed directly on the EC2 instance.

The installer was downloaded using `curl`:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

The downloaded file was then extracted:

```bash
unzip -u awscliv2.zip
```

The installation was performed with:

```bash
sudo ./aws/install
```

After installation, the following command was used to verify that the AWS CLI was available:

```bash
aws --version
```

The `aws help` command was also used to access the AWS CLI documentation directly from the terminal:

```bash
aws help
```

### 3. Reviewing IAM Configuration

Before using the AWS CLI, some IAM configurations were reviewed in the AWS Management Console.

The information reviewed included:

* the IAM user used in the lab;
* the `lab_policy` policy;
* the default policy version;
* the credentials later used to configure the AWS CLI.

The credentials used during the lab were not included in this documentation or repository.

### 4. Configuring the AWS CLI

After installation, the AWS CLI was configured to access the AWS account used in the lab.

The following command was executed:

```bash
aws configure
```

The following parameters were provided:

```text
AWS Access Key ID
AWS Secret Access Key
Default region name: us-west-2
Default output format: json
```

The credentials used in this step were not included in the documentation or repository.

### 5. Querying IAM Users

After configuring the AWS CLI, an IAM access test was performed using:

```bash
aws iam list-users
```

The command returns the IAM users available in the AWS account in JSON format.

The result confirmed that the AWS CLI was configured and could query the IAM service.

![IAM users query](./users.png)

### 6. Querying IAM Policies

Next, customer-managed policies were queried using:

```bash
aws iam list-policies --scope Local
```

The `--scope Local` parameter was used to filter customer-managed policies.

The `lab_policy` policy was identified in the results.

The returned information included:

* `PolicyName`
* `Arn`
* `DefaultVersionId`

The `DefaultVersionId` property was used to identify the policy version retrieved in the next step.

![IAM policies query](./policies.png)

### 7. Retrieving the `lab_policy` Version

After identifying the `lab_policy` policy and its default version, the `get-policy-version` command was used to retrieve the policy document in JSON format.

The command used was:

```bash
aws iam get-policy-version \
  --policy-arn arn:aws:iam::<AWS_ACCOUNT_ID>:policy/lab_policy \
  --version-id v1
```

The default version identified during the lab was `v1`.

The command returned the information for the policy version, including the JSON document corresponding to `lab_policy`.

![Retrieving the policy version](./policy-version.png)

### 8. Saving the Policy in JSON Format

The command output was saved to a file using the `>` redirection operator:

```bash
aws iam get-policy-version \
  --policy-arn arn:aws:iam::<AWS_ACCOUNT_ID>:policy/lab_policy \
  --version-id v1 \
  > lab_policy.json
```

The `>` operator redirects the command output to the `lab_policy.json` file.

The resulting file could then be viewed using:

```bash
cat lab_policy.json
```

This stored the response returned by the AWS CLI as a JSON file on the EC2 instance.

## Result

The lab was completed by installing and configuring the AWS CLI on an EC2 instance and using it to interact with AWS IAM.

IAM users and policies were queried, and the `lab_policy` policy version was retrieved through the command line and saved as a JSON file.

---

## Português

## Objetivo

O objetivo deste laboratório foi praticar a instalação e configuração da **AWS Command Line Interface (AWS CLI)** em uma instância EC2.

Ao final, a AWS CLI foi configurada para acessar a conta AWS utilizada no laboratório e utilizada para consultar recursos do **AWS Identity and Access Management (IAM)**, incluindo usuários e políticas.

Também foi realizada a recuperação da política `lab_policy` por meio da AWS CLI, utilizando sua versão padrão e salvando o resultado em um arquivo JSON.

## Arquitetura

O laboratório utilizou uma instância EC2 acessada remotamente por meio de SSH.

A AWS CLI foi instalada e configurada na instância EC2 para interagir com o AWS IAM. Em seguida, a CLI foi utilizada para consultar usuários, políticas e versões de políticas do IAM.

```mermaid
flowchart LR
    A["Computador Local"] -->|SSH| B["Instância EC2"]
    B --> C["AWS CLI"]
    C -->|"API da AWS"| D["AWS IAM"]

    D --> E["Usuários"]
    D --> F["Políticas"]
    D --> G["Versões de Políticas"]
```

## Serviços e Recursos Utilizados

* **Amazon EC2** — instância utilizada para executar a AWS CLI
* **AWS CLI** — ferramenta utilizada para interagir com os serviços da AWS por linha de comando
* **AWS IAM** — serviço utilizado para consultar usuários e políticas
* **SSH** — protocolo utilizado para acesso remoto à instância EC2

## Etapas Realizadas

### 1. Conexão com a Instância EC2

Foi estabelecida uma conexão SSH com a instância EC2 disponibilizada pelo laboratório.

Após a autenticação, foi possível acessar o terminal da instância e executar os comandos necessários para a realização das atividades.

![Conexão SSH com a instância](./login.png)

### 2. Instalação da AWS CLI

A AWS CLI foi instalada diretamente na instância EC2.

O instalador foi baixado utilizando o `curl`:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Em seguida, o arquivo foi descompactado:

```bash
unzip -u awscliv2.zip
```

A instalação foi realizada com:

```bash
sudo ./aws/install
```

Após a instalação, foi utilizado o comando abaixo para verificar se a AWS CLI estava disponível:

```bash
aws --version
```

Também foi utilizado o comando `aws help` para acessar a documentação da AWS CLI diretamente pelo terminal:

```bash
aws help
```

### 3. Observação da Configuração do IAM

Antes de utilizar a AWS CLI, foram observadas algumas configurações do IAM no AWS Management Console.

Entre as informações verificadas estavam:

* o usuário IAM utilizado no laboratório;
* a política `lab_policy`;
* a versão padrão da política;
* as credenciais utilizadas posteriormente na configuração da AWS CLI.

As credenciais utilizadas durante o laboratório não foram incluídas nesta documentação ou no repositório.

### 4. Configuração da AWS CLI

Após a instalação, a AWS CLI foi configurada para acessar a conta AWS utilizada no laboratório.

Para iniciar a configuração, foi executado:

```bash
aws configure
```

Foram informados os seguintes parâmetros:

```text
AWS Access Key ID
AWS Secret Access Key
Default region name: us-west-2
Default output format: json
```

As credenciais utilizadas nesta etapa não foram incluídas na documentação ou no repositório.

### 5. Consulta de Usuários do IAM

Após a configuração da AWS CLI, foi realizado um teste de acesso ao IAM utilizando:

```bash
aws iam list-users
```

O comando retorna os usuários IAM disponíveis na conta AWS em formato JSON.

O resultado confirmou que a AWS CLI estava configurada e conseguia realizar consultas ao serviço IAM.

![Consulta de usuários IAM](./users.png)

### 6. Consulta das Políticas IAM

Em seguida, foi realizada uma consulta às políticas gerenciadas pelo cliente utilizando:

```bash
aws iam list-policies --scope Local
```

O parâmetro `--scope Local` foi utilizado para filtrar as políticas gerenciadas pelo cliente.

No resultado, foi localizada a política `lab_policy`.

Entre as informações retornadas estavam:

* `PolicyName`
* `Arn`
* `DefaultVersionId`

A propriedade `DefaultVersionId` foi utilizada para identificar a versão da política recuperada na etapa seguinte.

![Consulta das políticas IAM](./policies.png)

### 7. Recuperação da Versão da `lab_policy`

Após identificar a política `lab_policy` e sua versão padrão, foi utilizado o comando `get-policy-version` para recuperar o documento da política em formato JSON.

O comando utilizado foi:

```bash
aws iam get-policy-version \
  --policy-arn arn:aws:iam::<AWS_ACCOUNT_ID>:policy/lab_policy \
  --version-id v1
```

A versão padrão identificada durante o laboratório foi `v1`.

O comando retornou as informações da versão da política, incluindo o documento JSON correspondente à `lab_policy`.

![Recuperação da versão da policy](./policy-version.png)

### 8. Salvamento da Policy em Formato JSON

O resultado do comando foi salvo em um arquivo utilizando o operador `>`:

```bash
aws iam get-policy-version \
  --policy-arn arn:aws:iam::<AWS_ACCOUNT_ID>:policy/lab_policy \
  --version-id v1 \
  > lab_policy.json
```

O operador `>` redireciona a saída do comando para o arquivo `lab_policy.json`.

O arquivo resultante pôde ser consultado com:

```bash
cat lab_policy.json
```

Dessa forma, a resposta obtida pela AWS CLI foi armazenada como um arquivo JSON dentro da instância EC2.

## Resultado

O laboratório foi concluído com a instalação e configuração da AWS CLI em uma instância EC2 e sua utilização para interagir com o AWS IAM.

Foram realizadas consultas de usuários e políticas, além da recuperação da versão da política `lab_policy` por meio da linha de comando e seu salvamento em um arquivo JSON.
