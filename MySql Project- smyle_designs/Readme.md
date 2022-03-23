
```sql
SHOW DATABASES;
```
| Database           |
|:-------------------|
| information_schema |
| museum             |
| mysql              |
| performance_schema |
| school             |
| smyle_designs      |
| sys                |
| views              |
###### 8 rows in set (0.00 sec)
```sql
USE smyle_designs;
```
Database changed
```sql
SHOW TABLES;
```
###### Empty set (0.01 sec)
```sql
CREATE TABLE users (user_id TINYINT PRIMARY KEY AUTO_INCREMENT,user_name VARCHAR(20) UNIQUE NOT NULL CHECK(LENGTH(user_name)>=3),mail_id VARCHAR(40) UNIQUE NOT NULL,password VARCHAR(15) NOT NULL);
```
###### Query OK, 0 rows affected (0.06 sec)
```sql
DESC users;
```
| Field     | Type        | Null | Key | Default | Extra          |
|:----------|:------------|:-----|:----|:--------|:---------------|
| user_id   | tinyint     | NO   | PRI | NULL    | auto_increment |
| user_name | varchar(20) | NO   | UNI | NULL    |                |
| mail_id   | varchar(40) | NO   | UNI | NULL    |                |
| password  | varchar(15) | NO   |     | NULL    |                |
###### 4 rows in set (0.00 sec)
```sql
CREATE TABLE personal_info(user_id TINYINT AUTO_INCREMENT ,FOREIGN KEY(user_id) REFERENCES users(user_id),f_name VARCHAR(18) NOT NULL CHECK(LENGTH(f_name)>=3),l_name VARCHAR(18) NOT NULL CHECK(LENGTH(l_name)>=3),occupation
VARCHAR(24) DEFAULT 'unknown',number BIGINT CHECK(LENGTH(number)=10));
```
###### Query OK, 0 rows affected (0.07 sec)
```sql
DESC personal_info;
```
| Field      | Type        | Null | Key | Default | Extra          |
|:-----------|:------------|:-----|:----|:--------|:---------------|
| user_id    | tinyint     | NO   | MUL | NULL    | auto_increment |
| f_name     | varchar(18) | NO   |     | NULL    |                |
| l_name     | varchar(18) | NO   |     | NULL    |                |
| occupation | varchar(24) | YES  |     | unknown |                |
| street     | varchar(35) | NO   |     | NULL    |                |
| state      | varchar(35) | NO   |     | NULL    |                |
| city       | varchar(35) | NO   |     | NULL    |                |
| pin_code   | int         | NO   |     | NULL    |                |
| number     | bigint      | YES  |     | NULL    |                |
###### 9 rows in set (0.00 sec)
```sql
ALTER TABLE personal_info ADD COLUMN street VARCHAR(35) NOT NULL;
```
###### Query OK, 0 rows affected (0.03 sec)
###### Records: 0  Duplicates: 0  Warnings: 0
```sql
ALTER TABLE personal_info ADD COLUMN state VARCHAR(35) NOT NULL;
```
###### Query OK, 0 rows affected (0.03 sec)
###### Records: 0  Duplicates: 0  Warnings: 0
```sql
ALTER TABLE personal_info ADD COLUMN city VARCHAR(35) NOT NULL;
```
###### Query OK, 0 rows affected (0.03 sec)
###### Records: 0  Duplicates: 0  Warnings: 0
```sql
ALTER TABLE personal_info ADD COLUMN pin_code int(10) NOT NULL;
```
###### Query OK, 0 rows affected, 1 warning (0.03 sec)
###### Records: 0  Duplicates: 0  Warnings: 1
```sql
DESC personal_info;
```
| Field      | Type        | Null | Key | Default | Extra          |
|:-----------|:------------|:-----|:----|:--------|:---------------|
| user_id    | tinyint     | NO   | MUL | NULL    | auto_increment |
| f_name     | varchar(18) | NO   |     | NULL    |                |
| l_name     | varchar(18) | NO   |     | NULL    |                |
| occupation | varchar(24) | YES  |     | unknown |                |
| street     | varchar(35) | NO   |     | NULL    |                |
| state      | varchar(35) | NO   |     | NULL    |                |
| city       | varchar(35) | NO   |     | NULL    |                |
| pin_code   | int         | NO   |     | NULL    |                |
###### 8 rows in set (0.00 sec)
```sql
CREATE TABLE designs(design_id TINYINT PRIMARY KEY AUTO_INCREMENT,title VARCHAR(25) NOT NULL,url TEXT NOT NULL,user_id TINYINT,FOREIGN KEY(user_id) REFERENCES users(user_id));
```
###### Query OK, 0 rows affected (0.06 sec)
```sql
DESC designs;
```
| Field     | Type        | Null | Key | Default | Extra          |
|:----------|:------------|:-----|:----|:--------|:---------------|
| design_id | tinyint     | NO   | PRI | NULL    | auto_increment |
| title     | varchar(25) | NO   |     | NULL    |                |
| url       | text        | NO   |     | NULL    |                |
| user_id   | tinyint     | YES  | MUL | NULL    |                |
###### 4 rows in set (0.00 sec)
```sql
CREATE TABLE category_name(category_id TINYINT PRIMARY KEY AUTO_INCREMENT,name VARCHAR(25) NOT NULL UNIQUE);
```
###### Query OK, 0 rows affected (0.05 sec)
```sql
DESC category_name;
```
| Field       | Type        | Null | Key | Default | Extra          |
|:------------|:------------|:-----|:----|:--------|:---------------|
| category_id | tinyint     | NO   | PRI | NULL    | auto_increment |
| name        | varchar(25) | NO   | UNI | NULL    |                |
###### 2 rows in set (0.01 sec)
```sql
CREATE TABLE categories (design_id TINYINT,FOREIGN KEY(design_id) REFERENCES designs(design_id),category_id TINYINT,FOREIGN KEY(category_id) REFERENCES category_name(category_id));
```
###### Query OK, 0 rows affected (0.06 sec)
```sql
DESC categories;
```
| Field       | Type    | Null | Key | Default | Extra |
|:------------|:--------|:-----|:----|:--------|:------|
| design_id   | tinyint | YES  | MUL | NULL    |       |
| category_id | tinyint | YES  | MUL | NULL    |       |
###### 2 rows in set (0.01 sec)
```sql
CREATE TABLE color_name(color_id TINYINT PRIMARY KEY AUTO_INCREMENT,name VARCHAR(15) NOT NULL UNIQUE);
```
###### Query OK, 0 rows affected (0.04 sec)
```sql
DESC color_name;
```
| Field    | Type        | Null | Key | Default | Extra          |
|:---------|:------------|:-----|:----|:--------|:---------------|
| color_id | tinyint     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(15) | NO   | UNI | NULL    |                |
2 rows in set (0.00 sec)
```sql
CREATE TABLE colors(design_id TINYINT,color_id TINYINT,FOREIGN KEY(design_id) REFERENCES designs(design_id),FOREIGN KEY(color_id) REFERENCES color_name(color_id));
```
###### Query OK, 0 rows affected (0.09 sec)
```sql
DESC colors;
```
| Field     | Type    | Null | Key | Default | Extra |
|:----------|:--------|:-----|:----|:--------|:------|
| design_id | tinyint | YES  | MUL | NULL    |       |
| color_id  | tinyint | YES  | MUL | NULL    |       |
###### 2 rows in set (0.00 sec)
```sql
SHOW TABLES;
```
| Tables_in_smyle_designs |
|:------------------------|
| categories              |
| category_name           |
| color_name              |
| colors                  |
| designs                 |
| personal_info           |
| users                   |
###### 7 rows in set (0.00 sec)
```sql
DESC users;
```
| Field     | Type        | Null | Key | Default | Extra          |
|:----------|:------------|:-----|:----|:--------|:---------------|
| user_id   | tinyint     | NO   | PRI | NULL    | auto_increment |
| user_name | varchar(20) | NO   | UNI | NULL    |                |
| mail_id   | varchar(40) | NO   | UNI | NULL    |                |
| password  | varchar(15) | NO   |     | NULL    |                |
###### 4 rows in set (0.00 sec)
```sql
INSERT INTO users VALUES (1,'Rishi','rishijeeva13@gmail.com','rishi@12345');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO users VALUES (2,'ismail','smile12@gmail.com','rishi@12345');
```
###### Query OK, 1 row affected (0.00 sec)
```sql
INSERT INTO users VALUES (3,'sahana','sahana134@gmail.com','sahana@smile');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO users VALUES (4,'santhanu','sanboi44@gmail.com','sanboi@1232');
```
###### Query OK, 1 row affected (0.00 sec)
```sql
UPDATE users SET password = 'smyle@2323' WHERE user_id = 2;
```
###### Query OK, 1 row affected (0.01 sec)
###### Rows matched: 1  Changed: 1  Warnings: 0
```sql
DESC personal_info;
```
| Field      | Type        | Null | Key | Default | Extra          |
|:-----------|:------------|:-----|:----|:--------|:---------------|
| user_id    | tinyint     | NO   | MUL | NULL    | auto_increment |
| f_name     | varchar(18) | NO   |     | NULL    |                |
| l_name     | varchar(18) | NO   |     | NULL    |                |
| occupation | varchar(24) | YES  |     | unknown |                |
| street     | varchar(35) | NO   |     | NULL    |                |
| state      | varchar(35) | NO   |     | NULL    |                |
| city       | varchar(35) | NO   |     | NULL    |                |
| pin_code   | int         | NO   |     | NULL    |                |
| number     | bigint      | YES  |     | NULL    |                |
###### 9 rows in set (0.01 sec)
```sql
INSERT INTO personal_info VALUES (1,'Rishi','Atgondan','Developer','Kangayem','Tamil_nadu','Tirupur',641604,6381950080);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO personal_info VALUES (2,'Ismal','Mohamed','Designer','Kayalpattinam','Tamil_nadu','Tuticorin',628204,6374563950);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO personal_info VALUES (3,'Sahana','Aisha','Tester','Kayalpattinam','Tamil_nadu','Tuticorin',628204,7687898769);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO personal_info VALUES (4,'Santhanu','sanboi','Developer','Rathinam_nagar','Tamil_nadu','Theni',625531,8870522547);
```
###### Query OK, 1 row affected (0.00 sec)
```sql
SELECT * FROM users;
```
| user_id | user_name | mail_id                | password     |
|:--------|:----------|:-----------------------|:-------------|
|       1 | Rishi     | rishijeeva13@gmail.com | rishi@12345  |
|       2 | ismail    | smile12@gmail.com      | smyle@2323   |
|       3 | sahana    | sahana134@gmail.com    | sahana@smile |
|       4 | santhanu  | sanboi44@gmail.com     | sanboi@1232  |
###### 4 rows in set (0.00 sec)
```sql
SELECT * FROM personal_info;
```
| user_id | f_name   | l_name   | occupation | street         | state      | city      | pin_code | number     |
|:--------|:---------|:---------|:-----------|:---------------|:-----------|:----------|:---------|:-----------|
|       1 | Rishi    | Atgondan | Developer  | Kangayem       | Tamil_nadu | Tirupur   |   641604 | 6381950080 |
|       2 | Ismal    | Mohamed  | Designer   | Kayalpattinam  | Tamil_nadu | Tuticorin |   628204 | 6374563950 |
|       3 | Sahana   | Aisha    | Tester     | Kayalpattinam  | Tamil_nadu | Tuticorin |   628204 | 7687898769 |
|       4 | Santhanu | sanboi   | Developer  | Rathinam_nagar | Tamil_nadu | Theni     |   625531 | 8870522547 |
###### 4 rows in set (0.00 sec)

