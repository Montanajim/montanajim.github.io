# Single File Queries





```mysql
Show databases;

use zdbNation;

show tables;

-- Select * from countries;

Select name from countries;

Select name 
From countries 
Where name like 'Canada';

Select name
From countries
Where name like 'C%';

Select name
From countries
Where name like '%a';

Select name as i3 
From countries 
Where name like '__i%';

Select name as uni
From countries 
Where name like 'Uni%';

Select name
From countries
Where name like '%ani%';

Select name as ani_countries 
From countries
Where name like '%ani%';

Select count(name) as ani_countries 
From countries
Where name like '%ani%';

Describe countries;

Select sum(area) as total_area
From countries;

Select max(area) as max_area
From countries;

Select min(area) as min_area
From countries;

Select avg(area) as avg_area
From countries;

Select std(area) as std_area
From countries;

Select name 
from countries
limit 10;

Select name, national_day
from countries
Where national_day is null;

Select name, region_id 
from  countries 
limit 50;

Select region_id, count(region_id) as theCount, sum(area) as totalArea 
from  countries 
group by region_id
order by totalArea desc;

Select region_id, count(region_id) as theCount, sum(area) as totalArea 
from  countries 
group by region_id
order by totalArea desc;

Select name, region_id,  area as totalArea 
from  countries 
where area < 20000 and name like 'S%' 
order by name asc;



CREATE OR REPLACE TABLE student (name CHAR(10), test CHAR(10), score TINYINT); 

INSERT INTO student VALUES 
  ('Charlie', 'SQL', 75), ('Charlie', 'Tuning', 73), 
  ('Elizabeth', 'SQL', 43), ('Elizabeth', 'Tuning', 31), 
  ('Katy', 'SQL', 56), ('Katy', 'Tuning', 88), 
  ('Tom', 'SQL', 87), ('Tom', 'Tuning', 83),
  ('Jim','SQL',90);

SELECT COUNT(*) FROM student;


SELECT  COUNT(DISTINCT (name)) FROM student;

SELECT  COUNT(DISTINCT (test)) FROM student;

SELECT  name, test, score
FROM student 
WHERE score > 80;


```

