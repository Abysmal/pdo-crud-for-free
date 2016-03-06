# pdo-crud-for-free
Classes to provide MySQL PDO CRUD methods 'magically' via a simple subclassing

Some classes to make it *really* easy to do PDO DB CRUD
as long as you follow a few basic (common practice) assumptions

## ASSUMPTION 1: lowerCamelCase - DB table column names matching PHP Class properties
This tool assumes your database table column names, and their corresponding PHP private class properties are named consistently in 'lowerCamelCase'
e.g.

    id
    title
    category
    price

## ASSUMPTION 2: lower case plural DB table name mapping to upper case singular PHP class name
If you have a DB table 'products' this will correspond to a PHP class 'Product'

table names are named lower case, are and plural, e.g 

    users

PHP class names are named with a capital first letter, and are singular, e.g. 

    User

## ASSUMPTION 3: no constructor for your PHP classes
due to the nature of PDO populating properties of objects when DB rows are converted into object instances
do not have a constructor for the PHP classes that correspond to your DB tables

so you'd create a new object, and use the objects public 'setter' methods
e.g.

    $p = new Product();
    $p->setDescription('hammer');
    $p->setPrice(9.99);
    etc.

## step 1: create your DB tables
e.g. create your tables (with integer 'id' field, primary key, auto-increment)

e.g. SQL table to store DVD data

    id:int (primary key, autoincrement)
    title:text
    category:text
    price:float

## step 2: create a corresponding PHP class, and subclass from Mattsmithdev\DatabaseTable
e.g.

    <?php
    namespace Whatever;
    
    use Mattsmithdev\DatabaseTable;
    
        class Dvd extends DatabaseTable
        {
            private $id;
            private $title;
            private $category;
            private $price;
            
            // and public getters and setters ...
            
## step 3: now use the 'magically appearing' static DB CRUD methods

e.g. to get an array of all dvd records from table 'dvds' just write:

    $dvds = Dvd::getAll();
    

## ::getAll()
this method returns an array of objects for eac row of the corresponding DB table
e.g.

    // array of Dvd objects, populated from database table 'dvds'
    $dvds = Dvd::getAll();

## ::getOneById($id)
this method returns an array of objects for eac row of the corresponding DB table
e.g.

    // one Dvd object (or 'null'), populated by row in database table 'dvds' with id=27
    $dvds = Dvd::getOneById(27);

## ::delete($id)
this method deletes the record corresponding to the given 'id'
returns true/false depending on success of the deletion
e.g.

    // delete row in database table 'dvds' with id=12
    $deleteSuccess = Dvd::delete(12);
    
## ::insert($dvd)
this method adds a new row to the database, based on the contents of the provided object
(any 'id' in this object is ignored, since the table is auto-increment, so it's left to the DB to assign a new, unique 'id' for new records)
returns the 'id' of the new record (or -1 if error when inserting)
e.g.

    // delete row in database table 'dvds' with id=12
    $dvd = new Dvd();
    $dvd->setTitle('Jaws II');
    $dvd->setCategory('thriller');
    $dvd->setPrice(9.99);
    
    // create the new Dvd row
    $id = Dvd::insert($dvd);
    
    // decision based on success/failure of insert
    if ($id < 0){
        // error action
    } else {
        // success action
    }
    
    
## ::update($dvd)
this method adds a UPDATES an existing row in the database, based on the contents of the provided object
returns true/false depending on success of the deletion

e.g.

    // update DB record for object 'dvd'
    $updateSuccess = Dvd:update($dvd);
    
            
## ::searchByColumn($columnName, $searchText))
perform an SQL '%' wildcard search on the given column with the given search text
returns an array of objects that match an SQL 'LIKE' query 

e.g.

    // get all Dvds with 'jaws' in the title
    $jawsDvds = Dvd::searchByColumn('title', 'jaws');


have fun!

.. matt ..

