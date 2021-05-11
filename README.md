# apireset
 CREATE TABLE produto ( 02  idproduto INTEGER  NOT NULL   IDENTITY , 03  descricao VARCHAR(100)    , 04  preco_compra DECIMAL(6,2)    , 05  preco_venda DECIMAL(6,2)    , 06  qtde_estoque INTEGER    , 07  data_cadastro DATE    , 08  status_produto VARCHAR(20)      , 09 PRIMARY KEY(idproduto)); 10 GO 11 12 CREATE TABLE cliente ( 13  idcliente INTEGER  NOT NULL   IDENTITY , 14  nome VARCHAR(100)    , 15  cpf_cnpj VARCHAR(18)    , 16  endereco VARCHAR(200)    , 17  bairro VARCHAR(40)    , 18  cidade VARCHAR(40)    , 19  cep VARCHAR(10)    , 20  email VARCHAR(50)    , 21  telefone VARCHAR(15)    , 22  status_cliente VARCHAR(20)    , 23  data_cadastro DATE      , 24 PRIMARY KEY(idcliente)); 25 GO 26 27 CREATE TABLE pedido_cabecalho ( 28  idpedido_cabecalho INTEGER  NOT NULL   IDENTITY , 29  idcliente INTEGER  NOT NULL  , 30  valor_total_pedido DECIMAL(6,2)    , 31  qtde_itens INTEGER    , 32  status_pedido VARCHAR(20)    , 33  data_pedido DATE      , 34 PRIMARY KEY(idpedido_cabecalho)  , 35  FOREIGN KEY(idcliente) 36    REFERENCES cliente(idcliente)); 37 GO 38 39 CREATE INDEX pedido_cabecalho_FKIndex1 ON pedido_cabecalho (idcliente); 40 GO 41 42 CREATE INDEX IFK_Rel_Cliente__Ped_Cab ON pedido_cabecalho (idcliente); 43 GO 44 45 CREATE TABLE pedido_itens ( 46  idpedido_itens INTEGER  NOT NULL   IDENTITY , 47  idpedido_cabecalho INTEGER  NOT NULL  , 48  idproduto INTEGER  NOT NULL  , 49  quantidade INTEGER    , 50  valor_unitario DECIMAL(6,2)    , 51  sub_total DECIMAL(6,2)    , 52  status_item VARCHAR(20)      , 53 PRIMARY KEY(idpedido_itens)    , 54  FOREIGN KEY(idpedido_cabecalho) 55    REFERENCES pedido_cabecalho(idpedido_cabecalho), 56  FOREIGN KEY(idproduto) 57    REFERENCES produto(idproduto)); 58 GO 59 60 CREATE INDEX pedido_itens_FKIndex1 ON pedido_itens (idpedido_cabecalho); 61 GO 62 CREATE INDEX pedido_itens_FKIndex2 ON pedido_itens (idproduto); 63 GO 64 65 CREATE INDEX IFK_Rel_PedCab__Ped_Itens ON pedido_itens (idpedido_cabecalho); 66 GO 67 CREATE INDEX IFK_Rel_Produto__Ped_Itens ON pedido_itens (idproduto); 68 GO
