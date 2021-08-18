# Filebeat 7.14.0 on DOCKER

ไว้รวบรวมไฟล์ในแต่ละ service แล้วส่งไปให้ elk stack เป็น monitor log

## Setup

---

create `.env` file on root folder

```
SERVICE_NAME=ชื่อ service ที่จะตั้ง
PATH_LOG=path ไฟล์ที่เก็บ log
LOGSTASH_IP= ip server logstash ถ้าทำในเครื่องเดียวกันหมดให้ใช้ host.docker.internal:5044
KIBANA_IP= ip server kibana ถ้าทำในเครื่องเดียวกันหมดให้ใช้ host.docker.internal:5601
```

## Start Docker

---

```
docker-compose up -d
```

ถ้าต้องการปรับปรุงวิธีส่งใหม่ให้ไปแก้ `filebeat.yml`

```
filebeat.inputs:
- type: log
  paths:
    - /var/${SERVICE_NAME}/*.log
  fields:
    log_type: ${SERVICE_NAME}

output.logstash:
  hosts: ${LOGSTASH_IP}

setup.kibana:
  host: ${KIBANA_IP}

```
