# Udemy - Performance Total no SQL Server

### **Instrutor**: Vínicius Nogueira
### **Linkedin**: [Link para página Perfil](https://www.linkedin.com/in/viniciusnogueira/)
### **Página curso na Udemy**: [Link para página do curso](https://www.udemy.com/course/performance-total-no-sql-server/learn/lecture/26043050?start=0#overview)
### Pasta Google Drive Treinamento: [Link para pasta do curso](https://drive.google.com/drive/folders/1DzaUlE7JZ8Sjoir8pWCLPQak6zVjqMDm?usp=drive_link)
### **Início**: 03/09/2024
### **Término**: 


---

## Introdução

- Tarefas devem ser executadas dentro de um tempo aceitável
- Empresas menores, performance normalmente é colocada de lado, problemas são observados em geral quando já está em produção
- É feito um bom trabalho de análise de requisitos, desenvolvimento, feito testes, porém sem levar em conta cenários realistas
- Solução de problemas de performance normalmente ocorre quando o sistema já está em uso, gerando muitas vezes indisponibilidade
- Normalmente estes problemas são decorrentes de questões de design, estrutura

### SQL Server: Performance

No ciclo comum de desenvolvimento de uma aplicação a Performante normalmente é observada na fase de Processamento, onde são feitos testes, QA estressa a aplicação e com base nos resultados são feitas avaliações de Performance, mas isto deveria ser visto ainda na fase de Recursos.

![img-CicloAnalisePerformance.png](./Imagens/CicloAnalisePerformance.png)

Não basta aumentarmos os Recursos de máquina e acharmos que isto irá resolver os problemas de performance, precisamos sim, identificar os gargalos de nosso sistema.

O que costuma acontecer:

- Problemas de Performance e Procrastinação andam de mãos dadas
- Ocorrem de forma lenta e gradativa, aumentando o nível de insatisfação dos usuários e diminuindo a produtividade

Problemas de Performance são os mais comuns e duradouros em sistemas de qualquer empresa, pois na maioria dos casos ele não impede a utilização total do sistema, fazendo com que as pessoas demorem mais para reagir a este problema.

Iniciaremos nossa jornada respondendo a estas questões:

1. _**Onde**_ o Servidor de Banco de Dados está instalado
1. _**Como**_ o Servidor de Banco de Dados está instalado
1. _**Como**_ o Servidor de Banco de Dados é acessado pelos usuários/aplicações
1. _**Como**_ o Servidor de Banco de Dados é Monitorado e Mantido

Passaremos pelos seguintes níveis de análise:

- Otimização em nível de Hardware (Servidor)
- Otimização em nível de Hypervisor
- Otimização em nível de VM Host (OS)
- Otimização em nível de SGBD
- Otimização em nível BD e Aplicações
- Monitoramento e Diagnóstico de Performance

![img-NiveisMonitoramento.png](./Imagens/NiveisMonitoramento.png)

---

## Preparação do Laboratório do Treinamento

Para nosso Laboratório faremos uso de máquina Virtual e para tanto podemos escolher entre as seguintes opções:

1. vmware
    - [Link para página de Download](https://access.broadcom.com/default/ui/v1/signin/)
1. VirtualBox
    - [Link para página de Download](https://www.virtualbox.org/wiki/Downloads)
1. Vagrant
    - [Link para página de Download](https://developer.hashicorp.com/vagrant/install)

Para o servidor onde o SQL Server irá rodar, utilizaremos o Windows Server 2019 Evaluation Edition (ISO)

- [Link para página de Download](https://info.microsoft.com/ww-landing-windows-server-2019.html?lcid=pt-BR)

Para o servidor SQL Server, utilizaremos:

- SQL Server 2019 Developer Edition
    - [Link para página de Download](https://info.microsoft.com/ww-landing-sql-server-2019.html?lcid=pt-BR)
- SQL Server Management Studio (SSMS)
    - [Link para página de Download](https://learn.microsoft.com/pt-br/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15)
- Banco de Dados de Exemplo (AdventureWorks sample database)
    - [Link para página de Downloads](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0)
        - _Escolha por WideWorldImporters-Full.bak_

Configurando a máquina Virtual

Criar a máquina Virtual com as seguintes características:

    - Nome: SQL-WIN-01
    - Local do arquivo: C:\Users\carlo\VirtualBox VMs
    - Tipo: Microsoft Windows
    - Versão: Windows 2019 (64-bit)
    - Hardware:
        - Memória Base = 3.0 GB
        - HD = 30 GB

Instalar Windows Server com as seguintes características:

    - Language to install: English (United States)
    - Time and currency format: English (United States)
    - Keyboard or input method: US
    - Operating system: Windows Server 2019 Standard Evaluation (Desktop Experience)
    - Which type of installation do you want: Custom: Install Windows only (advanced)
    - Customize settings:
        - User name: Administrator
        - Password: Minh@Senh@123

Pós instalação Windows Server:

    - Adicionar VBoxWindowsGuestAdditions
    - Ajustar Configurações de Pastas Compartilhadas
    - Executar Windows Update
    - Ajustar configurações Regionais (Data & Hora)
    - Ajustar Configurações de Rede
        - VirtualBox Rede: Placa de Rede em modo Bridge
        - Windows Server TCP/IPv4:
            - IP address: 192.168.0.133
            - Subnet mask: 255.255.255.0
            - Default gateway: 192.168.0.1
            - Preferred DNS server: 192.168.0.1
            - Alternate DNS server: 8.8.8.8

**Dores**: _Embora no Laboratório proposto não fosse pedido para fixar o IP da VM, achei que seria razoável faze-lo, entretanto isso me custou algumas horas de trabalho para realizar sua configuração, tudo porque não me atentei que o IP que havia definido já estava em uso, ainda que no teste previo de ping ele não estivesse respondendo. Fica a recomendação para fazer um planejamento e esboço prévio, para evitar este tipo de situação._

Instalar SQL Server com as seguintes características:

- Specify SQL Server media download target location
    - Media Location = C:\Softwares_Arquivos\SQL2019
    - Specify the edition of SQL Server 2019 to install = Developer
    - Features Selection:
        - Database Engine Services
        - SQL Server Replication
        - Integration Services
        - Client Tools Connectivity
        - Client Tools SDK
    - Features Rules:
        - Instance root directory = C:\Program Files\Microsoft SQL Server\
        - Shared feature directory = C:\Program Files\Microsoft SQL Server\
        - Shared feature directory (x86) = C:\Program Files (x86)\Microsoft SQL Server\
    - Instance Configuration:
        - Named instance = SQL2019DEMO
        - Instance ID = SQL2019DEMO
    - Server Configuration:
        - Service Accounts = Ficou com as opções Default
        - Collation = Ficou com as opções Default
    - Database Engine Configuration:
        - Server Configuration
            - Authentication Mode = Mixed Mode (SQL Server authentication and Windows authentication)
            - Add Current User = SQL-WIN-01\Administrator
        - Data Directories
            - Ficou com as opções Default
        - TempDB
            - Ficou com as opções Default
        - MaxDOP
            - Ficou com as opções Default
        - Memory
            - Ficou com as opções Default
        - FILESTREAM
            - Ficou com as opções Default