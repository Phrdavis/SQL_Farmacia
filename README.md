<h1>SQL_Farmacia</h1>

<p>Um script SQL para o controle de uma Farmacia, desde o atendimento até o fornecimento de medicação utilizando AZURE DATA STUDIO.</p>

<h2>Como criar o Banco</h2>

<p>Aqui o funcionamento do script criado para que você possa se localizar melhor :)</p>

<ul>

<li>Utilize a primeira linha para criar o banco <em>FARMACIA</em></li>

``` sql

CREATE DATABASE FARMACIA

```

<li>A linha três servirá para utilizar o banco criado</li>

``` sql

USE FARMACIA

```

<li>Na linha 5 será criado a tabela <em>LOCAL</em></li>

``` sql

CREATE TABLE LOCAL(
    local_cod INT CONSTRAINT PK_local PRIMARY KEY,
    local_rua CHAR(20),
    local_bairro CHAR(20),
    local_cidade CHAR(20),
    local_contato INT
)

```

<li>Na linha 13 será criado a tabela <em>FUNCIONARIOS</em></li>

``` sql

CREATE TABLE FUNCIONARIOS(
    func_cod INT CONSTRAINT PK_funcionarios PRIMARY KEY,
    local_cod INT,
    CONSTRAINT PK_local_funcionario FOREIGN KEY (local_cod) REFERENCES LOCAL(local_cod),
    func_nome CHAR(20),
    func_cpf INT,
    func_dn DATE,
    func_sal MONEY,
    func_contato INT
)

```

<li>Na linha 24 será criado a tabela <em>CLIENTE</em></li>

``` sql

CREATE TABLE CLIENTE(
    cliente_cod INT CONSTRAINT PK_cliente PRIMARY KEY,
    cliente_nome CHAR(20),
    cliente_cpf INT,
    cliente_dn DATE,
    cliente_contato INT
)

```

<li>Na linha 33 será criado a tabela <em>FORNECEDORES</em></li>

``` sql

CREATE TABLE FORNECEDORES(
    forne_cod INT CONSTRAINT PK_fornecedor PRIMARY KEY,
    forne_nome CHAR(20),
    forne_contato INT
)

```

<li>Na linha 39 será criado a tabela <em>MEDICAMENTOS</em></li>

``` sql

CREATE TABLE MEDICAMENTOS(
    med_cod INT CONSTRAINT PK_medicamentos PRIMARY KEY,
    forne_cod INT,
    CONSTRAINT PK_fornecedor_medicamento FOREIGN KEY (forne_cod) REFERENCES FORNECEDORES(forne_cod),
    validade DATE
)

```

<li>Na linha 46 será criado a tabela <em>ATENDIMENTO</em></li>

``` sql

CREATE TABLE ATENDIMENTO(
    atend_cod INT CONSTRAINT PK_atendimento PRIMARY KEY,
    cliente_cod INT,
    CONSTRAINT PK_atendimento_cliente FOREIGN KEY (cliente_cod) REFERENCES CLIENTE(cliente_cod),
    func_cod INT,
    CONSTRAINT PK_atendimento_funcionario FOREIGN KEY (func_cod) REFERENCES FUNCIONARIOS(func_cod),
    med_cod INT,
    CONSTRAINT PK_atendimento_medicamentos FOREIGN KEY (med_cod) REFERENCES MEDICAMENTOS(med_cod),
    atend_data DATE
)

```

</ul>

<h2>Inserindo informações no banco</h2>
<p>Aqui pode-se ver uma parte do script onde são inseridos algumas informações dentro do banco</p>

<ul>

<li>Da linha 57 até a 67 tem os <em>INSERT</em> e os <em>VALUES</em> da tabela <em>LOCAL</em></li>

``` sql

INSERT INTO LOCAL (local_cod, local_rua, local_bairro, local_cidade, local_contato)
VALUES (1, 'Palmeiras', 'América', 'Joinville', 47000)

INSERT INTO LOCAL (local_cod, local_rua, local_bairro, local_cidade, local_contato)
VALUES (2, 'EStivadores', 'América', 'Joinville', 45645)

INSERT INTO LOCAL (local_cod, local_rua, local_bairro, local_cidade, local_contato)
VALUES (3, 'José da silva', 'América', 'Joinville', 76889)

INSERT INTO LOCAL (local_cod, local_rua, local_bairro, local_cidade, local_contato)
VALUES (4, 'Magazine Luiza', 'América', 'Joinville', 12345)

```

<li>Da linha 69 até a 79 tem os <em>INSERT</em> e os <em>VALUES</em> da tabela <em>FUNCIONARIOS</em></li>

``` sql

INSERT INTO FUNCIONARIOS (func_cod, local_cod,func_nome,func_cpf,func_dn,func_sal,func_contato)
VALUES (1, 1,'Davi', 00000000000, '2002-04-02', '1200', 12345)

INSERT INTO FUNCIONARIOS (func_cod, local_cod,func_nome,func_cpf,func_dn,func_sal,func_contato)
VALUES (2,2,'Maria', 00000000000, '2002-04-02', '1800', 78945)

INSERT INTO FUNCIONARIOS (func_cod, local_cod,func_nome,func_cpf,func_dn,func_sal,func_contato)
VALUES (3, 3,'Carlos', 00000000000, '2002-04-02', '2000', 12335)

INSERT INTO FUNCIONARIOS (func_cod, local_cod,func_nome,func_cpf,func_dn,func_sal,func_contato)
VALUES (4, 4,'Gabriel', 00000000000, '2002-04-02', '6500', 74158)

```

<li>Da linha 81 até a 91 tem os <em>INSERT</em> e os <em>VALUES</em> da tabela <em>CLIENTE</em></li>

