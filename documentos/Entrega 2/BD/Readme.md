CREATE DATABASE IF NOT EXISTS SistemaEscolar;
USE SistemaEscolar;

-- Tabela Jogo
CREATE TABLE Jogo (
    id_jogo INT PRIMARY KEY AUTO_INCREMENT,
    titulo_jogo VARCHAR(100) NOT NULL,
    categoria VARCHAR(50)
);

-- Tabela Pacote
CREATE TABLE Pacote (
    id_pacote INT PRIMARY KEY AUTO_INCREMENT,
    nome_pacote VARCHAR(100) NOT NULL,
    limite_acessos INT
);

-- Tabela Associativa Jogo_Pacote (Relacionamento N:N)
CREATE TABLE Jogo_Pacote (
    fk_id_jogo INT,
    fk_id_pacote INT,
    PRIMARY KEY (fk_id_jogo, fk_id_pacote),
    FOREIGN KEY (fk_id_jogo) REFERENCES Jogo(id_jogo) ON DELETE CASCADE,
    FOREIGN KEY (fk_id_pacote) REFERENCES Pacote(id_pacote) ON DELETE CASCADE
);

-- Tabela Escola
CREATE TABLE Escola (
    id_escola INT PRIMARY KEY AUTO_INCREMENT,
    nome_escola VARCHAR(150) NOT NULL,
    cnpj VARCHAR(18) UNIQUE NOT NULL,
    status_assinatura VARCHAR(20),
    fk_id_pacote INT,
    FOREIGN KEY (fk_id_pacote) REFERENCES Pacote(id_pacote)
);

-- Tabela Ip_autorizado
CREATE TABLE Ip_autorizado (
    id_ip INT PRIMARY KEY AUTO_INCREMENT,
    endereco_ip VARCHAR(15) NOT NULL,
    fk_id_escola INT NOT NULL,
    FOREIGN KEY (fk_id_escola) REFERENCES Escola(id_escola) ON DELETE CASCADE
);

-- Tabela Log_Acesso
CREATE TABLE Log_Acesso (
    id_log INT PRIMARY KEY AUTO_INCREMENT,
    data_hora_acesso DATETIME DEFAULT CURRENT_TIMESTAMP,
    fk_id_jogo INT NOT NULL,
    fk_id_escola INT NOT NULL,
    FOREIGN KEY (fk_id_jogo) REFERENCES Jogo(id_jogo),
    FOREIGN KEY (fk_id_escola) REFERENCES Escola(id_escola)
);
