# MQTT
# Ingest and store real-time data from IoT sensors


IoT sensors ส่งข้อมูลด้วย MQTT protocol. 
- **Mosquitto (MQTT Broker)**: The MQTT broker (Mosquitto) receives sensor data and publishes it to specified topics.
- **Kafka Connect MQTT Source**: Kafka Connect pulls data from the MQTT broker and sends it to the Kafka cluster for processing. This integration ensures that raw sensor data is continuously streamed into Kafka topics.

- **Kafka Topics**: Data from IoT sensors is published to Kafka topics (e.g., `iot-frames`, `iot-aggregate-metrics-sensor`).
- **Kafka Connect MongoDB**: Data stored in Kafka is further processed and consolidated into MongoDB, a NoSQL database. This enables efficient storage of sensor data for long-term access and later viewing.


## iot-sensor-1

IoT Sensor 1 เป็น IoT ที่ได้มาจากการ compose up docker ใน Server ตัวมันเอง

## iot-sensor-2

IoT Sensor 2 เป็น IoT ที่ได้มาจากการ compose up docker ใน PC ตัวนอกที่ได้ทำการส่งข้อมูลไปยัง Server

## iot-sensor-3-10

IoT Sensor 3 เป็น IoT ที่ได้ข้อมูลมาจากการที่ IoT เราเอง 1 ตัว และ ตัวอื่นหรือกลุ่มอื่น ๆ ส่งมาให้เราอีก
