
PART 1 -------------------------------------------

1. Select the names of all users.

    fringe_shows=# SELECT name from users;
    name       
    ------------------
    Rick Henri
    Jay Chetty
    Keith Douglas
    Callum Dougan
    Andrew Insley
    Daniel Gillespie
    Bethany Fraser
    Nick Ridell
    Evelyn Utterson
    Sky Su
    Nicholas Hill
    Michael McLeod
    Callum Hogg
    Chris Sloan
    Gary Carmichael
    Oscar Brooks
    Ross Galloway
    Paul MacLean
    Stuart Ramsay
    Peter Forbes
    Euan Walls
    Aine Dunphy
    (22 rows)



2. Select the names of all shows that cost less than £15.

    fringe_shows=# SELECT name from shows where price < 15.00;
    name             
    ------------------------------
    Le Haggis
    Paul Dabek Mischief 
    Best of Burlesque
    Two become One
    Urinetown
    Two girls, one cup of comedy
    (6 rows)


3. Insert a user with the name "Val Gibson" into the users table.

    fringe_shows=# INSERT into users (name) VALUES ('Valerie Gibson');
    INSERT 0 1
    fringe_shows=# SELECT * from users;

        id |       name       
        ----+------------------
        1 | Rick Henri
        2 | Jay Chetty
        3 | Keith Douglas
        4 | Callum Dougan
        5 | Andrew Insley
        6 | Daniel Gillespie
        7 | Bethany Fraser
        8 | Nick Ridell
        9 | Evelyn Utterson
        10 | Sky Su
        11 | Nicholas Hill
        12 | Michael McLeod
        13 | Callum Hogg
        14 | Chris Sloan
        15 | Gary Carmichael
        16 | Oscar Brooks
        17 | Ross Galloway
        18 | Paul MacLean
        19 | Stuart Ramsay
        20 | Peter Forbes
        21 | Euan Walls
        22 | Aine Dunphy
        23 | Valerie Gibson
        (23 rows)


4. Select the id of the user with your name.

    fringe_shows=# SELECT id from users where name = 'Andrew Insley';
    id 
    ----
    5
    (1 row)

5. Insert a record that Val Gibson wants to attend the show "Two girls, one cup of comedy".

    fringe_shows=# INSERT into shows_users (show_id, user_id) VALUES (12, 23);
    INSERT 0 1


6. Updates the name of the "Val Gibson" user to be "Valerie Gibson".
    
    fringe_shows=# UPDATE users SET name = 'Val Gibson' where name = 'Valerie Gibson';
    UPDATE 1


7. Deletes the user with the name 'Valerie Gibson'.

    fringe_shows=# DELETE from users WHERE name = 'Val Gibson';
    DELETE 1

    id |       name       
    ----+------------------
    1 | Rick Henri
    2 | Jay Chetty
    3 | Keith Douglas
    4 | Callum Dougan
    5 | Andrew Insley
    6 | Daniel Gillespie
    7 | Bethany Fraser
    8 | Nick Ridell
    9 | Evelyn Utterson
    10 | Sky Su
    11 | Nicholas Hill
    12 | Michael McLeod
    13 | Callum Hogg
    14 | Chris Sloan
    15 | Gary Carmichael
    16 | Oscar Brooks
    17 | Ross Galloway
    18 | Paul MacLean
    19 | Stuart Ramsay
    20 | Peter Forbes
    21 | Euan Walls
    22 | Aine Dunphy
    (22 rows)

8. Deletes the shows for the user you just deleted.

    fringe_shows=# DELETE from shows_users WHERE user_id = 23;
    DELETE 1

SECTION 2-------------------------------------------------------------------------------

This section involves more complex queries. You will need to go and find out about aggregate funcions in SQL to answer some of the next questions.

1. Select the names and prices of all shows, ordered by price in ascending order.

    fringe_shows=# SELECT name, price FROM shows ORDER BY price;
    name                    | price 
    -------------------------------------------+-------
    Two girls, one cup of comedy              |  6.00
    Best of Burlesque                         |  7.99
    Two become One                            |  8.50
    Urinetown                                 |  8.50
    Paul Dabek Mischief                       | 12.99
    Le Haggis                                 | 12.99
    Joe Stilgoe: Songs on Film â€“ The Sequel | 16.50
    Game of Thrones - The Musical             | 16.50
    Shitfaced Shakespeare                     | 16.50
    Aaabeduation â€“ A Magic Show             | 17.99
    Camille O'Sullivan                        | 17.99
    Balletronics                              | 32.00
    Edinburgh Royal Tattoo                    | 32.99
    (13 rows)


2. Select the average price of all shows.

    fringe_shows=# SELECT AVG(price) FROM shows;
    avg         
    ---------------------
    15.9569230769230769
    (1 row)



