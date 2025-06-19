# bloor-survey-data
The file `bloor.sql` is a `mysqldump` of the database behind
https://mjo.osborne.economics.utoronto.ca/index.php/bloor/

This database consists of the results of my surveys of the businesses on Bloor Street, Toronto, between Spadina and Lansdowne, since 1995 augmented by similar data from city directories prior to 1995.

The database consists of the following tables:
```
+-------------------------+
| bloor_businesses        |
| bloor_categories        |
| bloor_directories       |
| bloor_ethnicities       |
| bloor_locations         |
| bloor_observation_types |
| bloor_observations      |
| bloor_streets           |
| bloor_subtypes          |
| bloor_surveys           |
| bloor_types             |
+-------------------------+
```

The table `bloor_observations` has the following structure:
```
+----------------+--------------+------+-----+---------+----------------+
| Field          | Type         | Null | Key | Default | Extra          |
+----------------+--------------+------+-----+---------+----------------+
| observation_id | mediumint(5) | NO   | PRI | NULL    | auto_increment |
| survey_id      | mediumint(5) | YES  | MUL | NULL    |                |
| directory_id   | mediumint(9) | YES  | MUL | NULL    |                |
| location_id    | mediumint(5) | YES  | MUL | NULL    |                |
| business_id    | mediumint(5) | YES  | MUL | NULL    |                |
| category_id    | bigint(20)   | YES  | MUL | NULL    |                |
| ethnicity_id   | smallint(6)  | YES  | MUL | NULL    |                |
| observed_name  | varchar(100) | YES  |     | NULL    |                |
| remark         | varchar(255) | YES  |     | NULL    |                |
| website        | varchar(255) | YES  |     | NULL    |                |
+----------------+--------------+------+-----+---------+----------------+
```
