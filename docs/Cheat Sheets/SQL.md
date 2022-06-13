# SQL

## Common Basic Commands

### SHOW ERRORS Example

``` SQL
SHOW ERRORS TRIGGER trigger_name;
```

### Get Number of Instances

```
select count(*), column_of_interest from table_name GROUP BY column_of_interest HAVING COUNT(*) > 1;
```

### UPDATE Example

```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

### INSERT Example

```
INSERT INTO table_name
VALUES
(value1,value2,...);
```

### CREATE Example

CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 DATE,
    column4 NUMBER(10,0),
    column5 VARCHAR(255),
   ....
);

GRANT SELECT ON "APP"."NAME_OF_VIEW" TO "USER";

### CREATE view with new data along with all data from a table

CREATE OR REPLACE FORCE EDITIONABLE VIEW "USER"."NAME_OF_VIEW" ("SPECIAL_COLUMN", "COLUMN_FROM_OTHER_TABLE", "ANOTHER_COLUMN_FROM_OTHER_TABLE") AS 
  select
      'special ' || t.special_column AS SPECIAL_COLUMN, -- put 'special ' in front of table value
      t.*
    from
      base_table_name t;

## Altering a Table

### Drop Column Example

```
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Add Column Example

```
ALTER TABLE Customers
ADD Email varchar(255);
```

### Rename Column Example

```
ALTER TABLE Customers
RENAME COLUMN old_name TO new_name;
```

### DROP Table Example

```
DROP TABLE table_name;
```

## Altering Data

### DELETE a row
```
DELETE FROM table_name WHERE condition;
