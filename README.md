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
######  HDFS

* Client node ask NameNode where to find data.
* Name node says use these nodes.
* Data node, respond back to NAme node about the status.
* HDFS doesn't support hard/soft links.
* 64MB blocks


* Adding file to HDFS ```hdfs dfs -put sample.csv /tmp/serdes/```

##### Map - Reduce
* Based on Key,Value pairs.
* Moving computation is cheaper than moving data.
* Data is sliced and stored in distributed and replicate form.
* Map is applied parallely on each data slice.
* Each map operation writes the ouput to disk
* Reduce step take the processed data and does the reduction.
* Computation is moved to where data reside.

