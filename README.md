# 🚀 Automação de Infraestrutura Global com AWS CloudFormation

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white)
![IaC](https://img.shields.io/badge/IaC-Infra_as_Code-blue?style=for-the-badge)

Este repositório foi desenvolvido para o segundo desafio de **AWS CloudFormation** da **Digital Innovation One (DIO)**. O objetivo aqui é elevar o nível da automação, demonstrando como criar uma infraestrutura de rede isolada e segura utilizando o conceito de **Infraestrutura como Código (IaC)**.

---

## 📐 Arquitetura do Template (VPC + Subnet + EC2)
Diferente de um provisionamento simples, este template automatiza a criação de um ecossistema completo:
1. **AWS::EC2::VPC:** Cria uma rede virtual privada e isolada na nuvem.
2. **AWS::EC2::Subnet:** Define uma sub-rede interna dentro da nossa VPC para hospedar os recursos.
3. **AWS::EC2::Instance:** Cria o servidor virtual (EC2) já configurado e embutido dentro da rede que acabamos de criar.

---

## 📄 Código do Template de Automação Avançada (YAML)

Abaixo está o arquivo de configuração declarativo que desenha a nossa rede e o nosso servidor de forma automatizada:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'Template de Automacao de Infraestrutura de Rede e Servidores - Lab DIO'

Resources:
  # 1. Criando a Rede Isolada (VPC)
  MinhaVPCPro:
    Type: 'AWS::EC2::VPC'
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: VPC-Laboratorio-DIO

  # 2. Criando a Sub-rede dentro da VPC
  MinhaSubnetPro:
    Type: 'AWS::EC2::Subnet'
    Properties:
      VpcId: !Ref MinhaVPCPro
      CidrBlock: 10.0.1.0/24
      AvailabilityZone: us-east-1a
      Tags:
        - Key: Name
          Value: Subnet-Laboratorio-DIO

  # 3. Criando o Servidor dentro da Sub-rede criada acima
  ServidorProducao:
    Type: 'AWS::EC2::Instance'
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c55b159cbfafe1f0
      SubnetId: !Ref MinhaSubnetPro
      Tags:
        - Key: Name
          Value: Servidor-Automação-Avancada