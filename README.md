# intermediate-sql-queries-afternoon

For today we will be practicing inserting and querying data using SQL.

Here is a website that will let us write queries to interact with some data. http://jxs.me/chinook-web/

On the left are the Tables with their fields. The right is where we will be writing our queries. The bottom is where we will see our results.

Any new tables or records that we add into the database will be removed after you refresh the page. So if you're wondering where you data went, that may be why.

Use www.sqlteaching.com or sqlbolt.com as resources for the missing keywords you'll need.

## Practice joins

### Use at least one join for all of the following

__Examples__ 
```
Select [Column names] from [Table] [abbv] join [Table2] [abbv2] on abbv.prop=abbv2.prop where [Conditions]

Select a.Name, b.Name from someTable a join anotherTable b on a.someid=b.someid
Select a.Name, b.Name from someTable a join anotherTable b on a.someid=b.someid where b.email='e@mail.com'
```

* Get all invoices where the unit price on the invoice line is greater than $0.99
* Get all invoices and show me their invoice date, customer first and last names, and total

* Get all customers and show me their first name, last name, and support rep first name and last name (support reps are on the Employees table)

* Get all Albums and show me the album title and the artist name

* Get all Playlist Tracks where the playlist name is Music
* Get all Tracknames for playlistId 5
* Now we want all tracknames and the playlist name that they're on (You'll have to use 2 joins)

* Get all Tracks that are alternative and show me the track name and the album name (2 joins)

#### Black Diamond :

* Get all tracks on the playlist(s) called Music and show their name, genre name, album name, and artist name (at least 5 joins)


## Practice nested queries

### Use no joins for the following queries.  Use only nested queries.

__Examples__ 
```
Select [Column names] from [Table] where columnId in (select columnId from [Table2] where [Condition])

Select Name, email from athlete where athleteId in (select personId from pieEaters where flavor='Apple')
```

* Get all invoices where the unit price on the invoice line is greater than $0.99
* Get all Playlist Tracks where the playlist name is Music
* Get all Tracknames for playlistId 5
* Get all tracks where the genre is comedy
* Get all tracks where the album is Fireball
* Get all tracks for the artist queen Queen (2 nested subqueries)


## Practice updating Rows

__Examples__
```
Update [Table] set [column1]=[value1], [column2]=[value2] where [Condition]

Update Athletes set sport='Picklball' where sport='pockleball'
```

* Find all customers with fax numbers and set those numbers to null
* Find all customers with no company (null) and set their company to self
* Find the customer `Julia Barnett` and change her last name to `Thompson`
* Find the customer with this email `luisrojas@yahoo.cl` and change his support rep to rep 4

* Find all tracks that are of the genre `Metal` and that have no composer and set the composer to be 'The darkness around us'


Once you're done with all of those refresh your page to blow away your changes to the database!

## Group by

* Find a count of how many tracks there are per genre
* Find a count of all Tracks where the Genre is pop
* Find a list of all artist and how many albums they have

## Use Distinct

* From the tracks table find a unique list of all composers
* From the Invoice table find a unique list of all Billing postal codes
* From the Customer table find a unique list of all companies 

## Delete Rows

Always do a select before a delete to make sure you get back exactly what you want and only what you want to delete!

* Remove all pop tracks from the tracks table
* Remove all tracks by `Santana`
* Remove all of the rest of the tracks, yes all of them.

Now refresh your browser to reset all your data



## eCommerce simulation

Let's simulate an e-commerce site.  We're going to need users, products, and orders.

Users need a name and an email.
Products need a name and a price
Orders need a ref to product.
All 3 need primary keys.

Add some data to fill up each table (write down your schema since you won't see it on the side).  You'll need to insert products before you can link them.

Add 2 users, multiple products and multiple orders.

Run some queries against your data: 

* Get all products for the first order
* Get all orders
* Get the total cost of an order (sum the price of all products on an order)

## Add foreign key to existing table

Orders have products, but someone needs to place the order.

Add a ref from Orders to Users.  
Add some users.
Update the Orders table to link the a user to each order.

Run some queries against your data:

* Get all orders for a user
* Get how many orders each user has
* __Black Diamond:__ Get the total spend on all orders for each user
