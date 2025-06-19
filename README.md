# bloor-survey-data
The file `bloor.sql` is a `mysqldump` of the database behind
https://mjo.osborne.economics.utoronto.ca/index.php/bloor/

This database consists of the results of my surveys of the businesses on Bloor Street, Toronto, between Spadina and Lansdowne, since 1995 augmented by similar data from city directories prior to 1995.  The page
https://mjo.osborne.economics.utoronto.ca/index.php/bloor/bloorData
describes the data in detail.

The database consists of the following tables:
```+-------------------------+
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
```+----------------+--------------+------+-----+---------+----------------+
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

Observations that come from my surveys have non-null `survey_id`s and observations that come from the directories have non-null `directory_id`s.

The table `bloor_surveys` gives the dates I conducted the surveys and has a flag (`current`) indicating whether the survey is the latest one I have conducted.
```+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| survey_id  | mediumint(5) | NO   | PRI | NULL    | auto_increment |
| year       | char(4)      | YES  |     | NULL    |                |
| start_date | date         | YES  |     | NULL    |                |
| end_date   | date         | YES  |     | NULL    |                |
| current    | char(1)      | YES  |     | NULL    |                |
| note       | varchar(255) | YES  |     | NULL    |                |
+------------+--------------+------+-----+---------+----------------+
```

The table `bloor_directories` gives the details of the directories (scans of which are available from the Toronto Public Library, on the page https://www.torontopubliclibrary.ca/history-genealogy/lh-digital-city-directories.jsp).
```+---------------------------+--------------+------+-----+---------+----------------+
| Field                     | Type         | Null | Key | Default | Extra          |
+---------------------------+--------------+------+-----+---------+----------------+
| directory_id              | mediumint(5) | NO   | PRI | NULL    | auto_increment |
| year                      | smallint(6)  | YES  |     | NULL    |                |
| title                     | varchar(255) | YES  |     | NULL    |                |
| publisher                 | varchar(255) | YES  |     | NULL    |                |
| bloor_spadina_page_number | smallint(6)  | YES  |     | NULL    |                |
| note                      | varchar(255) | YES  |     | NULL    |                |
+---------------------------+--------------+------+-----+---------+----------------+
```
Some of the scans exclude the edges of the pages.  In these cases, I went to the Toronto Reference Library and took photos of the missing information.

The table `bloor_locations` has the following structure.
```+----------------+--------------+------+-----+---------+----------------+
| Field          | Type         | Null | Key | Default | Extra          |
+----------------+--------------+------+-----+---------+----------------+
| location_id    | mediumint(5) | NO   | PRI | NULL    | auto_increment |
| number         | varchar(20)  | YES  |     | NULL    |                |
| sector         | tinyint(4)   | YES  |     | NULL    |                |
| note           | varchar(200) | YES  |     | NULL    |                |
| spos           | varchar(6)   | YES  |     | NULL    |                |
| epos           | varchar(6)   | YES  |     | NULL    |                |
| vpos           | varchar(6)   | YES  |     | NULL    |                |
| latitude       | varchar(15)  | YES  |     | NULL    |                |
| longitude      | varchar(15)  | YES  |     | NULL    |                |
| image_filename | varchar(255) | YES  |     | NULL    |                |
+----------------+--------------+------+-----+---------+----------------+
```
For most locations, `number` is the number assigned by the city.  For some buildings on the corner of Bloor and another street, the number assigned by the city is a number on the other street.  For these buildings, I have assigned numbers on Bloor Street.  In some other cases, a building with a single number is occupied by more than one business.  In those cases, I have assigned a number like `123 L`, `123 M`, or `123 R` (for left, middle, and right).

The field `sector` is either `1`, indicating a location between Spadina and Christie or `2`, indicating a location between Christie and Lansdowne.

The fields `spos` and `epos` (starting and ending positions) are used by my routine to construct an image showing all the locations on the street.  They are not otherwise relevant.

The fields `latitude` and `longitude` are mostly unpopulated.

The field `image_filename` is used to identify the photo in which the location appears.  It is used only on the administrative site, as an aid when entering data from the directories.

The table `bloor_businesses` assigns a name to each business (usually the name of the business in the first year I observed it).
```+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| business_id | mediumint(5) | NO   | PRI | NULL    | auto_increment |
| name        | varchar(80)  | YES  |     | NULL    |                |
| comment     | varchar(200) | YES  |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
```

The table `bloor_categories`
```+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| category_id | bigint(20)   | NO   | PRI | NULL    | auto_increment |
| description | varchar(100) | YES  |     | NULL    |                |
| details     | varchar(255) | YES  |     | NULL    |                |
| seq         | float        | YES  |     | NULL    |                |
| color       | varchar(7)   | YES  |     | NULL    |                |
| dark_color  | varchar(7)   | YES  |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
```
