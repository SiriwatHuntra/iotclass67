# Main technologies of architecture

## Architecture Overview

![IoT Event Streaming Architecture](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*IUaBLlbVKgmsjbjqzew0ZQ.png)

## Eclipse Mosquitto
	โปรแกรม Open Source สำหรับการจัดการ Message (Message Broker) ในการใช้งาน MQTT Protocol สามารถใช้งานได้บนคอมพิวเตอร์ขนาดเล็กจนถึงเครื่อง Server
 	MQTT Protocol เป็น Protocol สำหรับการใช้ส่ง Message ระหว่างอุปกรณ์แบบ Asynchronous (Pub/Sub Model) เหมาะสำหรับการใช้งานบนระบบ IoT ที่ประกอบด้วย Low Power Sensor และ Mobile Device ในระบบ

## Apache ZooKeeper
	ระบบ Central Service สำหรับการกำหนดค่าต่างๆ ระหว่าง Service ในกลุ่มเดียวกัน เพื่อลดความซับซ้อนในการใช้งานขณะที่ทำการ Deploy application

## Apache Kafka
	Platform สำหรับการส่งกระจายข้อมูล เพื่อการส่ง, เก็บ, ดำเนินการ และติดตาม data stream ที่มาจากหลายแหล่งที่มา และกระจายไปยังอุปกรณ์ในเครือข่าย

## Apache Kafka Connect
	Frame Work ในการเชื่อมต่อเครือข่ายในระบบเข้ากับเรือข่ายายนอก เช่น Databases หรือ File Systems โดยจะเน้นที่ Streaming Data ที่ส่งไปที่ Kafka และมาจาก Kafka เพื่อการเขียน Connector Plugin ที่มีประสิทธิภาพ


## Apache Kafka Streams
	Client Library สำหรับการสร้าง Application และ Microservice สำหรับการเก็บ Input และ Output ใน Apache Kafka Cluster


## Prometheus
    Software สำหรับการติดตามและแจ้งเตือน Event ต่างของ Database ด้วยการบันทึก Metric ของ Time-series Database ที่ใช้งาน HTTP Pull Model


## MongoDB
	ระบบ NoSQL Database แบบ Open source  


## Grafana
    Software ที่มีพื้นฐานมาจาก Apache 2.0 ใช้ในการแสดงผลข้อมูลที่อยู่ในรูปแบบ Metric Data สามารถแสดงผลได้ด้วยการสร้าง Dashboard และกราฟจากข้อมูล รองรับการแสวงข้อมูลจาก Time Series Databases 