``` sql

INSERT INTO CLIENTE (cliente_cod, cliente_nome,cliente_cpf,cliente_dn,cliente_contato)
VALUES (1,'Jefferson', 00000000000, '2002-04-02', 12345)

INSERT INTO CLIENTE (cliente_cod, cliente_nome,cliente_cpf,cliente_dn,cliente_contato)
VALUES (2,'Pedro', 00000000000, '1976-04-02', 12345)

INSERT INTO CLIENTE (cliente_cod, cliente_nome,cliente_cpf,cliente_dn,cliente_contato)
VALUES (3,'Diogo', 00000000000, '1999-04-02', 12345)

INSERT INTO CLIENTE (cliente_cod, cliente_nome,cliente_cpf,cliente_dn,cliente_contato)
VALUES (4,'Lucas', 00000000000,'1980-04-02', 12345)

```

<li>Da linha 93 até a 103 tem os <em>INSERT</em> e os <em>VALUES</em> da tabela <em>FORNECEDORES</em></li>

``` sql

INSERT INTO FORNECEDORES (forne_cod, forne_nome, forne_contato)
VALUES (1, 'M&M', 12345)

INSERT INTO FORNECEDORES (forne_cod, forne_nome, forne_contato)
VALUES (2, 'Casas da Mata', 12345)

INSERT INTO FORNECEDORES (forne_cod, forne_nome, forne_contato)
VALUES (3, 'Univille', 12345)

INSERT INTO FORNECEDORES (forne_cod, forne_nome, forne_contato)
VALUES (4, 'Posto Shell', 12345)

```

<li>Da linha 105 até a 115 tem os <em>INSERT</em> e os <em>VALUES</em> da tabela <em>MEDICAMENTOS</em></li>

``` sql

INSERT INTO MEDICAMENTOS (med_cod, validade, forne_cod)
VALUES (1, '2022-10-06', 1)

INSERT INTO MEDICAMENTOS (med_cod, validade, forne_cod)
VALUES (2, '2022-10-06', 2)

INSERT INTO MEDICAMENTOS (med_cod, validade, forne_cod)
VALUES (3, '2022-9-06', 3)

INSERT INTO MEDICAMENTOS (med_cod, validade, forne_cod)
VALUES (4, '2022-8-06', 4)

```

<li>Da linha 117 até a 127 tem os <em>INSERT</em> e os <em>VALUES</em> da tabela <em>ATENDIMENTO</em></li>

``` sql

INSERT INTO ATENDIMENTO (atend_cod, cliente_cod, func_cod, med_cod, atend_data)
VALUES (1,1,1,1, '2022-10-06')

INSERT INTO ATENDIMENTO (atend_cod, cliente_cod, func_cod, med_cod, atend_data)
VALUES (2,2,2,2, '2022-10-06')

INSERT INTO ATENDIMENTO (atend_cod, cliente_cod, func_cod, med_cod, atend_data)
VALUES (3,3,3,3, '2022-10-06')

INSERT INTO ATENDIMENTO (atend_cod, cliente_cod, func_cod, med_cod, atend_data)
VALUES (4,4,4,4, '2022-10-06')

```

</ul>

<h2>Atualizando tabelas</h2>
<p>Aqui iremos atualizar alguns valores e informações presentes dentro das tabelas</p>

<ul>

<li><em>UPDATES</em> na tabela <em>MEDICAMENTOS</em></li>

``` sql

UPDATE MEDICAMENTOS SET validade = '1990-8-06', forne_cod = 1 WHERE med_cod = 1

UPDATE MEDICAMENTOS SET validade = '1990-5-27', forne_cod = 1 WHERE med_cod = 2

```

<li><em>UPDATES</em> na tabela <em>FORNECEDORES</em></li>

``` sql

UPDATE FORNECEDORES SET forne_contato = 101010, forne_nome = 'Lorenzetti' WHERE forne_cod = 1

UPDATE FORNECEDORES SET forne_contato = 202020, forne_nome = 'Brastemp' WHERE forne_cod = 2

```

<li><em>UPDATES</em> na tabela <em>CLIENTE</em></li>

``` sql

UPDATE CLIENTE SET cliente_contato = 12345, cliente_dn = 1999 WHERE cliente_cod = 1 

UPDATE CLIENTE SET cliente_contato = 101010, cliente_dn = 2000 WHERE cliente_cod = 2

```

<li><em>UPDATES</em> na tabela <em>FUNCIONARIOS</em></li>

``` sql

UPDATE FUNCIONARIOS SET func_nome = 'José', func_dn = '1976-04-17' WHERE func_cod = 1 

UPDATE FUNCIONARIOS SET func_nome = 'Mafalda', func_dn = '1976-04-17' WHERE func_cod = 2

```

<li><em>UPDATES</em> na tabela <em>LOCAL</em></li>

``` sql

UPDATE LOCAL SET local_cidade = 'São Francisco', local_contato = 54321 WHERE local_cod = 1 

UPDATE LOCAL SET local_cidade = 'São Paulo', local_contato = 10923 WHERE local_cod = 3 

```


<li><em>UPDATES</em> na tabela <em>ATENDIMENTO</em></li>

``` sql

UPDATE ATENDIMENTO SET func_cod = 4, med_cod = 2 WHERE atend_cod = 3

UPDATE ATENDIMENTO SET func_cod = 2, med_cod = 4 WHERE atend_cod = 4

```
</ul>

<h2>Selecionando as tabelas</h2>

<p>Por fim iremos selecionar as tabelas utilizando as ultimas linhas do script</p>

``` sql

SELECT * FROM ATENDIMENTO
SELECT * FROM CLIENTE
SELECT * FROM FUNCIONARIOS
SELECT * FROM MEDICAMENTOS
SELECT * FROM FORNECEDORES

```
