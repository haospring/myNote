~~~mysql
create table tb_dept(
dp_no int primary key auto_increment,
dp_name varchar(30) not null unique,
dp_tele varchar(30),
dp_mobile varchar(30),
dp_contacts varchar(30)
);
~~~

~~~shell
create table tb_cust(
ct_no int primary key auto_increment,
ct_registTime date,
ct_nature varchar(20),
ct_name varchar(30) not null,
ct_address varchar(30) not null,
ct_mobile varchar(11) not null,
ct_unitName varchar(30),
ct_tele varchar(20),
ct_mail varchar(30),
ct_gender varchar(10),
ct_IDCard varchar(18),
ct_bith date,
ct_hobbies varchar(30),
ct_remark varchar(100)
);
~~~

~~~mysql
insert into tb_dept values
(001,'财务部','0561-4685','18346821645','金鑫'),
(null,'人力资源部','4561-9513','18643891254','火焱'),
(null,'开发部','3695-1256','18546953765','水淼'),
(null,'测试部','6495-4628','18346597565','木森'),
(null,'摸鱼部','4683-4699','18246598565','土垚');
~~~

