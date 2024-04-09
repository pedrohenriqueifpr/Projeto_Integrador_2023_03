CREATE TABLE Cliente (
    idCliente INT(11) AUTO_INCREMENT PRIMARY KEY,
    nomeCliente VARCHAR(100) NOT NULL DEFAULT '0',
    cpfCliente VARCHAR(14) NOT NULL DEFAULT '0',
    dataNascimento DATETIME NOT NULL DEFAULT '1900-01-01',
    docIdentificador VARCHAR(20) NOT NULL DEFAULT '0',
    orgaoEmissor VARCHAR(50) NOT NULL DEFAULT '0',
    ufEmissor VARCHAR(2) NOT NULL DEFAULT '0',
    dataEmissao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    naturalidadeCliente VARCHAR(100) NOT NULL DEFAULT '0',
    idEstadoCivil INT(11) NOT NULL DEFAULT 0,
    idSexo INT(11) NOT NULL DEFAULT 0,
    nomeMae VARCHAR(100) NOT NULL DEFAULT '0',
    nomePai VARCHAR(100) NOT NULL DEFAULT '0',
    obsCliente VARCHAR(140) NOT NULL DEFAULT '0'
);

CREATE TABLE EstadoCivil (
    idEstadoCivil INT(11) AUTO_INCREMENT PRIMARY KEY,
    estadoCivil VARCHAR(20) NOT NULL
);

CREATE TABLE Sexo(
    idSexo INT(11) AUTO_INCREMENT PRIMARY KEY,
    genero VARCHAR(20) NOT NULL
);

CREATE TABLE Endereco(
    idEndereco INT(11) AUTO_INCREMENT PRIMARY KEY,
    idCliente INT(11) NOT NULL,
    enderecoCliente VARCHAR(100) NOT NULL DEFAULT '0',
    numeroCliente VARCHAR(10) NOT NULL DEFAULT '0',
    complementoCliente VARCHAR(100) NOT NULL DEFAULT '0',
    bairroCliente VARCHAR(100) NOT NULL DEFAULT '0',
    cidadeCliente VARCHAR(100) NOT NULL DEFAULT '0',
    ufCliente VARCHAR(2) NOT NULL DEFAULT '0',
    cepCliente VARCHAR(9) NOT NULL DEFAULT '0',
    telefoneCliente VARCHAR(20) NOT NULL DEFAULT '0',
    emailCliente VARCHAR(100) NOT NULL DEFAULT '0'
);

CREATE TABLE Emprestimo (
    idEmprestimo INT(11) AUTO_INCREMENT PRIMARY KEY,
    idCliente INT(11) NOT NULL,
    tipoEmprestimo VARCHAR(100) NOT NULL DEFAULT '0',
    valorEmprestimo DECIMAL (15,2) DEFAULT 0,
    parcelaEmprestimo DECIMAL (15, 2) DEFAULT 0,
    prazoEmprestimo DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    adeEmprestimo VARCHAR(100) NOT NULL DEFAULT '0',
    idPromotora  INT(11) NOT NULL,
    idOrgao INT(11) NOT NULL,
    dataEmprestimo DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    comissaoEmprestimo DECIMAL (15, 2) DEFAULT 0
); 

CREATE TABLE Promotora (
    idPromotora  INT(11) AUTO_INCREMENT PRIMARY KEY,
    promotoraEmprestimo VARCHAR(100) NOT NULL
);

CREATE TABLE Orgao (
    idOrgao INT(11) AUTO_INCREMENT PRIMARY KEY,
    orgaoEmprestimo VARCHAR(100) NOT NULL 
);

CREATE TABLE dadosBancarios (
    idDadosBancarios INT(11) AUTO_INCREMENT PRIMARY KEY,
    idBanco INT(11) NOT NULL,
    idCliente INT(11) NOT NULL,
    cpfTitularBanco VARCHAR(14) NOT NULL DEFAULT '0',
    agenciaBanco VARCHAR(20) NOT NULL DEFAULT '0',
    contaBanco VARCHAR(20) NOT NULL DEFAULT '0'
);

CREATE TABLE Banco (
    idBanco INT(11) AUTO_INCREMENT PRIMARY KEY,
    codigoBanco VARCHAR(10) NOT NULL
);

ALTER TABLE Cliente ADD CONSTRAINT fkEstadoCivil FOREIGN KEY (idEstadoCivil) REFERENCES EstadoCivil(idEstadoCivil);
ALTER TABLE Cliente ADD CONSTRAINT fkSexo FOREIGN KEY (idSexo) REFERENCES Sexo(idSexo);

ALTER TABLE Endereco ADD CONSTRAINT fkClienteEndereco FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente);

ALTER TABLE dadosBancarios ADD CONSTRAINT fkClienteDadosBancarios FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente);
ALTER TABLE dadosBancarios ADD CONSTRAINT fkBanco FOREIGN KEY (idBanco) REFERENCES Banco(idBanco);

ALTER TABLE Emprestimo ADD CONSTRAINT fkClienteEmprestimo FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente);
ALTER TABLE Emprestimo ADD CONSTRAINT fkEmprestimoPromotora FOREIGN KEY (idPromotora) REFERENCES Promotora(idPromotora);
ALTER TABLE Emprestimo ADD CONSTRAINT fkEmprestimoOrgao FOREIGN KEY (idOrgao) REFERENCES Orgao(idOrgao);

INSERT INTO EstadoCivil 
    (estadoCivil)
VALUES 
    ('Solteiro(a)'),
    ('Casado(a)'),
    ('Divorciado(a)'),
    ('Viúvo(a)');

INSERT INTO Sexo 
    (genero)
VALUES 
    ('Masculino'),
    ('Feminino');
