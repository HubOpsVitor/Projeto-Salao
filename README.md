# Projeto Banco Salão
@author: Allan Vítor

## Instalação do MySQL no Docker (Fedora)

Primeiro, no Fedora, instale o MySQL no Docker com o seguinte comando:

```bash
docker pull mysql
```

Após isso, execute o comando para iniciar o container com o MySQL:

```bash
docker run --name bancosalao -e MYSQL_ROOT_PASSWORD=123bancosalao -p 3280:3306 -v ~/dados-salao:/var/lib/mysql -d mysql:latest
```

## Conexão no MySQL Workbench
Agora, abra o MySQL Workbench e conecte-se ao seu banco de dados. Acesse o MySQL utilizando a porta 3280 e a senha root 123bancosalao.

## Criação do Banco de Dados e Tabelas
Execute os seguintes comandos SQL para criar o banco de dados e as tabelas necessárias:

````
CREATE DATABASE SalaoCabeleireiro;
USE SalaoCabeleireiro;

-- Criar tabela de Clientes
CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20) NOT NULL,
    email VARCHAR(100) UNIQUE,
    data_cadastro DATE
);

-- Criar tabela de Funcionários
CREATE TABLE funcionarios (
    id_funcionario INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    cargo VARCHAR(50) NOT NULL,
    telefone VARCHAR(20),
    email VARCHAR(100) UNIQUE,
    data_contratacao DATE 
);

-- Criar tabela de Serviços
CREATE TABLE servicos (
    id_servico INT PRIMARY KEY AUTO_INCREMENT,
    descricao VARCHAR(200) NOT NULL,
    preco DECIMAL(10,2) NOT NULL,
    duracao_minutos INT NOT NULL
);

-- Criar tabela de Agendamentos
CREATE TABLE agendamentos (
    id_agendamento INT PRIMARY KEY AUTO_INCREMENT,
    id_cliente INT,
    id_funcionario INT,
    id_servico INT,
    data_hora DATETIME NOT NULL,
    status ENUM('Agendado', 'Concluído', 'Cancelado') DEFAULT 'Agendado',
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente),
    FOREIGN KEY (id_funcionario) REFERENCES funcionarios(id_funcionario),
    FOREIGN KEY (id_servico) REFERENCES servicos(id_servico)
);

-- Criar tabela de Pagamentos
CREATE TABLE pagamentos (
    id_pagamento INT PRIMARY KEY AUTO_INCREMENT,
    id_agendamento INT,
    valor DECIMAL(10,2) NOT NULL,
    metodo_pagamento ENUM('Dinheiro', 'Cartão', 'Pix') NOT NULL,
    data_pagamento DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_agendamento) REFERENCES agendamentos(id_agendamento)
);
````

# Após isso basta fazer a inserção de dados nas tabelas e acabou!
