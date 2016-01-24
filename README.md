# MongoDB BI Connector

## Download & Install

* Go to MongoDB Download & get all the rpms
* sudo yum install -y *.rpm
* Load sample database  sakila into MongoDB

#### Populate local mongodb database

	mongorestore sakila-dump/
#### Create BI User

	mongobiuser create biuser mongodb://localhost:27017/sakila
#### Generate Schema file

	mongodrdl --host localhost -d sakila -o sakila-schema.drdl

#### Load schema

	mongobischema import biuser sakila-schema.drdl
	
	2016-01-21T03:45:51.759-0500	creating table customer
	2016-01-21T03:45:51.776-0500	creating table customer_Rentals
	2016-01-21T03:45:51.780-0500	creating table customer_Rentals_Payments
	2016-01-21T03:45:51.783-0500	creating table film
	2016-01-21T03:45:51.786-0500	creating table film_Actors
	2016-01-21T03:45:51.790-0500	creating table payment
	2016-01-21T03:45:51.793-0500	creating table store
	2016-01-21T03:45:51.796-0500	creating table store_Inventory
	2016-01-21T03:45:51.800-0500	creating table store_Staff


#### Test the connector

	$ psql -U biuser -W  -h localhost
	psql (9.4.5 MongoDB BI Connector 1.0.0)
	SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
	Type "help" for help.
	
	biuser=> 
	biuser=> \d
	                        List of relations
	 Schema |             Name              |     Type      | Owner  
	--------+-------------------------------+---------------+--------
	 public | customer                      | view          | biuser
	 public | customer_Rentals              | view          | biuser
	 public | customer_Rentals_Payments     | view          | biuser
	 public | customer_Rentals_Payments_fdw | foreign table | biuser
	 public | customer_Rentals_fdw          | foreign table | biuser
	 public | customer_fdw                  | foreign table | biuser
	 public | film                          | view          | biuser
	 public | film_Actors                   | view          | biuser
	 public | film_Actors_fdw               | foreign table | biuser
	 public | film_fdw                      | foreign table | biuser
	 public | payment                       | view          | biuser
	 public | payment_fdw                   | foreign table | biuser
	 public | store                         | view          | biuser
	 public | store_Inventory               | view          | biuser
	 public | store_Inventory_fdw           | foreign table | biuser
	 public | store_Staff                   | view          | biuser
	 public | store_Staff_fdw               | foreign table | biuser
	 public | store_fdw                     | foreign table | biuser
	(18 rows)


    biuser=> 
	  biuser=> select * from customer;
	                Address                 |            City            |                Country                |       District       | First Name  |  Last Name   |    Phone     | _id 
  	----------------------------------------+----------------------------+---------------------------------------+----------------------+-------------+--------------+--------------+-----
  	 1913 Hanoi Way                         | Sasebo                     | Japan                                 | Nagasaki             | MARY        | SMITH        | 28303384290  |   1
  	 1121 Loja Avenue                       | San Bernardino             | United States                         | California           | PATRICIA    | JOHNSON      | 838635286649 |   2
  	 692 Joliet Street                      | Athenai                    | Greece                                | Attika               | LINDA       | WILLIAMS     | 448477190408 |   3
  	 1566 Inegl Manor                       | Myingyan                   | Myanmar                               | Mandalay             | BARBARA     | JONES        | 705814003527 |   4
  	 53 Idfu Parkway                        | Nantou                     | Taiwan                                | Nantou               | ELIZABETH   | BROWN        | 10655648674  |   5
  	 1795 Santiago de Compostela Way        | Laredo                     | United States                         | Texas                | JENNIFER    | DAVIS        | 860452626434 |   6
  	 900 Santiago de Compostela Parkway     | Kragujevac                 | Yugoslavia                            | Central Serbia       | MARIA       | MILLER       | 716571220373 |   7
  	 478 Joliet Way                         | Hamilton                   | New Zealand                           | Hamilton             | SUSAN       | WILSON       | 657282285970 |   8
  	 613 Korolev Drive                      | Masqat                     | Oman                                  | Masqat               | MARGARET    | MOORE        | 380657522649 |   9
  	 1531 Sal Drive                         | Esfahan                    | Iran                                  | Esfahan              | DOROTHY     | TAYLOR       | 648856936185 |  10
  	 1542 Tarlac Parkway                    | Sagamihara                 | Japan                                 | Kanagawa             | LISA        | ANDERSON     | 635297277345 |  11
  	 808 Bhopal Manor                       | Yamuna Nagar               | India                                 | Haryana              | NANCY       | THOMAS       | 465887807014 |  12
  	 270 Amroha Parkway                     | Osmaniye                   | Turkey                                | Osmaniye             | KAREN       | JACKSON      | 695479687538 |  13
  	 770 Bydgoszcz Avenue                   | Citrus Heights             | United States                         | California           | BETTY       | WHITE        | 51