```sql
DESC category_name;
```
| Field       | Type        | Null | Key | Default | Extra          |
|:------------|:------------|:-----|:----|:--------|:---------------|
| category_id | tinyint     | NO   | PRI | NULL    | auto_increment |
| name        | varchar(25) | NO   | UNI | NULL    |                |
###### 2 rows in set (0.01 sec)
```sql
INSERT INTO category_name VALUES (1,'Logo_design');
```
###### Query OK, 1 row affected (0.00 sec)
```sql
INSERT INTO category_name VALUES (2,'Poster_design');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO category_name VALUES (3,'UI_design');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
SELECT * FROM category_name;
```
| category_id | name          |
|:------------|:--------------|
|           1 | Logo_design   |
|           2 | Poster_design |
|           3 | UI_design     |
###### 3 rows in set (0.00 sec)
```sql
DESC designs;
```
| Field     | Type        | Null | Key | Default | Extra          |
|:----------|:------------|:-----|:----|:--------|:---------------|
| design_id | tinyint     | NO   | PRI | NULL    | auto_increment |
| title     | varchar(25) | NO   |     | NULL    |                |
| url       | text        | NO   |     | NULL    |                |
| user_id   | tinyint     | YES  | MUL | NULL    |                |
###### 4 rows in set (0.00 sec)
```sql
INSERT INTO designs VALUES (1,'Ten_dots','https://mir-s3-cdn-cf.behance.net/project_modules/fs/0f1ca6137637039.620e780f15a37.jpg ',1);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO designs VALUES (2,'Read_with_india','https://mir-s3-cdn-cf.behance.net/project_modules/1400_opt_1/8c0bb9137815551.62121eec740b6.png',2);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO designs VALUES (3,'Seven_pounds','https://mir-s3-cdn-cf.behance.net/project_modules/fs/6552b9137817617.621228e36cd2b.jpg',3);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO designs VALUES (4,'Wishes','https://mir-s3-cdn-cf.behance.net/project_modules/1400_opt_1/bfde9e126001639.612ca7e622378.png',4);
```
###### Query OK, 1 row affected (0.00 sec)
```sql
SELECT * FROM designs;
```
| design_id | title           | url                                                                                            | user_id |
|:----------|:----------------|:-----------------------------------------------------------------------------------------------|:--------|
|         1 | Ten_dots        | https://mir-s3-cdn-cf.behance.net/project_modules/fs/0f1ca6137637039.620e780f15a37.jpg         |       1 |
|         2 | Read_with_india | https://mir-s3-cdn-cf.behance.net/project_modules/1400_opt_1/8c0bb9137815551.62121eec740b6.png |       2 |
|         3 | Seven_pounds    | https://mir-s3-cdn-cf.behance.net/project_modules/fs/6552b9137817617.621228e36cd2b.jpg         |       3 |
|         4 | Wishes          | https://mir-s3-cdn-cf.behance.net/project_modules/1400_opt_1/bfde9e126001639.612ca7e622378.png |       4 |
###### 4 rows in set (0.00 sec)
```sql
DESC color_name;
```
| Field    | Type        | Null | Key | Default | Extra          |
|:---------|:------------|:-----|:----|:--------|:---------------|
| color_id | tinyint     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(15) | NO   | UNI | NULL    |                |
###### 2 rows in set (0.00 sec)
```sql
INSERT INTO color_name VALUES (1,'red');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO color_name VALUES (2,'black');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO color_name VALUES (3,'blue');
```
###### Query OK, 1 row affected (0.00 sec)
```sql
INSERT INTO color_name VALUES (4,'brown');
```
###### Query OK, 1 row affected (0.01 sec)
```sql
SELECT * FROM color_name;
```
| color_id | name  |
|:---------|:------|
|        2 | black |
|        3 | blue  |
|        4 | brown |
|        1 | red   |
###### 4 rows in set (0.00 sec)
```sql
DESC colors;
```
| Field     | Type    | Null | Key | Default | Extra |
|:----------|:--------|:-----|:----|:--------|:------|
| design_id | tinyint | YES  | MUL | NULL    |       |
| color_id  | tinyint | YES  | MUL | NULL    |       |
###### 2 rows in set (0.00 sec)
```sql
INSERT INTO colors VALUES (1,1);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
TRUNCATE colors;
```
###### Query OK, 0 rows affected (0.08 sec)
```sql
INSERT INTO colors VALUES (1,2);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO colors VALUES (2,3);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO colors VALUES (3,2);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO colors VALUES (4,1);
```
###### Query OK, 1 row affected (0.00 sec)
```sql
SELECT * FROM colors;
```
| design_id | color_id |
|:----------|:---------|
|         1 |        2 |
|         2 |        3 |
|         3 |        2 |
|         4 |        1 |
###### 4 rows in set (0.00 sec)
```sql
DESC categories;
```
| Field       | Type    | Null | Key | Default | Extra |
|:------------|:--------|:-----|:----|:--------|:------|
| design_id   | tinyint | YES  | MUL | NULL    |       |
| category_id | tinyint | YES  | MUL | NULL    |       |

###### 2 rows in set (0.01 sec)
```sql
INSERT INTO categories VALUES (1,1);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO categories VALUES (2,1);
```
###### Query OK, 1 row affected (0.02 sec)
```sql
INSERT INTO categories VALUES (3,2);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
INSERT INTO categories VALUES (4,3);
```
###### Query OK, 1 row affected (0.01 sec)
```sql
SELECT * FROM categories ;
```
| design_id | category_id |
|:----------|:------------|
|         1 |           1 |
|         2 |           1 |
|         3 |           2 |
|         4 |           3 |
###### 4 rows in set (0.00 sec)

## ER Model

![ER SMYLE_DESIGNS](https://user-images.githubusercontent.com/93571043/159666425-71c08bd9-c281-4ae2-b573-a1ea53a5c415.png)


## EER Model

![Screenshot from 2022-03-23 15-00-01](https://user-images.githubusercontent.com/93571043/159667622-2dfc57e9-5068-4379-b43a-de78600473b8.png)


