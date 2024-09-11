# Ingest and store real-time data from IoT sensors.
- Eclip MQTT

## MQTT Topic and Payload
Topic: iot-frames
Payload:
  JsonObject payload = jsonDoc.createNestedObject("payload");
  payload["temperature"] = temp;
  payload["humidity"] = humid;
  payload["pressure"] = pressure;
  payload["luminosity"] = analogval;
  
## ESP32
>> เอา code ที่ใช้มาวาง พร้อมทั้งวาดรูป flow chart

```cpp

```
