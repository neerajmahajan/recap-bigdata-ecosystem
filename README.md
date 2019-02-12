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

###### Using options.file (shortcut)

* format : Use below format and save as hdr-options.txt
* To run import now do

```sqoop --options-file hdr-options.txt --table product -m 1 --target-dir <path>```

```
import
--connect
jdbc:mysql://fin-server/hdr
--username
root
--password
root_password
```

###### Using query to import data and using multiple mappers
```
sqoop --options-file hdr-options.txt -m 4 --target-dir <path> 
--query "SELECT id,name from product where brand='hero' AND \$CONDITIONS" --split-by id
```

###### Export

```
sqoop --options-file hdr-export-options.txt 
--table product --staging-table product_staging
--clear-staging-table
-m 4
--export-dir <path> 
--query "SELECT id,name from product where brand='hero' AND \$CONDITIONS" --split-by id
```
######  Hadoop Basic commmands

* Adding file to HDFS ```hdfs dfs -put sample.csv /tmp/serdes/```
