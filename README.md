How many users are there?

select * from users;

response:

count (*)
50

What are the 5 most expensive items?
select * from items order by price desc limit 5;
response:
id|title|category|description|price
25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984
83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859
100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790
40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390
60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341
sqlite>

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

select * from items where category="Books" order by price asc limit 1;

repsonse:

76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496


Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
select * from users inner join addresses on users.id=addresses.id where addresses.street="6439 Zetta Hills"
Response:
43|Kyra|Kilback|demarcus.predovic@grimes.org|43|40|6439 Zetta Hills|Willmouth|WY|15029

Do they have another address?

select * from addresses where user_id=43 or id=43;
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

Correct Virginie Mitchell's address to "New York, NY, 10108".

update addresses set city="New York", state="NY", zip="10108" where user_id=39;
sqlite> select * from addresses where user_id=39;
id|user_id|street|city|state|zip
41|39|12263 Jake Crossing|New York|NY|10108
42|39|83221 Mafalda Canyon|New York|NY|10108

How much would it cost to buy one of each tool?

SELECT AVG(price) FROM items;
AVG(price)
4674.88

How many total items did we sell?

select sum(quantity) from orders;
sum(quantity)
2129

How much was spent on books?

select SUM(items.price) from items inner join orders on items.id=orders.item_id where items.category="Books";
SUM(items.price)
68982

Simulate buying an item by inserting a User for yourself and an Order for that User.

INSERT INTO users VALUES (51,'Charles','Mustaklem','charles.mustaklem@gmail.com');
INSERT INTO orders VALUES (378,51,93,4,datetime());
