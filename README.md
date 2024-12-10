# Provisionando uma EC2 Instance com Terraform

## O que é Terraform e para que serve?

Terraform é uma ferramenta de **Infraestrutura como Código (IaC)** desenvolvida pela HashiCorp. Ela permite gerenciar e provisionar infraestrutura de forma automatizada, declarativa e consistente. Com suporte a múltiplos provedores de nuvem, como AWS, Azure e Google Cloud, o Terraform facilita:

- **Automação**: Reduzindo esforços manuais.
- **Escalabilidade**: Permitindo gerenciar infraestrutura em larga escala.
- **Versionamento**: Registrando mudanças na configuração da infraestrutura.

---

## Requisitos

Antes de começar, certifique-se de ter:
1. **Terraform CLI** instalado (versão 1.2.0 ou superior).
2. **AWS CLI** configurado com um perfil ou variáveis de ambiente com credenciais válidas.
3. Uma conta na AWS com permissões para criar recursos (instâncias EC2).

---

## Passo a Passo

### 1. Configuração do Ambiente

1. **Configure as variáveis de ambiente para autenticação (opcional)**:
   ```bash
   export AWS_ACCESS_KEY_ID=SEU_ACCESS_KEY
   export AWS_SECRET_ACCESS_KEY=SEU_SECRET_KEY
   ```

---

### 2. Estrutura do Código
O código principal está no arquivo `src/main.tf`. A configuração define um provedor AWS e cria uma instância EC2.

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }
  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}
```

---

### 3. Inicializando o Projeto
1. Execute o comando para inicializar o Terraform e baixar os provedores necessários:
   ```bash
   terraform init
   ```

2. Valide a configuração para garantir que não haja erros:
   ```bash
   terraform validate
   ```

3. Formate o arquivo para garantir consistência:
   ```bash
   terraform fmt
   ```

---

### 4. Aplicando a Configuração
1. **Gerar o plano de execução**:
   ```bash
   terraform plan
   ```
   Este comando exibirá os recursos que serão criados na AWS.

2. **Aplicar a configuração**:
   ```bash
   terraform apply
   ```
   Confirme a execução digitando `yes` quando solicitado.

3. Após a execução, os recursos definidos serão provisionados na AWS.

---

## Recursos Provisionados

Os recursos provisionados incluem:

- **Instância EC2**:
  - **AMI**: ami-830c94e3
  - **Tipo**: t2.micro
  - **Tag**: `Name: EC2Pondeada`

---

## Conclusão

Terraform é uma ferramenta essencial para a automação e gerenciamento de infraestrutura em nuvem. Neste projeto, aprendemos como configurar e provisionar uma instância EC2 na AWS usando uma abordagem declarativa e padronizada. 
