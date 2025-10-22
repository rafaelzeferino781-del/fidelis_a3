# fidelis_a3
A3 SISTEMAS DISTRIBUIDOS E MOBILE
DROP TABLE IF EXISTS Transacoes;
DROP TABLE IF EXISTS Contas;
DROP TABLE IF EXISTS Clientes;

CREATE TABLE Clientes (
    cliente_id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    cpf TEXT UNIQUE NOT NULL,
    data_nascimento TEXT,
    endereco TEXT
);

CREATE TABLE Contas (
    numero_conta TEXT PRIMARY KEY,
    cliente_id INTEGER NOT NULL,
    tipo_conta TEXT NOT NULL CHECK (tipo_conta IN ('Corrente', 'Poupanca')),
    saldo REAL NOT NULL DEFAULT 0.00,
    data_abertura TEXT NOT NULL,
    status_conta TEXT NOT NULL DEFAULT 'Ativa' CHECK (status_conta IN ('Ativa', 'Inativa', 'Bloqueada')),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(cliente_id)
);

CREATE TABLE Transacoes (
    transacao_id INTEGER PRIMARY KEY AUTOINCREMENT,
    numero_conta TEXT NOT NULL,
    tipo_transacao TEXT NOT NULL CHECK (tipo_transacao IN ('Deposito', 'Saque', 'Transferencia')),
    valor REAL NOT NULL,
    data_hora TEXT DEFAULT CURRENT_TIMESTAMP,
    descricao TEXT,
    FOREIGN KEY (numero_conta) REFERENCES Contas(numero_conta)
);

