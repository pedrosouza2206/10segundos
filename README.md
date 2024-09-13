
create database bd_loja;

use bd_loja;

create table tb_produto(
cd_produto int auto_increment,
nm_produto varchar(50) not null,
vl_produto decimal(6,2),
qt_estoque int,
Primary Key (cd_produto)
);

create table tb_cliente(
cpf_cliente char(11),
nm_cliente varchar(80) not null,
nr_fone varchar(11) not null,
nm_endereco varchar(50),
nr_endereco int,
nm_bairro varchar(30),
id_status bit not null default 0,
primary key (cpf_cliente)
);

create table tb_pedido(
cd_pedido int auto_increment,
dt_pedido date not null,
vl_total decimal(6,2) not null,
id_pagamento char(1),
fk_cpf_cliente char(11),
Primary key (cd_pedido),
foreign key (fk_cpf_cliente) references tb_cliente (cpf_cliente)
);
create table tb_item(
cd_item int auto_increment,
fk_cd_pedido int,
fk_cd_produto int,
qt_item_produto int not null,
vl_item decimal(6,2),
primary key (cd_item),
foreign key(fk_cd_pedido) references tb_pedido (cd_pedido),
foreign key (fk_cd_produto) references tb_produto (cd_produto)
);
create table tb_agenda(
cd_agenda int auto_increment,
dt_agenda date not null,
hr_agenda time not null,
fk_cpf_cliente char(11),
primary key (cd_agenda),
foreign key (fk_cpf_cliente) references tb_cliente (cpf_cliente)
);

/*ATIVIDADE COMEÇA AQUI*/

Alter table tb_cliente
change nr_fone fone_cliente varchar(11) not null;

alter table tb_cliente
add sg_estado char(2);

alter table tb_produto
modify vl_produto decimal(5,2);

alter table tb_pedido
drop column id_pagamento;

alter table tb_pedido
modify vl_total decimal(6,2) null;

describe tb_pedido;

Insert into tb_cliente (cpf_cliente, nm_cliente, fone_cliente, nm_endereco, nr_endereco, nm_bairro, id_status, sg_estado) 
values ('815648954', 'Fernando Henrique', '139458962', 'Rua do Campo', 485, 'Balneario Nosso', 0, 'SP'), 
('12345678912', 'Arnaldo Ferreira', '139458963', 'Rua das Mariposas', 1008, 'Mariposas Legais', 1, 'SP'),
('12345678918', 'Geovana Santos', '139458978', 'Av. das Ferreiras', 56, 'Ferro da Quinze', 1, 'SP'),
('12345678949', 'Caique Bento', '139458278', 'Av. das Ferreiras', 58, 'Ferro da Quinze', 0, 'SP'),
('12345678969', 'Naiara Hervantes', '139451271', 'Rua do Caiçara', 987, 'Ferro da Quinze', 1, 'SP');

Select * from tb_cliente;

Insert into tb_produto (nm_produto, vl_produto, qt_estoque)
values ('Gol', 670, 2),
('Uno', 990, 5),
('Palio', 436, 10),
('Fox/CrossFox', 990, 6),
('Siena', 270, 4),
('Celta', 900, 9),
('Voyage', 110, 3),
('HB20', 090, 11),
('Corsa Sedan', 287, 16),
('Onix', 900, 5);

Select * from tb_produto;

Insert into tb_pedido (dt_pedido, vl_total, fk_cpf_cliente) 
values ('2022-03-07', null, '815648954'),
('2022-03-06', null, '12345678912'),
('2022-03-05', null, '12345678912'),
('2022-03-03', null, '12345678912'),
('2022-03-01', null, '12345678949'),
('2022-02-26', null, '12345678949'),
('2022-02-24', null, '12345678918'),
('2022-02-18', null, '12345678912');

SELECT * FROM tb_pedido;

Insert into tb_item(fk_cd_pedido, fk_cd_produto, qt_item_produto, vl_item) 
values (1, 1, 1, 670),
(2, 2, 1, 990),
(3, 3, 1, 436),
(4, 4, 1, 990),
(5, 5, 1, 270),
(6, 6, 1, 900),
(7, 7, 1, 110),
(8, 8, 1, 90),
(1, 9, 1, 287),
(2, 10, 1, 900),
(3, 1, 1, 670),
(5, 2, 1, 990),
(8, 3, 1, 436),
(7, 4, 1, 990),
(2, 5, 1, 270),
(1, 6, 1, 900),
(4, 7, 1, 110),
(2, 8, 1, 90),
(6, 9, 1, 287),
(8, 10, 1, 900);

select * from tb_item;

insert into tb_agenda (dt_agenda, hr_agenda, fk_cpf_cliente)
values ('2022-03-25', '13:15:30', '815648954'),
('2022-03-12', '15:15:30', '12345678912'),
('2022-03-26', '16:15:30', '12345678918'),
('2022-03-29', '09:15:30', '12345678949'),
('2022-03-14', '13:15:30', '12345678969'),
('2022-03-16', '17:15:30', '12345678918'),
('2022-03-24', '13:15:30', '12345678969'),
('2022-03-25', '14:15:30', '12345678912'),
('2022-03-26', '12:15:30', '815648954'),
('2022-03-18', '20:15:30', '12345678918');

select * from tb_agenda;


Busque os registros da tabela agenda cujos códigos sejam 5 e 6 
Exiba todos os registros da tabela item que possua o código do produto 3 
Liste os dados do cliente que  está no terceiro registro da tabela cliente. 
Exiba nome e valor dos produtos com código maior que 6 
Mostre o código e a data do pedido de código 2 
Busque os produtos cujo valor seja maior que 20 ou o código menor que 10 
Exiba todos os itens que pertencem ao pedido de código 4 
Busque na tabela agenda os registros de código menor que 8 e que o horário seja antes do meio dia 
Exiba os clientes com status 1 
Exiba os dados do cliente que tenham a sigla do estado RJ 
Listar todos os nomes de clientes que contenham o sobrenome SANTOS 
Listar os nomes dos clientes que contenham a palavra ANA 
Exiba todos os agendamentos que estejam marcadas no dia 15/04/2022 entre os horários das 10h até às 16h 
Exiba o código do pedido que contenham os produtos de código: 1, 7,10 
Liste todos os pedidos feitos no período da semana de férias (10/07/2022 a 30/07/2022) 


