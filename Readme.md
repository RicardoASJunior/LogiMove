# Documentação do Projeto de Banco de Dados para LogiMove Transportes

## Aluno Estácio
Nome: Ricardo Alves dos Santos Junior

Matrícula: 202208681158

E-mail: 202208681158@alunos.estacio.br

## Visão Geral
O objetivo deste projeto é desenvolver um banco de dados no Azure SQL para a LogiMove Transportes, uma empresa de logística que está migrando de um sistema baseado em papel para uma solução digital. Este novo sistema visa melhorar a coordenação e rastreamento de remessas através de autenticação digital. O banco de dados armazenará informações essenciais sobre motoristas, clientes e pedidos, facilitando o gerenciamento e a eficiência operacional da empresa.

## Configuração do Ambiente Azure

### Criar uma Conta no Azure
1. Acesse o site do Azure e, se ainda não tiver uma conta, crie uma nova.

### Configurar uma Instância do Azure SQL Database
1. No portal do Azure, selecione "Criar um recurso" e procure por "SQL Database".
2. Configure a instância, fornecendo os detalhes necessários como nome do servidor, nome do banco de dados, tipo de plano, entre outros.

### Estabelecer Parâmetros de Segurança
1. Configure as regras de firewall para garantir o acesso seguro ao banco de dados.
2. Defina regras de acesso para controlar quem pode acessar e modificar o banco de dados.

## Design do Banco de Dados

### Definir a Arquitetura do Banco de Dados
1. Planeje a estrutura do banco de dados levando em conta as necessidades específicas da LogiMove Transportes.

### Criar um Diagrama de Entidade-Relacionamento (ER)
1. Utilize ferramentas como Draw.io ou Lucidchart para visualizar as relações entre as tabelas e facilitar o entendimento da estrutura.

## Implementação do Banco de Dados

### Criar Tabelas com T-SQL

#### Tabela de Motoristas (Drivers):
```sql
IF OBJECT_ID('Drivers', 'U') IS NOT NULL
    DROP TABLE Drivers;

CREATE TABLE Drivers (
    DriverID INT IDENTITY(1,1) PRIMARY KEY,
    Nome NVARCHAR(100) NOT NULL,
    CNH NVARCHAR(20) NOT NULL,
    Endereço NVARCHAR(200),
    Contato NVARCHAR(50)
);
```

#### Tabela de Clientes (Clients):
```sql
IF OBJECT_ID('Clients', 'U') IS NOT NULL
    DROP TABLE Clients;

CREATE TABLE Clients (
    ClientID INT IDENTITY(1,1) PRIMARY KEY,
    Nome NVARCHAR(100) NOT NULL,
    Empresa NVARCHAR(100),
    Endereço NVARCHAR(200),
    Contato NVARCHAR(50)
);

```

#### Tabela de Pedidos (Orders):
```sql
IF OBJECT_ID('Orders', 'U') IS NOT NULL
    DROP TABLE Orders;

CREATE TABLE Orders (
    OrderID INT IDENTITY(1,1) PRIMARY KEY,
    ClientID INT NOT NULL,
    DriverID INT NOT NULL,
    DetalhesPedido NVARCHAR(500),
    DataEntrega DATE,
    Status NVARCHAR(20),
    FOREIGN KEY (ClientID) REFERENCES Clients(ClientID),
    FOREIGN KEY (DriverID) REFERENCES Drivers(DriverID)
);

```

### Inserção de Dados Fictícios

#### Tabela Drivers:
```sql
INSERT INTO Drivers (Nome, CNH, Endereço, Contato)
VALUES 
('João Silva', 'AB123456', 'Rua das Flores, 123', '(11) 91234-5678'),
('Maria Santos', 'CD789012', 'Av. Paulista, 1000', '(11) 92345-6789'),
('Carlos Oliveira', 'EF345678', 'Rua do Carmo, 50', '(11) 93456-7890');

```

#### Tabela Clients:
```sql
INSERT INTO Clients (Nome, Empresa, Endereço, Contato)
VALUES 
('Empresa ABC', 'ABC Ltda', 'Rua Alfa, 300', '(11) 94567-8901'),
('Empresa XYZ', 'XYZ S/A', 'Av. Beta, 400', '(11) 95678-9012'),
('Empresa LMN', 'LMN Corp', 'Rua Gama, 500', '(11) 96789-0123');

```

#### Tabela Orders:
```sql
INSERT INTO Orders (ClientID, DriverID, DetalhesPedido, DataEntrega, Status)
VALUES 
(1, 1, 'Entrega de materiais de construção', '2024-06-15', 'Em andamento'),
(2, 2, 'Entrega de equipamentos de escritório', '2024-06-16', 'Pendente'),
(3, 3, 'Entrega de produtos eletrônicos', '2024-06-17', 'Concluído');

```
## Validação da Estrutura
1. Verifique se todas as tabelas foram criadas corretamente.
2. Insira dados de teste para validar as funcionalidades e assegurar que tudo está funcionando conforme esperado.

## Configuração de Backups e Monitoramento

### Configure Políticas de Backup
1. Garanta que políticas de backup estejam configuradas para evitar a perda de dados em casos de falhas ou desastres.

### Implemente Monitoramento
1. Utilize ferramentas de monitoramento para acompanhar a performance e segurança do banco de dados, garantindo um funcionamento otimizado e seguro.

## Considerações Finais
Este guia fornece uma estrutura completa para configurar e utilizar um banco de dados no Azure SQL para a LogiMove Transportes, facilitando a transição para um sistema digital eficiente e melhorando significativamente o gerenciamento das operações da empresa.

