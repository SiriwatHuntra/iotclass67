# IoT Docker compose


## start-service #0

start service ในหน้าจอ service_0 มี zookeeper และ kafka
โดยเราต้องรอให้ทั้ง 2 ตัวนี้ Run ให้เรียบร้อยก่อนที่จะไป Step ต่อไป เพื่อให้เราไม่มีปัญหาในตอนข้อมูลขึ้น
โดยให้รออย่างน้อย 5 นาที หรือ จน terminal นั้นมีความนิ่ง

## start-service #1

start service ในหน้าจอ service_1 มี kafka-rest-proxy, kafka-connect, mosquitto, mongo, grafana และ prometheus
โดยเราต้องรอให้ทั้ง 6 ตัวนี้ Run ให้เรียบร้อยก่อนที่จะไป Step ต่อไป เพื่อให้เราไม่มีปัญหาในตอนข้อมูลขึ้น
โดยให้รออย่างน้อย 5 นาที หรือ จน terminal นั้นมีความนิ่ง

## start-service #2

start service ในหน้าจอ service_2 มี iot-processor
โดยเราต้องรอให้ทั้ง 1 ตัวนี้ Run ให้เรียบร้อยก่อนที่จะไป Step ต่อไป เพื่อให้เราไม่มีปัญหาในตอนข้อมูลขึ้น
โดยให้รออย่างน้อย 5 นาที หรือ จน terminal นั้นมีความนิ่ง
หรือจน iot-processor นั้นมีข้อความที่ขึ้นว่า REBLANCEING TO RUNNING เป็นคำสำคัญ
ไม่อย่างงั้นต้องทำการ Restart ไปเรื่อย ๆ

## start-service #3

start service ในหน้าจอ service_3 มี iot_sensor_1
โดยเราต้องรอให้ทั้ง 1 ตัวนี้ Run ให้เรียบร้อยก่อนที่จะไป Step ต่อไป
โดยให้ Run ได้เลย