4. Select the price of the least expensive show.

    fringe_shows=# SELECT MIN(price) FROM shows;
    min  
    ------
    6.00
    (1 row)


5. Select the sum of the price of all shows.

    fringe_shows=# SELECT SUM(price) AS TotalPrice FROM shows;
    totalprice 
    ------------
    207.44
    (1 row)

6. Select the sum of the price of all shows whose prices is less than £20.

    fringe_shows=# SELECT SUM(price) AS TotalPrice FROM shows WHERE price > 20.0;
    totalprice 
    ------------
    64.99
    (1 row)


7. Select the name and price of the most expensive show.

    fringe_shows=# SELECT name, price FROM shows WHERE price = (SELECT MAX(price) FROM shows); 
    name          | price 
    ------------------------+-------
    Edinburgh Royal Tattoo | 32.99
    (1 row)


8. Select the name and price of the second from cheapest show.

    fringe_shows=# SELECT name, price  FROM shows ORDER BY price LIMIT 1 OFFSET 1;
    name        | price 
    -------------------+-------
    Best of Burlesque |  7.99
    (1 row)


9. Select the names of all users whose names start with the letter "N".

    fringe_shows=# SELECT * FROM users where name like 'N%';
    id |     name      
    ----+---------------
    8 | Nick Ridell
    11 | Nicholas Hill
    (2 rows)


10. Select the names of users whose names contain "mi".

    fringe_shows=# SELECT * FROM users where name like '%mi%';
    id |      name       
    ----+-----------------
    15 | Gary Carmichael
    (1 row)

    fringe_shows=# SELECT * FROM users where name like '%mi%' or name like '%Mi%';
    id |      name       
    ----+-----------------
    12 | Michael McLeod
    15 | Gary Carmichael
    (2 rows)


SECTION 3-------------------------------------------------------------------------------------------------

The following questions can be answered by using nested SQL statements but ideally you should learn about JOIN clauses to answer them.

1. Select the time for the Edinburgh Royal Tattoo.

    fringe_shows=# SELECT time FROM times INNER JOIN shows ON times.show_id = shows.id WHERE shows.name = 'Edinburgh Royal Tattoo';
    time  
    -------
    22:00
    (1 row)


2. Select the number of users who want to see "Shitfaced Shakespeare".

    fringe_shows=# SELECT COUNT(user_id) FROM shows_users INNER JOIN shows ON shows_users.show_id = shows.id WHERE shows.name = 'Shitfaced Shakespeare';
    count 
    -------
    7
    (1 row)

3. Select all of the user names and the count of shows they're going to see.
O
    fringe_shows=# SELECT name, COUNT(shows_users.show_id) FROM users INNER JOIN shows_users ON users.id = shows_users.user_id GROUP BY users.id;
    name       | count 
    ------------------+-------
    Nick Ridell      |     5
    Nicholas Hill    |     5
    Oscar Brooks     |     4
    Keith Douglas    |     6
    Chris Sloan      |     4
    Ross Galloway    |     5
    Gary Carmichael  |     4
    Callum Dougan    |     4
    Michael McLeod   |     6
    Rick Henri       |     5
    Sky Su           |     5
    Callum Hogg      |     4
    Evelyn Utterson  |     7
    Daniel Gillespie |     4
    Jay Chetty       |     5
    Andrew Insley    |     4
    Bethany Fraser   |     4
    (17 rows)



4. SELECT all users who are going to a show at 17:15.

    fringe_shows=# SELECT users.name, shows.name, times.time FROM users INNER JOIN shows_users ON users.id = shows_users.user_id INNER JOIN times ON shows_users.show_id = times.show_id INNER JOIN shows ON shows.id = shows_users.show_id WHERE times.time = '17:15';
    name       |                   name                    | time  
    -----------------+-------------------------------------------+-------
    Rick Henri      | Camille O'Sullivan                        | 17:15
    Keith Douglas   | Camille O'Sullivan                        | 17:15
    Andrew Insley   | Camille O'Sullivan                        | 17:15
    Nick Ridell     | Camille O'Sullivan                        | 17:15
    Evelyn Utterson | Camille O'Sullivan                        | 17:15
    Callum Hogg     | Camille O'Sullivan                        | 17:15
    Gary Carmichael | Camille O'Sullivan                        | 17:15
    Nicholas Hill   | Joe Stilgoe: Songs on Film â€“ The Sequel | 17:15
    Michael McLeod  | Joe Stilgoe: Songs on Film â€“ The Sequel | 17:15
    Callum Hogg     | Joe Stilgoe: Songs on Film â€“ The Sequel | 17:15
    Oscar Brooks    | Joe Stilgoe: Songs on Film â€“ The Sequel | 17:15
    Ross Galloway   | Joe Stilgoe: Songs on Film â€“ The Sequel | 17:15
    (12 rows)












































