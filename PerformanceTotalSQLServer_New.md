# Udemy - Performance Total no SQL Server

### **Instrutor**: Vínicius Nogueira
### **Linkedin**: [Perfil do LinkeIn](https://www.linkedin.com/in/viniciusnogueira/)
### **Página do curso na Udemy**: [Link para página do curso](https://www.udemy.com/course/performance-total-no-sql-server/learn/lecture/26043050?start=0#overview)
### **Pasta Google Drive Treinamento**: [Link para pasta do curso](https://drive.google.com/drive/folders/1DzaUlE7JZ8Sjoir8pWCLPQak6zVjqMDm?usp=drive_link)
### **Início**: 03/09/2024
### **Término**: 

## A Jornada

Me considerando um Administrador de Banco de Dados com muitos anos de experiência em Gestão e Administração de ambientes SQL Server, tenho uma grande deficiência quando o assunto é Performance e Tuning e para mudar o jogo, estou iniciando uma longa jornada com intuito de sanar esta deficiência e deixarei aqui meus registros desta caminhada.

## Índice
- [Seção 1: Visão Geral do Curso Performance Total no SQL Server](#seção-1-visão-geral-do-curso-performance-total-no-sql-server)
- [Seção 2: Preparação do Ambiente](#seção-2-preparação-do-ambiente)
- [Seção 3: Onde o Seviço do Banco de Dados está Instalado](#seção-3-onde-o-serviço-do-banco-de-dados-está-instalado)
- [Seção 4: Como o Serviço do Banco de Dados está Instalado](#seção-4-como-o-serviço-do-banco-de-dados-está-instalado)
- [Seção 5: Como o Serviço do Banco de Dados é Acessado pelos Usuários e Aplicações](#seção-5-como-o-serviço-do-banco-de-dados-é-acessado-pelos-usuários-e-aplicações)
- [Lições Aprendidas](#lições-aprendidas)

---

## Dia 1

---

## Seção 1: Visão Geral do Curso Performance Total no SQL Server

### Visão Geral do Curso

#### Introdução

- Tarefas devem ser executadas dentro de um tempo aceitável.
- Em empresas menores, a performance normalmente é colocada de lado, e problemas são observados geralmente quando o sistema já está em produção.
- É feito um bom trabalho de análise de requisitos, desenvolvimento e testes, porém sem levar em conta cenários realistas.
- A solução de problemas de performance normalmente ocorre quando o sistema já está em uso, gerando muitas vezes indisponibilidade.
- Normalmente, esses problemas são decorrentes de questões de design e estrutura.

#### SQL Server - Performance

No ciclo comum de desenvolvimento de uma aplicação, a performance normalmente é observada na fase de Processamento, onde são feitos testes, QA estressa a aplicação e, com base nos resultados, são feitas avaliações de performance. No entanto, isso deveria ser visto ainda na fase de Recursos.

![Ciclo de Análise de Performance](images/ciclo_analise_performance.png)

Não basta aumentarmos os recursos de máquina e acharmos que isso irá resolver os problemas de performance; precisamos identificar os gargalos do nosso sistema.

O que costuma acontecer:

- Problemas de performance e procrastinação andam de mãos dadas.
- Ocorrem de forma lenta e gradativa, aumentando o nível de insatisfação dos usuários e diminuindo a produtividade.

Problemas de performance são os mais comuns e duradouros em sistemas de qualquer empresa, pois, na maioria dos casos, eles não impedem a utilização total do sistema, fazendo com que as pessoas demorem mais para reagir a esse problema.

Iniciaremos nossa jornada respondendo a estas questões:

1. **Onde** o servidor de banco de dados está instalado?
2. **Como** o servidor de banco de dados está instalado?
3. **Como** o servidor de banco de dados é acessado pelos usuários/aplicações?
4. **Como** o servidor de banco de dados é monitorado e mantido?

Passaremos pelos seguintes níveis de análise:

- Otimização em nível de hardware (servidor)
- Otimização em nível de hypervisor
- Otimização em nível de VM host (OS)
- Otimização em nível de SGBD
- Otimização em nível de banco de dados e aplicações
- Monitoramento e diagnóstico de performance

![Níveis de Monitoramento](images/niveis_monitoramento.png)

## Seção 2: Preparação do Ambiente

### Como será nosso Laboratório de Treinamento

#### Para nosso Laboratório faremos uso de VMs e para tanto podemos escolher entre as seguintes opções:

1. vmware - [Link para página de Download do vmware](https://access.broadcom.com/default/ui/v1/signin/)
2. VirtualBox - [Link para página de Download do VirtualBox](https://www.virtualbox.org/wiki/Downloads)
3. Vagrant - [Link para página de Download do Vagrant](https://developer.hashicorp.com/vagrant/install)

#### Para o servidor onde o SQL Server irá rodar utilizaremos a seguinte opção:

1. Windows Server 2019 Evaluation Edition [Link para página de Download do Windows Server 2019](https://info.microsoft.com/ww-landing-windows-server-2019.html?lcid=pt-BR)

#### Para o ambiente do SQL Server precisaremos dos seguintes itens:

1. SQL Server 2019 Developer Edition [Link para página de Download do SQL Server 2019](https://info.microsoft.com/ww-landing-sql-server-2019.html?lcid=pt-BR)
2. SQL Server Management Studio (SSMS) [Link para página de Download do SQL Server Management Studio](https://learn.microsoft.com/pt-br/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15)
3. Banco de Dados de Exemplo (AdventureWorks sample database) [Link para página de Download do Banco de Dados de Exemplo](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) **Obs.**: _Escolha por WideWorldImporters-Full.bak_

### Montagem do Laboratório de Treinamento

#### Configurando a máquina Virtual

Optamos por usar o **VirtualBox** e vamos criar uma VM com as seguintes características:

- **Nome**: SQL-WIN-01
- **Local do arquivo**: C:\Users\UserName\VirtualBox VMs
- **Tipo**: Microsoft Windows
- **Versão**: Windows 2019 (64-bit)
- **Hardware**:
  - **Memória Base**: 3.0 GB
  - **HD**: 30 GB

Após criar a VM, iremos fazer a instalação do Sistema Operacional escolhido (Windows Server 2019 Evaluation Edition), com as seguintes características:

- **Language to install**: English (United States)
- **Time and currency format**: English (United States)
- **Keyboard or input method**: US
- **Operating system**: Windows Server 2019 Standard Evaluation (Desktop Experience)
- **Which type of installation do you want**: Custom: Install Windows only (advanced)
- **Customize settings**:
  - **User name**: Administrator
  - **Password**: Minh@Senh@123