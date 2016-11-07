How many users are there?

select count(*) from users;

response:


51 (this should be 50, but I have done a lot of work on this file)

What are the 5 most expensive items?
select * from items order by price desc limit 5;
response:
id          title                category                    description                         price     
----------  -------------------  --------------------------  ----------------------------------  ----------
25          Small Cotton Gloves  Automotive, Shoes & Beauty  Multi-layered modular service-desk  9984      
83          Small Wooden Comput  Health                      Re-engineered fault-tolerant adapt  9859      
100         Awesome Granite Pan  Toys & Books                Upgradable 24/7 access              9790      
40          Sleek Wooden Hat     Music & Baby                Quality-focused heuristic info-med  9390      
60          Ergonomic Steel Car  Books & Outdoors            Enterprise-wide secondary firmware  9341


What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

select * from items where category="Books" order by price asc limit 1;

repsonse:

id          title                    category    description                          price     
----------  -----------------------  ----------  -----------------------------------  ----------
76          Ergonomic Granite Chair  Books       De-engineered bi-directional portal  1496


select * from items where category like "%Books%" order by price asc limit 1;

response:

76	Ergonomic Granite Chair	Books	De-engineered bi-directional portal	1496

There is no difference


Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
select * from users inner join addresses on users.id=addresses.user_id where addresses.street="6439 Zetta Hills"
Response:
40	Corrine	Little	rubie_kovacek@grimes.net	43	40	6439 Zetta Hills	Willmouth	WY	15029

Do they have another address?

select * from addresses where user_id=43;
id|user_id|street|city|state|zip
43|40|6439 Zetta Hills|Willmouth|WY|15029
47|43|405 Zulauf Park|North Pascale|OK|51657



Correct Virginie Mitchell's address to "New York, NY, 10108".

select * from users where first_name="Virginie" and last_name="Mitchell";
id|first_name|last_name|email
39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz
sqlite> select * from addresses where user_id=39;
id|user_id|street|city|state|zip
41|39|12263 Jake Crossing|Roxanehaven|NY|34705
42|39|83221 Mafalda Canyon|Bahringerland|WY|24028

update addresses set city="New York", state="NY", zip="10108" where user_id=39;
sqlite> select * from addresses where user_id=39;
id|user_id|street|city|state|zip
41|39|12263 Jake Crossing|New York|NY|10108
42|39|83221 Mafalda Canyon|New York|NY|10108

//I misunderstood the question. I thought that we would need to updated both questions. I thought that were were going to update both addresses. I see now that we would only need to update one of the addresses.

For this, the query is...

UPDATE addresses SET city = "New York", state= "NY", zip=10108 WHERE id = 41;

select * from addresses where id=41;
id          user_id     street               city        state       zip       
----------  ----------  -------------------  ----------  ----------  ----------
41          39          12263 Jake Crossing  New York    NY          10108

How much would it cost to buy one of each tool?

select sum(price) from items where category like '%Tools%';
sum(price)
46477

How many total items did we sell?

select sum(quantity) from orders;

2129

//there are 378 orders because I ran this after creating that new order.

How much was spent on books?

select SUM(items.price * orders.quantity) from items inner join orders on items.id=orders.item_id where items.category like "%Books%";

1081352


Simulate buying an item by inserting a User for yourself and an Order for that User.

INSERT INTO users VALUES (51,'Charles','Mustaklem','charles.mustaklem@gmail.com');
INSERT INTO orders VALUES (378,51,93,4,datetime());
