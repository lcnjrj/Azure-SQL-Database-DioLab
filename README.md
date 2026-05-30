# Azure SQL Database: Guia Prático de Arquitetura, Configuração e Conectividade via Linux

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.org/)
[![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)](https://www.microsoft.com/sql-server)

Este repositório foi desenvolvido como parte de um laboratório prático com o objetivo de explorar, configurar e documentar uma instância de banco de dados relacional na plataforma **Microsoft Azure**. O conteúdo aqui presente serve como apoio para estudos de administração de infraestrutura em nuvem.

---

## Objetivos de Aprendizagem

- [x] Entender a arquitetura e posicionamento da família de produtos Azure SQL.
- [x] Aplicar conceitos de computação em nuvem (PaaS e Serverless) em um ambiente prático.
- [x] Configurar regras rígidas de segurança, redes e firewalls no ecossistema Azure.
- [x] Estabelecer conexões seguras e estáveis utilizando o terminal corporativo Linux.
- [x] Praticar a engenharia de documentação técnica clara, estruturada e autoexplicativa.

---

## 📂 Estrutura Estrutural do Repositório

```text
├── images/               # Capturas de tela das etapas de configuração no portal Azure
├── README.md             # Documentação principal e guia de estudos do laboratório

```
## Arquitetura e Configuração do Azure SQL
O ambiente de dados moderno exige flexibilidade, resiliência e segurança. Abaixo estão documentados os fundamentos teóricos e o passo a passo operacional para provisionamento e consumo do Azure SQL Database.

## 1. O que é o Azure SQL e sua Finalidade
O Azure SQL é uma família de produtos de banco de dados relacionais em nuvem baseados no mecanismo de alta performance do Microsoft SQL Server. Classificado estritamente na categoria de PaaS (Plataforma como Serviço), ele foi desenhado para eliminar a complexidade da gestão de infraestrutura física e de sistemas operacionais.

Sua principal finalidade é permitir que Engenheiros de Software, Administradores de Banco de Dados (DBAs) e Profissionais de Infraestrutura foquem exclusivamente no valor de negócio: modelagem de dados, otimização de queries, indexação e lógica de negócios, delegando rotinas complexas de hardware, patch e rede à Microsoft.

## 2. Vantagens Estruturais do Modelo PaaS
*Gerenciamento Automatizado:* Rotinas críticas como backups (com retenção customizável), atualizações do engine do SQL Server e aplicação de patches de segurança ocorrem de forma transparente e sem downtime.

*Escalabilidade Elástica:* Capacidade de escalar recursos de computação (vCores) e armazenamento sob demanda para suportar picos de carga de trabalho, retornando ao estado inicial sem interrupção dos serviços.

*Camada Serverless:* Abordagem altamente eficiente em custos onde os recursos computacionais são faturados estritamente por segundo de uso ativo. Inclui o recurso de Pausa Automática, que suspende o banco de dados durante períodos de inatividade definidos pelo administrador.

*Segurança Avançada e Integrada:* Proteção em multicamadas que inclui criptografia nativa em repouso e em trânsito (TDE), mascaramento dinâmico de dados confidenciais (Dynamic Data Masking), isolamento de rede e detecção pró-ativa de ameaças ou acessos anômalos baseada em Inteligência Artificial.

## Passo a Passo para Configuração no Portal Azure
Etapa 1: Provisionamento do Recurso
No menu lateral ou na barra de pesquisas do Portal do Azure, busque por Azure SQL.

Clique em Criar e selecione a opção SQL Databases. Em tipo de recurso, opte por Single Database (Banco de dados único).

Etapa 2: Definição de Escopo e Infraestrutura básica
Grupo de Recursos (Resource Group): Crie ou selecione um grupo dedicado para este laboratório (ex: rg-diolab-sql), facilitando a governança e futura exclusão de recursos vinculados.

Detalhes do Banco de Dados: Crie o nome do banco de dados de sua preferência.

Servidor Lógico (Server): Caso não possua, clique em Criar novo. Defina um nome globalmente único (ex: diolab-sql-servidor) e selecione a região geográfica ideal (ex: Brazil South foi oquefuncionoupelo sistema grátis).

## Etapa 3: Arquitetura de Computação e Armazenamento (Foco em Custo-Benefício)
Clique em Configurar banco de dados (Configure database).

Mude a camada de serviço padrão para General Purpose (Propósito Geral).

No tipo de computação, altere para Serverless.

Configure os limites máximo e mínimo de vCores conforme seu cenário de testes.

Essencial: Ative a caixa de Pausa Automática (Auto-pause delay) e configure o tempo de espera (ex: 1 mês, para ficar de acordo com a promoção) para evitar cobranças indesejadas enquanto o banco estiver ocioso.

print

## Etapa 4: Configuração da Identidade e Autenticação Nativa para Linux
Ambientes Linux corporativos exigem conexões diretas e eficientes via ferramentas de linha de comando. A autenticação mista garante estabilidade máxima para este cenário.

No menu de criação ou acessando a página do Servidor Lógico criado, localize o menu lateral Segurança > Autenticação (ou Microsoft Entra ID).

Modifique a configuração de autenticação para: "Suporte para autenticação do SQL e do Microsoft Entra" (Use both SQL and Microsoft Entra authentication).

Defina as credenciais do administrador nativo do banco de dados:

Login de administrador: admin_linux (ou o usuário de sua preferência)

Senha: Defina uma senha forte e segura.

Clique em Salvar no topo da página.
