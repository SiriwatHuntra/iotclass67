# Data Visualization.

ข้อมูลที่จะนำมาแสดงนั้นเป็นข้อมูลที่ได้จากเครื่อง Gateway โดยข้อมูลที่ดึงมาแสดงจะ
ประกอบด้วย 1. อุณหภูมิ 2. ความชื้น 3. แสง 4. แรงดันไฟฟ้า  5. สถานะ Gateway

- # IOT sensuor Humidity
  
![Humi](https://github.com/user-attachments/assets/bc1e72df-f1a4-4143-bd40-2719874f9fe1)

- # IOT sensor AVG Temperature
  
![AVGTemp](https://github.com/user-attachments/assets/98ed7821-f15a-4ec2-b0b5-1a3fba4620ae)

- # IOT sensuor Luminosity

![Lumi](https://github.com/user-attachments/assets/150e217e-47bf-4bc9-9fd2-c545c0d1a592)

- # IOT sensuor Pressure

![Presure](https://github.com/user-attachments/assets/c374c01c-704c-442f-9ec5-f57b8592f907)

- # IOT sensor Temperature

![Temp](https://github.com/user-attachments/assets/cbc9db10-f936-4d2f-aa26-b55e954af69f)

- # IOT 10 sensor map dashbord

![10sensor](https://github.com/user-attachments/assets/d0b21df3-7f16-4b05-adba-1a1acce8f777)

- # Node Exporter

![Node](https://github.com/user-attachments/assets/c3885aba-e15b-4b62-b986-c82b33cf6e1f)

- # วิธีการทำ IOT 10 sensor map dashbord

1. ลง Plugin Flowcharting จาก (https://github.com/skyfrank/grafana-flowcharting/releases/tag/v1.0.0e)

- Remote เข้าไปในเซิร์ฟเวอร์ เข้าไปใน folder Plugin ของ grafana

- สร้าง Directory ใหม่เพือลงไฟล์ Zip ในเซิร์ฟเวอร์ 

```cpp
sudo mkdir Name_directory
```

- เข้าไปใน Directory ใหม่ที่สร้างไว้

- โหลดไฟล์ zip เข้าเซิร์ฟเวอร์

```cpp
sudo wget Link_by_Flowcharting
```

![Step1_1](https://github.com/user-attachments/assets/d583d01e-f3c3-4eee-b9b4-583a223a2c56)

- แตกไฟล์ Zip

```cpp
sudo unzip File_name
```

- ย้ายไฟล์ dist ออกมาจาก Directory

```cpp
sudo mv dist Grafana-flowcharting
```

- ebit flie docker-compose.yml ที่บรรทัด 289,290

![Step1_2](https://github.com/user-attachments/assets/f7b4b973-eb41-45c5-bd6d-02c1af8edf57)

- restart grafana

```cpp
docker compose restart grafana
```

2. เลือกใช้ plugin ใน dashboard

![Step2](https://github.com/user-attachments/assets/4dee787b-33f4-4775-acce-0ea08f07ea9e)

3. เลือกดึงข้อมูลจาก Prometheus โดยเซ็ตข้อมูลที่ต้องการใน Metric

![Step3](https://github.com/user-attachments/assets/3e2aa72b-ebdf-498b-9f40-d990c66079de)

- เซ็ต Options เพื่อความสดวกในการเรียกใช้

![Step3_1](https://github.com/user-attachments/assets/0976f9f2-d460-4247-9da2-88d49a6a3253)

4. เซ็ตภาพที่ต้องการ ใน Draw.io โดยใช้คำาสั่ง Edit Diagram

- import ไฟล์ .csv (สามารถนำไฟล์ ภาพ เข้าในโปรแกรม Draw.io แล้ว export ออกมาเป็นไฟล์ .csv ได้)

![Step4_1](https://github.com/user-attachments/assets/e1662b6c-9495-4675-aaa9-a2079a8e87fd)

- วาง Opject ลงในจุดที่ต้องการแล้ว กด save

5. เลื่อนไปที่ Rule เพื่อ เซ็ต จุดวางเซ็นเซอร์แต่ละตัว

![Step5_1](https://github.com/user-attachments/assets/d9461fe8-87d0-4528-acde-55e7f99f7d6f)

- เซ็ตข้อมูลที่ต้องการดึง

![Step5_2](https://github.com/user-attachments/assets/b0ba20bc-5626-4fee-bf94-377678276e87)

- เซ็ตสีที่ต้องการ

![Step5_3](https://github.com/user-attachments/assets/65c55539-7c30-448c-83a0-f4b823dcf2f6)

- เลือก Opject และ Text ที่ต้องการแสดง

![Step5_4](https://github.com/user-attachments/assets/c92350cf-99ca-45aa-a430-9b125080dfd6)

- save, apply

- # วิธีการทำ Node Exporter

- Edit File docker-compose.yml node exporter

![Node1](https://github.com/user-attachments/assets/01fd20de-e8cf-4639-a790-fbc7bfd373fb)

- Edit File prometheus.yml

![Node2](https://github.com/user-attachments/assets/b6ad12b8-330e-4e22-a4c8-3dba984df4dc)

- restart prometheus

```cpp
docker compose restart prometheus
```

- ลง Dashbord ใน Grafana โดย import dashbord json file (เลือก template จากใน Internet)
