# 時刻表服務
CAJ 使用之時刻表服務

## Image 位置
```
quay.io/ske/m-caj-schedule
```

## 環境變數

| No | 變數 | 說明 | 預設值 |
| -------- | -------- | -------- | -------- |
| 1     | DB_DIALECT     | DB 語系     |org.hibernate.dialect.H2Dialect|
| 2     | DB_DRIVER     | DB 驅動程式     |org.h2.Driver|
| 3     | DB_URL     | DB 連線位置     |jdbc:h2:mem:lab;DB_CLOSE_DELAY=-1|
| 4     | DB_USER     | DB 使用者     |sa|
| 5     | DB_PXD     | DB 密碼     |sa|
| 6     | JAEGER_URI     | Jaeger 位置     |http://jaeger-collector.istio-system.svc:4318/v1/traces|


## 應用基本資訊
* Health Check Endpoint
```
/actuator/health
```
* Prometheus Exporter
```
/actuator/prometheus
```

* Swagger UI
```
/swagger-ui.html
```

## 應用建置
1. 程式碼品質掃描
```bash=
mvn clean package sonar:sonar \
-Dsonar.projectKey=PROJECT_KEY \
-Dsonar.projectName='PROJECT_NAME' \ 
-Dsonar.host.url=http://localhost:9000 \ 
-Dsonar.token=THE_GENERATED_TOKEN
```

2. 建置 Java Artifact
```bash=
mvn clean package
ls target
```

3. 啟動應用
```bash=
# 預設 port 8080
java -jar target/schedule-0.0.1-SNAPSHOT.jar
```


## 容器化
1. 建置容器
```bash=
podman build -f Containerfile -t m-caj-schedule:latest .
```


2. 啟動容器
```bash=
podman run -p 8080:8080 m-caj-m-caj-schedule:latest
```