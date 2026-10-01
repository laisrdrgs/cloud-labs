# Lab — IAM, Users, Groups, and Policies

[English](#english) · [Português](#português)

---

## English

## Objective

The objective of this lab was to practice AWS Identity and Access Management (IAM) by creating and configuring users, groups, password policies, and permissions.

Permission tests were also performed using different IAM users to verify access to Amazon S3 and Amazon EC2 resources.

## Services and Resources Used

* **AWS Identity and Access Management (IAM)** — used to manage users, groups, password policies, and permissions
* **Amazon S3** — used to test read-only access
* **Amazon EC2** — used to test read-only and administrative permissions

## Steps Performed

### 1. Password Policy Configuration

A custom password policy was configured for the AWS account.

| Setting                               | Value            |
| ------------------------------------- | ---------------- |
| Minimum password length               | 10 characters    |
| Uppercase letter                      | Required         |
| Lowercase letter                      | Required         |
| Number                                | Required         |
| Special character                     | Required         |
| Password expiration                   | 90 days          |
| Password reuse prevention             | Last 5 passwords |
| Administrator-required password reset | Disabled         |

![Configured password policy](./password-policy.png)

### 2. IAM Users and Groups

Three IAM users and three IAM groups were configured.

| User     | Group         | Role                      |
| -------- | ------------- | ------------------------- |
| `user-1` | `S3-Support`  | Amazon S3 support         |
| `user-2` | `EC2-Support` | Amazon EC2 support        |
| `user-3` | `EC2-Admin`   | Amazon EC2 administration |

The users were assigned to groups according to the access required for each role.

![IAM groups](./iam-groups.png)

### 3. Policies and Permissions

Different policies were configured for each group.

#### S3-Support

The `S3-Support` group was assigned the managed policy `AmazonS3ReadOnlyAccess`.

This allowed `user-1` to view and list Amazon S3 resources without allowing modifications.

#### EC2-Support

The `EC2-Support` group was assigned the managed policy `AmazonEC2ReadOnlyAccess`.

This allowed `user-2` to view Amazon EC2 resources without allowing modifications.

#### EC2-Admin

The `EC2-Admin` group was configured with an inline policy named `EC2-Admin-Policy`.

The policy allowed `user-3` to view EC2 instances and perform start and stop actions.

### 4. Permission Testing

The configured permissions were tested with each IAM user.

#### user-1 — S3-Support

`user-1` was able to access Amazon S3 and view the available buckets and their contents.

The user was unable to access Amazon EC2 resources because the assigned group did not provide EC2 permissions.

#### user-2 — EC2-Support

`user-2` was able to view Amazon EC2 instances.

When attempting to stop an instance, the operation was denied because the assigned policy provides read-only access.

The user was also unable to list Amazon S3 buckets.

#### user-3 — EC2-Admin

`user-3` was able to view Amazon EC2 instances and successfully stop an instance.

This test confirmed that the configured permissions allowed actions beyond read-only access for EC2 resources.

## Result

The lab was completed by configuring IAM users, groups, a password policy, and different access permissions.

Permission tests were performed with all three users, demonstrating the differences between S3 read-only access, EC2 read-only access, and EC2 permissions that allow resource actions.

---

## Português

## Objetivo

O objetivo deste laboratório foi praticar o AWS Identity and Access Management (IAM) por meio da criação e configuração de usuários, grupos, política de senha e permissões.

Também foram realizados testes de permissões utilizando diferentes usuários IAM para verificar o acesso aos recursos do Amazon S3 e Amazon EC2.

## Serviços e Recursos Utilizados

* **AWS Identity and Access Management (IAM)** — utilizado para gerenciar usuários, grupos, política de senha e permissões
* **Amazon S3** — utilizado para testar acesso somente para leitura
* **Amazon EC2** — utilizado para testar permissões de leitura e permissões para realizar ações

## Etapas Realizadas

### 1. Configuração da Política de Senha

Foi configurada uma política de senha personalizada para a conta AWS.

| Configuração                         | Valor            |
| ------------------------------------ | ---------------- |
| Comprimento mínimo da senha          | 10 caracteres    |
| Letra maiúscula                      | Obrigatória      |
| Letra minúscula                      | Obrigatória      |
| Número                               | Obrigatório      |
| Caractere especial                   | Obrigatório      |
| Expiração da senha                   | 90 dias          |
| Prevenção de reutilização            | Últimas 5 senhas |
| Reset obrigatório pelo administrador | Desativado       |

![Política de senha configurada](./password-policy.png)

### 2. Usuários e Grupos IAM

Foram configurados três usuários IAM e três grupos IAM.

| Usuário  | Grupo         | Função                      |
| -------- | ------------- | --------------------------- |
| `user-1` | `S3-Support`  | Suporte ao Amazon S3        |
| `user-2` | `EC2-Support` | Suporte ao Amazon EC2       |
| `user-3` | `EC2-Admin`   | Administração do Amazon EC2 |

Os usuários foram associados aos grupos de acordo com as permissões necessárias para cada função.

![Grupos IAM](./iam-groups.png)

### 3. Políticas e Permissões

Foram configuradas diferentes políticas para cada grupo.

#### S3-Support

O grupo `S3-Support` recebeu a política gerenciada `AmazonS3ReadOnlyAccess`.

Essa política permitiu que o `user-1` visualizasse e listasse recursos do Amazon S3 sem permitir alterações.

#### EC2-Support

O grupo `EC2-Support` recebeu a política gerenciada `AmazonEC2ReadOnlyAccess`.

Essa política permitiu que o `user-2` visualizasse recursos do Amazon EC2 sem permitir alterações.

#### EC2-Admin

O grupo `EC2-Admin` foi configurado com uma política inline chamada `EC2-Admin-Policy`.

A política permitiu que o `user-3` visualizasse instâncias EC2 e realizasse ações de iniciar e parar instâncias.

### 4. Teste das Permissões

As permissões configuradas foram testadas utilizando cada usuário IAM.

#### user-1 — S3-Support

O `user-1` conseguiu acessar o Amazon S3 e visualizar os buckets disponíveis e seus conteúdos.

O usuário não conseguiu acessar os recursos do Amazon EC2 porque o grupo atribuído não possuía permissões para EC2.

#### user-2 — EC2-Support

O `user-2` conseguiu visualizar as instâncias do Amazon EC2.

Ao tentar parar uma instância, a operação foi negada porque a política atribuída fornece acesso somente para leitura.

O usuário também não conseguiu listar os buckets do Amazon S3.

#### user-3 — EC2-Admin

O `user-3` conseguiu visualizar as instâncias do Amazon EC2 e parar uma instância com sucesso.

Esse teste confirmou que as permissões configuradas permitiam realizar ações além do acesso somente para leitura nos recursos EC2.

## Resultado

O laboratório foi concluído com a configuração de usuários IAM, grupos, uma política de senha e diferentes permissões de acesso.

Foram realizados testes de permissões com os três usuários, demonstrando as diferenças entre acesso somente para leitura ao S3, acesso somente para leitura ao EC2 e permissões para realizar ações sobre recursos EC2.
