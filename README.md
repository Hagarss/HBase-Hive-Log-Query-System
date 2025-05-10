
---

## Log Analysis with Hive & HBase

This project demonstrates how to store and query log data using **Apache HBase** and **Apache Hive**. It includes the creation of HBase tables and namespaces, integration with Hive for SQL-like querying, and retrieval of log entries based on specific conditions such as service type.
![image](https://github.com/user-attachments/assets/508d8736-20f4-4aee-aa05-acf7dd9c6b92)


---

### Technologies Used

* Apache HBase
* Apache Hive
* Hadoop (HDFS)
* ZooKeeper (for HBase coordination)
* Bash Shell

---

### Project Tasks

#### 1. Create HBase Namespace

```bash
hbase shell
create_namespace 'bigdata'
```

#### 2. Create HBase Table

```bash
create 'bigdata:AnalysisLog_ID', 'LogInfo'
```
![image](https://github.com/user-attachments/assets/60bdb191-9b2c-4c2c-bc4f-24febda7908e)

#### 3. Insert Log Data into HBase

```bash
put 'bigdata:AnalysisLog_ID', '001', 'LogInfo:hostname', 'FI01Miner01'
put 'bigdata:AnalysisLog_ID', '001', 'LogInfo:service', 'miner'
put 'bigdata:AnalysisLog_ID', '001', 'LogInfo:type', 'info'

put 'bigdata:AnalysisLog_ID', '002', 'LogInfo:hostname', 'FI01Miner02'
put 'bigdata:AnalysisLog_ID', '002', 'LogInfo:service', 'zookeeper'
put 'bigdata:AnalysisLog_ID', '002', 'LogInfo:type', 'info'

put 'bigdata:AnalysisLog_ID', '003', 'LogInfo:hostname', 'FI01Miner01'
put 'bigdata:AnalysisLog_ID', '003', 'LogInfo:service', 'miner'
put 'bigdata:AnalysisLog_ID', '003', 'LogInfo:type', 'error'

put 'bigdata:AnalysisLog_ID', '004', 'LogInfo:hostname', 'FI01Miner02'
put 'bigdata:AnalysisLog_ID', '004', 'LogInfo:service', 'miner'
put 'bigdata:AnalysisLog_ID', '004', 'LogInfo:type', 'error'

put 'bigdata:AnalysisLog_ID', '005', 'LogInfo:hostname', 'FI01Miner02'
put 'bigdata:AnalysisLog_ID', '005', 'LogInfo:service', 'spark'
put 'bigdata:AnalysisLog_ID', '005', 'LogInfo:type', 'info'

put 'bigdata:AnalysisLog_ID', '006', 'LogInfo:hostname', 'FI01Miner01'
put 'bigdata:AnalysisLog_ID', '006', 'LogInfo:service', 'zookeeper'
put 'bigdata:AnalysisLog_ID', '006', 'LogInfo:type', 'debug'

put 'bigdata:AnalysisLog_ID', '007', 'LogInfo:hostname', 'FI01Miner03'
put 'bigdata:AnalysisLog_ID', '007', 'LogInfo:service', 'zookeeper'
put 'bigdata:AnalysisLog_ID', '007', 'LogInfo:type', 'debug'

put 'bigdata:AnalysisLog_ID', '008', 'LogInfo:hostname', 'FI01Miner02'
put 'bigdata:AnalysisLog_ID', '008', 'LogInfo:service', 'miner'
put 'bigdata:AnalysisLog_ID', '008', 'LogInfo:type', 'info'

put 'bigdata:AnalysisLog_ID', '009', 'LogInfo:hostname', 'FI01Miner01'
put 'bigdata:AnalysisLog_ID', '009', 'LogInfo:service', 'miner'
put 'bigdata:AnalysisLog_ID', '009', 'LogInfo:type', 'info'
```

---

### Hive-HBase Integration

#### 4. Create Hive External Table

```sql
CREATE EXTERNAL TABLE Log_hive_ID(
  key string,
  hostname string,
  service string,
  type string
)
STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
WITH SERDEPROPERTIES (
  "hbase.columns.mapping" = ":key,LogInfo:hostname,LogInfo:service,LogInfo:type"
)
TBLPROPERTIES (
  "hbase.table.name" = "bigdata:AnalysisLog_ID"
);
```
![image](https://github.com/user-attachments/assets/58f612ac-961a-4a08-b3c0-2a7cb97c984b)

---

### Querying the Logs

#### 5. Query All Logs with Service = 'miner'

```sql
SELECT * FROM Log_hive_ID WHERE service = 'miner';
```

---

###  Output

![image](https://github.com/user-attachments/assets/01ef0f82-d0c6-4767-80a3-236170459716)


---

###  Summary

This project demonstrates how HBase can be used as a scalable NoSQL backend for log storage, while Hive provides SQL-like access for analytics. It is especially useful for large-scale log processing in big data environments.

---

