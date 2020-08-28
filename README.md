# Full_Or_Incremental_Load
#### GET The process Details & Design Medium.com: https://medium.com/@apu.nandi88/full-and-incremental-data-loading-concept-from-source-to-destination-using-azure-data-factory-dd39627d6f21
###### Run SQL Query
---------------- Create & Insert Data into configuration_table ----------------------------[Target System]
create table dbo.configuration_table( Table_Name varchar(100),
Incremental_Full_Load int,
Max_Last_Updated_Date datetime,
Active_Indicator int
);

insert into dbo.configuration_table values('customer',0,null,1);
insert into dbo.configuration_table values('transaction_table',0,null,1);
insert into dbo.configuration_table values('promotion',0,null,0);

-------------------------- Create customer Table------------------------- [Source & Target System]
create table dbo.customer( cust_id int,
first_name varchar(30),
last_name varchar(30),
email varchar(30),
added_date datetime
);

-------------------- Insert Data into customer Table for 1st Run ----------------------------------[Source System]
insert into dbo.customer values(1000,'Amitava','Nandi','abc001@gmail.com',getdate());
insert into dbo.customer values(1001,'Sandeep','Paul','abc010@gmail.com',getdate());
insert into dbo.customer values(1002,'Amit','Kumar','dfg01@gmail.com',getdate());


-------------------------- Create transaction_table table------------------------- [Source & Target System]

create table dbo.transaction_table( trns_id int,
product_name varchar(30),
unit_price float,
quantity float,
promotion_flag int,
added_date datetime
);

-------------------- Insert Data transaction_table Table for 1st Run ------------------------------[Source System]

insert into dbo.transaction_table values(1111,'LG TV 0sd2',25000.00,1,0,getdate());
insert into dbo.transaction_table values(1112,'Snacks',50.25,10,0,getdate());
insert into dbo.transaction_table values(1113,'Toy0123',450.50,5,0,getdate());
insert into dbo.transaction_table values(1114,'Microwave',15800.00,1,0,getdate());
insert into dbo.transaction_table values(1115,'Mobile',16999.00,1,0,getdate());


-------------------------- Create promotion table ------------------------- [Source & Target System]
create table dbo.promotion( promo_id int,
product_name varchar(30),
promo_desc varchar(100),
benifit float,
added_date datetime
);

-------------------------- Insert Data promotion Table for 1st Run ---------------------------[Source System]
insert into dbo.promotion values(1,'Instant Off','Flat 10% off max 500',500,getdate());
insert into dbo.promotion values(2,'Instant Off','Flat 5% off max 800',800,getdate());


-------------------------- Create & Insert Data promotion Table after the 1st run and before 2nd Run------------------------- [Source System]

insert into dbo.transaction_table values(1111,'T-Shirt',1199.00,2,0,getdate()+1);
insert into dbo.transaction_table values(1111,'Masala & Species',29.00,8,0,getdate()+1);


