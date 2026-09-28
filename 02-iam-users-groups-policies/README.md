# Lab — IAM, Users, Groups, and Policies

[English](#english) · [Português](#português)

---

## English

## Objective

The objective of this lab was to explore AWS Identity and Access Management (IAM) by creating and configuring users, groups, password policies, and access permissions.

The lab also included permission testing with different IAM users to verify how policies control access to Amazon S3 and Amazon EC2 resources.

## Services and Resources Used

* **AWS Identity and Access Management (IAM)** — management of users, groups, password policies, and permissions
* **Amazon S3** — service used to test read-only access permissions
* **Amazon EC2** — service used to test read-only and administrative permissions

## Steps Performed

### 1. Password Policy Configuration

A custom password policy was created for the AWS account.

The following settings were applied:

| Setting | Value |
| --- | --- |
| Minimum password length | 10 characters |
| Uppercase letter | Required |
| Lowercase letter | Required |
| Number | Required |
| Special character | Required |
| Password expiration | 90 days |
| Password reuse prevention | Last 5 passwords |
| Administrator-required password reset | Disabled |

![Configured password policy](./password-policy.png)

The password policy establishes account-level requirements for IAM user passwords and helps enforce consistent authentication requirements.

### 2. IAM Users and Groups

The lab environment contains three IAM users and three IAM groups.

| User | Group | Role |
| --- | --- | --- |
| `user-1` | `S3-Support` | Amazon S3 support |
| `user-2` | `EC2-Support` | Amazon EC2 support |
| `user-3` | `EC2-Admin` | Amazon EC2 administration |

The groups were used to organize permissions according to each user's role.

This allows permissions to be managed at the group level instead of assigning the same permissions individually to each user.

![IAM groups](./iam-groups.png)

### 3. Policies and Permissions

The groups were configured with different policies according to the access required for each role.

#### S3-Support

The `S3-Support` group has the managed policy `AmazonS3ReadOnlyAccess`.

This policy allows users to view and list Amazon S3 resources without allowing modifications.

#### EC2-Support

The `EC2-Support` group has the managed policy `AmazonEC2ReadOnlyAccess`.

This policy allows users to view information about Amazon EC2 resources but does not allow them to modify those resources.

#### EC2-Admin

The `EC2-Admin` group has an inline policy named `EC2-Admin-Policy`.

This policy allows users to view information about EC2 instances and also start and stop instances.

### 4. Permission Testing

The configured permissions were tested using each IAM user.

#### user-1 — S3-Support

`user-1` was able to access Amazon S3 and view the available buckets and their contents.

However, the user was unable to access Amazon EC2 instances because the `S3-Support` group does not have permissions for that service.

This test demonstrated that the user's permissions were restricted to the resources covered by the assigned policy.

#### user-2 — EC2-Support

`user-2` was able to view Amazon EC2 instances.

When attempting to stop an instance, the operation was denied, demonstrating that the assigned policy provides read-only access.

The user was also unable to list Amazon S3 buckets.

This test demonstrated that read-only permissions allow users to retrieve resource information without authorizing modification actions.

#### user-3 — EC2-Admin

`user-3` was able to view Amazon EC2 instances and successfully stop an instance.

This test demonstrated the difference between read-only permissions and permissions that allow administrative actions on EC2 resources.

## Result

At the end of the lab, IAM users, groups, password policies, and access permissions were configured and tested.

The permission tests demonstrated how different IAM policies control which AWS resources users can access and which actions they are authorized to perform.

The lab provided practical experience with access control in AWS by comparing read-only permissions, service-specific access, and permissions that allow resource actions.

---

## Português

## Objetivo

Este laboratório teve como objetivo explorar o AWS Identity and Access Management (IAM) por meio da criação e configuração de usuários, grupos, política de senha e permissões de acesso.

O laboratório também incluiu testes de permissões com diferentes usuários IAM para verificar como as políticas controlam o acesso aos recursos do Amazon S3 e Amazon EC2.

## Serviços e Recursos Utilizados

* **AWS Identity and Access Management (IAM)** — gerenciamento de usuários, grupos, política de senha e permissões
* **Amazon S3** — serviço utilizado para testar permissões de acesso somente para leitura
* **Amazon EC2** — serviço utilizado para testar permissões de leitura e administrativas

## Etapas Realizadas

### 1. Configuração da Política de Senha

Foi criada uma política de senha personalizada para a conta AWS.

As seguintes configurações foram aplicadas:

| Configuração | Valor |
| --- | --- |
| Comprimento mínimo da senha | 10 caracteres |
| Letra maiúscula | Obrigatória |
| Letra minúscula | Obrigatória |
| Número | Obrigatório |
| Caractere especial | Obrigatório |
| Expiração da senha | 90 dias |
| Prevenção de reutilização | Últimas 5 senhas |
| Reset obrigatório pelo administrador | Desativado |

![Política de senha configurada](./password-policy.png)

A política de senha estabelece requisitos para as senhas dos usuários IAM e permite aplicar critérios de autenticação de forma consistente na conta.

### 2. Usuários e Grupos IAM

O ambiente do laboratório possui três usuários IAM e três grupos IAM.

| Usuário | Grupo | Função |
| --- | --- | --- |
| `user-1` | `S3-Support` | Suporte ao Amazon S3 |
| `user-2` | `EC2-Support` | Suporte ao Amazon EC2 |
| `user-3` | `EC2-Admin` | Administração do Amazon EC2 |

Os grupos foram utilizados para organizar as permissões de acordo com a função de cada usuário.

Isso permite que as permissões sejam gerenciadas no nível dos grupos, evitando a necessidade de atribuir individualmente as mesmas permissões a cada usuário.

![Grupos IAM](./iam-groups.png)

### 3. Políticas e Permissões

Os grupos foram configurados com diferentes políticas de acordo com as permissões necessárias para cada função.

#### S3-Support

O grupo `S3-Support` possui a política gerenciada `AmazonS3ReadOnlyAccess`.

Essa política permite visualizar e listar recursos do Amazon S3, sem permitir alterações.

#### EC2-Support

O grupo `EC2-Support` possui a política gerenciada `AmazonEC2ReadOnlyAccess`.

Essa política permite visualizar informações sobre recursos do Amazon EC2, mas não permite modificá-los.

#### EC2-Admin

O grupo `EC2-Admin` possui uma política inline chamada `EC2-Admin-Policy`.

Essa política permite visualizar informações sobre instâncias EC2 e também iniciar e parar instâncias.

### 4. Teste das Permissões

As permissões configuradas foram testadas utilizando cada usuário IAM.

#### user-1 — S3-Support

O `user-1` conseguiu acessar o Amazon S3 e visualizar os buckets disponíveis e seus conteúdos.

Por outro lado, o usuário não conseguiu acessar as instâncias do Amazon EC2, pois o grupo `S3-Support` não possui permissões para esse serviço.

Esse teste demonstrou que as permissões do usuário estavam restritas aos recursos abrangidos pela política atribuída.

#### user-2 — EC2-Support

O `user-2` conseguiu visualizar as instâncias do Amazon EC2.

Ao tentar parar uma instância, a operação foi negada, demonstrando que a política atribuída fornece acesso somente para leitura.

O usuário também não conseguiu listar os buckets do Amazon S3.

Esse teste demonstrou que permissões de somente leitura permitem consultar informações dos recursos sem autorizar ações de alteração.

#### user-3 — EC2-Admin

O `user-3` conseguiu visualizar as instâncias do Amazon EC2 e realizar com sucesso a operação de parar uma instância.

Esse teste demonstrou a diferença entre permissões somente para leitura e permissões que permitem realizar ações administrativas sobre recursos EC2.

## Resultado

Ao final do laboratório, foram configurados e testados usuários IAM, grupos, política de senha e permissões de acesso.

Os testes de permissões demonstraram como diferentes políticas do IAM controlam quais recursos da AWS os usuários podem acessar e quais ações estão autorizados a executar.

O laboratório proporcionou experiência prática com controle de acesso na AWS, comparando permissões somente para leitura, acesso específico a serviços e permissões que permitem realizar ações sobre recursos.
