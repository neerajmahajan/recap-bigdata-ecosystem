# recap-bigdata-ecosystem

###### Scoop
```
sqoop list-databases --connect jdbc:mysql://host/datbase_name --username sqoop --password sqoop
sqoop list-tables --connect jdbc:mysql://host/database_name --username sqoop --password sqoop

hdfs dfs -mkdir sqoop-mysql-import

sqoop import --connect jdbc:mysql://host/datbase_name --username sqoop --password sqoop
  --table <table_name>
  -m 1
  --target-dir /user/hdfs/sqoop-mysql-import/country

hdfs dfs -cat sqoop-mysql-import/country/part-m-00000

````
