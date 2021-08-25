1. Create a new table by using the following SQL
```sql
CREATE TABLE "test_table" (
	sno	int,
	location varchar(255),
	org_name varchar(255),
	capacity float,
	joining_date date
);
```

2. Download [this CSV File](https://github.com/Samagra-Development/X-Series/blob/main/X1/res/Sample%20CSV.csv). Remove the second line.
3. Import file using Import/Export option in pgadmin by right clicking the table name.
