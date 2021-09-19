# Publications-database
Many to one cardinality

## Explanation

### Database constraints

One Publication can belong to one Composer, one Composer can have multiple Publications. One Publication can belong only to one Publisher and one Publisher can have multiple Publications. 

### Entity Relationship Diagram ( ERD )

### SQL scripts

CREATE TABLE composers( 
composer_id VARCHAR(10), 
composer_name VARCHAR(25) NOT NULL, 
PRIMARY KEY(composer_id)); 

INSERT INTO 
composers 
VALUES 
('A1','Aarons'), 
('A2','Abel'), 
('A3','Abdey');

CREATE TABLE publishers( 
publisher_id VARCHAR(10), 
publisher_name VARCHAR(25), 
PRIMARY KEY(publisher_id)); 

INSERT INTO 
publishers 
VALUES 
('C1','Witmark'), 
('C2','Printed for the author'), 
('C3','Shapiro');

CREATE TABLE publications( 
publication_id VARCHAR(10), 
publication_name VARCHAR(25) NOT NULL, 
publication_date INT(10), 
composer_id VARCHAR(10), 
publisher_id VARCHAR(10), 
PRIMARY KEY (publication_id), 
FOREIGN KEY (composer_id) REFERENCES composer(composer_id), 
FOREIGN KEY (publisher_id) REFERENCES publisher(publisher_id));

INSERT INTO 
publications 
VALUES 
('B1','A China Doll',1904,'A1','C1'), 
('B2','Six simphonies',1780,'A2','C2'), 
('B3','Pam the wonder',1908,'A3','C3'); 

Note: The script below runs the query to see who is the composer and publisher of publications.

SELECT composer_name,publication_name,publication_date,publisher_name 
FROM composers,publications,publishers 
WHERE 
composers.composer_id=publications.composer_id 
AND 
publishers.publisher_id=publications.publisher_id;
