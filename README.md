<img src="https://devmounta.in/img/logowhiteblue.png" width="250" align="right">

# Project Summary

In this project, we'll continue to use <a href="http://jxs.me/chinook-web/">Chinook</a> to practice joins, nested queries, updating rows, group by, distinct, and foreign keys.

Any new tables or records that you add into the database will be removed after you refresh the page.

Use <a href="www.sqlteaching.com">SQL Teaching</a> or <a href="www.sqlbolt.com">SQL Bolt</a> as resources for referencing on keywords you'll need.

## Practice joins

### Instructions

<details>

<summary> <code> Syntax Hint </code> </summary>

```sql
SELECT [Column names] 
FROM [Table] [abbv]
JOIN [Table2] [abbv2] ON abbv.prop = abbv2.prop WHERE [Conditions];

SELECT a.Name, b.Name FROM SomeTable a JOIN AnotherTable b ON a.someid = b.someid;
SELECT a.Name, b.Name FROM SomeTable a JOIN AnotherTable b ON a.someid = b.someid WHERE b.email = 'e@mail.com';
```

</details>

<br />

1. Get all invoices where the total is greater than $0.99.
2. Get the invoice date, customer first and last names, and total from all invoices.
3. Get the first name, last name, and support rep's first name and last name from all customers. 
    * Support reps are on the Employee table.
4. Get the album title and the artist name from all albums.
5. Get all Playlist Tracks where the playlist name is Music.
6. Get all Tracknames for playlistId 5.
7. Now we want all tracknames and the playlist name that they're on ( 2 joins ).
8. Get all Tracks that are alternative and show me the track name and the album name ( 2 joins ).

### Solution

<details>

<summary> <code> SQL Solutions </code> </summary>

<details>

<summary> <code> #1 </code> </summary>

```sql
SELECT *
FROM Invoice i
JOIN InvoiceLine il ON il.UnitPrice > 0.99;
```

</details>

<details>

<summary> <code> #2 </code> </summary>

```sql
SELECT i.InvoiceDate, c.firstName, c.lastName, i.Total
FROM Invoice i
JOIN Customer c ON i.CustomerId = c.CustomerId;
```

</details>

<details>

<summary> <code> #3 </code> </summary>

```sql
SELECT c.FirstName, c.LastName, e.FirstName, e.LastName
FROM Customer c
JOIN Employee e ON c.SupportRepId = e.EmployeeId;
```

</details>

<details>

<summary> <code> #4 </code> </summary>

```sql
SELECT al.Title, ar.Name
FROM Album al
JOIN Artist ar ON al.ArtistId = ar.ArtistId;
```

</details>

<details>

<summary> <code> #5 </code> </summary>

```sql
SELECT pt.TrackId
FROM PlaylistTrack pt
JOIN Playlist p ON p.Name = "Music";
```

</details>

<details>

<summary> <code> #6 </code> </summary>

```sql
SELECT t.Name
FROM Track t
JOIN PlaylistTrack pt ON pt.PlaylistId = 5;
```

</details>

<details>

<summary> <code> #7 </code> </summary>

```sql
SELECT t.name, p.Name
FROM Track t
JOIN PlaylistTrack pt ON t.TrackId = pt.TrackId
JOIN Playlist p ON pt.PlaylistId = p.PlaylistId;
```

</details>

<details>

<summary> <code> #8 </code> </summary>

```sql
SELECT t.Name, a.title
FROM Track t
JOIN Album a ON t.AlbumId = a.AlbumId
JOIN Genre g ON g.Name = "Alternative";
```

</details>

</details>

### Black Diamond

* Get all tracks on the playlist(s) called Music and show their name, genre name, album name, and artist name.
  * At least 5 joins.


## Practice nested queries

### Summary

Complete the instructions without using any joins. Only use nested queries to come up with the solution.

### Instructions

<details>

<summary> <code> Syntax Hint </code> </summary>

```sql
SELECT [Column names] 
FROM [Table] 
WHERE ColumnId IN ( SELECT ColumnId FROM [Table2] WHERE [Condition] );

SELECT Name, Email FROM Athlete WHERE AthleteId IN ( SELECT PersonId FROM PieEaters WHERE Flavor='Apple' );
```

</details>

<br />

1. Get all invoices where the `UnitPrice` on the `InvoiceLine` is greater than $0.99.
2. Get all Playlist Tracks where the playlist name is Music.
3. Get all Track names for `playlistId` 5.
4. Get all tracks where the `Genre` is Comedy.
5. Get all tracks where the `Album` is Fireball.
6. Get all tracks for the artist Queen ( 2 nested subqueries ).

### Solution

<details>

<summary> <code> SQL Solutions </code> </summary>

<details>

<summary> <code> #1 </code> </summary>

```sql
SELECT *
FROM Invoice
WHERE InvoiceId IN ( SELECT InvoiceId FROM InvoiceLine WHERE UnitPrice > 0.99 );
```

</details>

<details>

<summary> <code> #2 </code> </summary>

```sql
SELECT *
FROM PlaylistTrack
WHERE PlaylistId = ( SELECT PlaylistId FROM Playlist WHERE Name = "Music" );
```

</details>

<details>

<summary> <code> #3 </code> </summary>

```sql
SELECT Name
FROM Track
WHERE TrackId IN ( SELECT TrackId FROM PlaylistTrack WHERE PlaylistId = 5 );
```

</details>

<details>

<summary> <code> #4 </code> </summary>

```sql
SELECT *
FROM Track
WHERE GenreId IN ( SELECT GenreId FROM Genre WHERE Name = "Comedy" );
```

</details>

<details>

<summary> <code> #5 </code> </summary>

```sql
SELECT *
FROM Track
WHERE AlbumId IN ( SELECT AlbumId FROM Album WHERE Title = "Fireball" );
```

</details>

<details>

<summary> <code> #6 </code> </summary>

```sql
SELECT *
FROM Track
WHERE AlbumId IN ( 
  SELECT AlbumId FROM Album WHERE ArtistId IN ( 
    SELECT ArtistId FROM Artist WHERE Name = "Queen" 
  )
); 
```

</details>

</details>

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

## Contributions

If you see a problem or a typo, please fork, make the necessary changes, and create a pull request so we can review your changes and merge them into the master repo and branch.

## Copyright

© DevMountain LLC, 2017. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://devmounta.in/img/logowhiteblue.png" width="250">
</p>
