

Download the latest jar from
https://oss.sonatype.org/content/repositories/snapshots/am/ik/demo/demo-oracledb/0.0.1-SNAPSHOT/


### How to run locally

```
java -jar demo-oracledb-0.0.1-*.jar \
  --spring.datasource.username=**** \
  --spring.datasource.password=**** \
  --spring.datasource.url=jdbc:oracle:thin:@<hostname>:<port>:<sid>
```

```
$ curl http://localhost:8080
2020-04-20 18:00:59
```

```
$ curl http://localhost:8080/actuator/health
{"status":"UP","components":{"db":{"status":"UP","details":{"database":"Oracle","result":"Hello","validationQuery":"SELECT 'Hello' from DUAL"}},"diskSpace":{"status":"UP","details":{"total":1000240963584,"free":749625405440,"threshold":10485760}},"ping":{"status":"UP"}}}
```

### How to deploy to Cloud Foundry

#### Connection Type: SID

```
cf create-service credhub default demo-db -c '{"username":"<username>", "password":"<password>", "jdbcUrl":"jdbc:oracle:thin:@<hostname>:<port>:<sid>"}'
```

or 

```
cf create-user-provided-service demo-db -p '{"username":"<username>", "password":"<password>", "jdbcUrl":"jdbc:oracle:thin:@<hostname>:<port>:<sid>"}'
```
#### Connection Type: Service Name

```
cf create-service credhub default demo-db -c '{"username":"<username>", "password":"<password>", "jdbcUrl":"jdbc:oracle:thin:@//<hostname>:<port>/<servicename>"}'
```

or 

```
cf create-user-provided-service demo-db -p '{"username":"<username>", "password":"<password>", "jdbcUrl":"jdbc:oracle:thin:@//<hostname>:<port>/<servicename>"}'
```

then,

```
wget https://raw.githubusercontent.com/making/demo-oracledb/master/manifest.yml
cf push -p demo-oracledb-0.0.1-*.jar	
```
