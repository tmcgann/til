To run seed a mysql database from the CLI:

```bash
mysql -p -u <username> <database> < <filename>
```

To dump the database into a sql script:

```bash
mysqldump -p -u <username> <database> > <filename>
```

For example:

```bash
mysql -p -u root my_database < dummy_data.sql
mysqldump -p -u root my_database > dummy_data.sql
```
