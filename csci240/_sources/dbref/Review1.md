# Review Session A



```mysql
/*
David Doge
Donald Dryus
Debbie Dingle

Bubba Baker
Brian Brown
Belinda Booey

Doge
    Brown Collie Bella
    Redd  Collie Luna

Dryus
    Grey Hound Max
    Red  Mutt  Buddy

Dingle
    Red  Spaniel Daisy


Orphans
   Brown Shepard Wolfy
   Red   Sitter  Wiskey
   Blue  Aussie  Windle
   Grey  Mutt    Winnie


Shot A
   Bella, Luna, Daisy, Wolfy, Windle

Shot B 
   Luna, Buddy, Wolfy, Wiskey

*/



drop  database if exists  zdbinclass425;

create or replace database zdbinclass425;

commit;

use zdbinclass425;


-- drop database zdbzdbinclass425

drop table if exists tbl_person;

CREATE OR REPLACE TABLE tbl_person(
    fname VARCHAR(255),
    lname VARCHAR(255),
    person_id int(9) NOT NULL AUTO_INCREMENT PRIMARY KEY
    -- ON DELETE CASCADE
);


CREATE OR REPLACE TABLE tbl_dog(
    dogname VARCHAR(255),
    dogbreed VARCHAR(255),
    dogcolor VARCHAR(255),
    person_id int(9),
    dog_id int(9) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    CONSTRAINT dogperson_fk FOREIGN KEY(person_id )
        REFERENCES tbl_person(person_id)
    ON DELETE CASCADE

    );

CREATE OR REPLACE TABLE tbl_vac(
    shotname VARCHAR(255),
    dog_id int(9),
    vac_id int(9) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    CONSTRAINT vacdog_fk FOREIGN KEY(dog_id )
        REFERENCES tbl_dog(dog_id)
    ON DELETE CASCADE

);

INSERT INTO tbl_person(fname,lname,person_id)
    VALUES 
        ('David','Doge',1),
        ('Donald','Dryfus',2),
        ('Debbie','Dingle',3),
        ('Bubba','Baker',4),
        ('Brian','Brown',5),
        ('Belinda','Booey',6);

INSERT INTO tbl_dog(dogname,dogbreed,dogcolor,person_id,dog_id)
    VALUES 
        ('Bella','Collie','Brown',1,1),
        ('Luna','Collie','Red',1,2),
        ('Max','Hound','Grey',2,3),
        ('Buddy','Mutt','Red',2,4),
        ('Daisy','Spaniel','Red',3,5),
        ('Wolfy','Shepard','Brown',NULL,6),
        ('Wiskey','Sitter','Red',NULL,7),
        ('Windel','Aussie','Blue',NULL,8),
        ('Winford','Mutt','Grey',NULL,9);

INSERT INTO tbl_vac(shotname,dog_id)
    VALUES 
        ("SHOT A", 1),
        ("SHOT A", 2),
        ("SHOT A", 5),
        ("SHOT A", 6),
        ("SHOT A", 8),
        ("SHOT B", 2),
        ("SHOT B", 4),
        ("SHOT B", 6),
        ("SHOT B", 7);
        
-- how many people own dogs
SELECT  count(distinct person_id)
FROM tbl_dog;

SELECT count(distinct tbl_person.person_id) as numDogOwners
FROM tbl_person Inner Join tbl_dog
    on tbl_person.person_id = tbl_dog.person_id;

-- how many dogs have no owners
SELECT count(dog_id) as noOwners
FROM tbl_dog
WHERE person_id IS NULL;

-- how many dogs do each person has?
SELECT lname, count(dog_id) as numDogs
FROM tbl_person LEFT JOIN tbl_dog 
    ON tbl_person.person_id = tbl_dog.person_id
GROUP BY lname
Order BY lname;

-- how many dogs do each person has who are only dog owners?
SELECT lname, count(dog_id) as numDogs
FROM tbl_person JOIN tbl_dog 
    ON tbl_person.person_id = tbl_dog.person_id
GROUP BY lname
Order BY lname;

-- how many dogs do each person has who are only dog owners and
-- have more than one dog
SELECT lname, count(dog_id) as numDogs
FROM tbl_person JOIN tbl_dog 
    ON tbl_person.person_id = tbl_dog.person_id
GROUP BY lname
Having numDogs > 1
Order BY lname;


-- All people who start with the letter 'D'
SELECT Fname, lname
FROM tbl_person
WHERE Fname LIKE "D%";

-- Last name with last names of only 4 characters
SELECT Fname, lname
FROM tbl_person
WHERE lname LIKE "____";

-- Want all of the dogs with the second letter 
-- of dog name being the letter 'i' and include
-- the owner first and last name

SELECT fname, lname, dogname
FROM  tbl_dog LEFT JOIN tbl_person
        on tbl_dog.person_id = tbl_person.person_id
WHERE dogname LIKE "_i%";

-- and also the dognames that end with the letter 'y'
SELECT fname, lname, dogname
FROM  tbl_dog LEFT JOIN tbl_person
        on tbl_dog.person_id = tbl_person.person_id
WHERE dogname LIKE '_i%' OR dogname LIKE '%Y'; 

-- Count the dogs by color
SELECT dogcolor, count(dogcolor)
FROM  tbl_dog
GROUP BY dogcolor;

describe tbl_dog;

-- Add a value into a table
INSERT INTO tbl_dog(dogname,dogbreed,dogcolor,person_id)
    VALUE ('Dodger','Spaniel','Red', 2 );


-- Count the dogs by color and breed
SELECT dogcolor,dogbreed, count(dogcolor), count(dogbreed)
FROM  tbl_dog
GROUP BY dogcolor, dogbreed;

SELECT dogcolor,dogbreed
FROM  tbl_dog
GROUP BY dogcolor, dogbreed;

SELECT dogbreed, dogcolor, count(dogcolor), count(dogbreed)
FROM  tbl_dog
GROUP BY dogbreed,dogcolor;

SELECT dogbreed, dogcolor
FROM  tbl_dog
GROUP BY dogbreed,dogcolor;


-- never do this in real life
SELECT * 
FROM tbl_dog join tbl_person;


-- Delete a record
Delete FROM tbl_dog
Where dogname LIKE 'Dodger';


SELECT *
FROM tbl_dog;


SELECT dogcolor,dogbreed
FROM  tbl_dog
GROUP BY dogcolor, dogbreed
HAVING dogcolor LIKE 'Red';

-- change a value of record
UPDATE  tbl_dog
    SET dogbreed = "Mutt", dogname = "Dilly"
    WHERE dog_id = 5;

SELECT *
FROM tbl_dog;

-- How many dogs have vacinations
SELECT count(vac_id)
FROM tbl_vac;

-- Which dogs have vacinations
SELECT dogname
FROM tbl_dog INNER JOIN tbl_vac
    ON tbl_dog.dog_id = tbl_vac.dog_id;

-- To remove duplicates use distinct
SELECT DISTINCT dogname
FROM tbl_dog INNER JOIN tbl_vac
    ON tbl_dog.dog_id = tbl_vac.dog_id;

-- What dogs do not have vacinations?
SELECT dogname, shotname
FROM tbl_dog LEFT JOIN tbl_vac
    on tbl_dog.dog_id = tbl_vac.dog_id
WHERE shotname IS NULL;

-- List the dog owner fname, lname and dogname
-- for the dogs that have no vacinations

SELECT concat(fname," ",lname) as name, dogname, shotname
FROM tbl_dog LEFT JOIN tbl_vac
        on tbl_dog.dog_id = tbl_vac.dog_id
    Left Join tbl_person
        on tbl_person.person_id = tbl_dog.person_id
Where shotname is null;


-- List the dog owners who have dogs that 
-- are not vacinated
SELECT concat(fname," ",lname) as name, dogname, shotname
FROM (tbl_dog LEFT JOIN tbl_vac
        on tbl_dog.dog_id = tbl_vac.dog_id)
    Inner Join tbl_person
        on tbl_person.person_id = tbl_dog.person_id
Where shotname is null;

SELECT concat(fname," ",lname) as name, dogname, shotname
FROM (tbl_vac RIGHT JOIN tbl_dog
        on tbl_dog.dog_id = tbl_vac.dog_id)
    Inner Join tbl_person
        on tbl_person.person_id = tbl_dog.person_id
Where shotname is null;
```

