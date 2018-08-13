# Default Time Zone

To view the global and session time zones for MySQL:

```sql
SELECT @@global.time_zone, @@session.time_zone;
```

To set the default time zone to UTC add the following line to the MySQL config:
```
[mysqld]
default-time-zone='+00:00'
```

For Homebrew installations of mysql, the config file can be found at `/usr/local/etc/my.cnf`.

Lastly, be sure to restart the server. For Homebrew installations:

```
mysql.server restart
```
