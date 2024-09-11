# Main technologies of architecture

## Architecture Overview

![IoT Event Streaming Architecture ![F351E2C8-6E5A-4243-A734-352C90589307](https://github.com/user-attachments/assets/206acbde-8d36-4a34-a7a3-3fcbeb8fccd4)


## Eclipse Mosquitto



## Apache ZooKeeper

    ระบบ Central Service สำหรับการกำหนดค่าต่างๆ ระหว่าง Service ในกลุ่มเดียวกัน เพื่อลดความซับซ้อนในการใช้งานขณะที่ทำการ Deploy application ช่วยให้การจัดการระบบกระจายเป็นไปอย่างมีประสิทธิภาพ

## Apache Kafka

    Apache Kafka เป็น Platform สำหรับการใช้ส่ง, เก็บ, ดำเนินการ และติดตาม data stream จากหลายแหล่งที่มาเหมาะสำหรับการสร้าง data pipeline ที่มีประสิทธิภาพสูงและการวิเคราะห์ข้อมูลแบบ Real Timeโดยมีข้อดีคือความสามารถในการจัดการข้อมูลปริมาณมากและมีความยืดหยุ่นสูง


## Apache Kafka Connect

    เป็น Framework ในการเชื่อมต่อเครือข่ายในระบบเข้ากับเรือข่ายภายนอก เช่น Database หรือ File Systems โดยจะเน้นที่ Streaming Data ที่ส่งไปที่ Kafka และมาจาก Kafka เพื่อการเขียน Connector Plugin ที่มีประสิทธิภาพ

## Apache Kafka Streams

    เป็น Client Library สำหรับการสร้าง Application และ Microservice ใช้สำหรับการประมวลผลและการวิเคราะห์ข้อมูลที่เก็บใน Kafka Cluster ช่วยให้การสร้าง Application และ Microservice ที่มีประสิทธิภาพสูงและสามารถประมวลผลข้อมูลแบบเรียลไทม์

## Prometheus

    เป็น Software สำหรับการติดตามและแจ้งเตือน Event ต่างของ Database โดยทำงานด้วยการบันทึก Metric ของ Time-series Database ที่ใช้งาน HTTP Pull Model

## MongoDB

    MongoDB เป็นระบบ NoSQL Database แบบ Open source ใช้ Document Data Model สำหรับการจัดเก็บและการจัดการข้อมูล ช่วยให้การจัดเก็บและการจัดการข้อมูลเป็นไปอย่างยืดหยุ่นและมีประสิทธิภาพ ซึ่งมีความสามารถในการขยายและการจัดการข้อมูลที่มีประสิทธิภาพสูง

## Grafana

    Software ที่มีพื้นฐานมาจาก Apache 2.0 ใช้ในการแสดงผลข้อมูลที่อยู่ในรูปแบบ Metric Data สามารถแสดงผลได้ด้วยการสร้าง Dashboard และกราฟจากข้อมูล รองรับการแสวงข้อมูลจาก Time Series Databases 
