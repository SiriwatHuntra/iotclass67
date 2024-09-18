# IoT Sensor Setup and Configuration Guide

## 1. Install Apache Maven into a PC

To install Apache Maven, follow the steps below:
- Docker Maven: [Docker Maven Installation Guide](https://hub.docker.com/_/maven)
- Windows Maven Installation: [PhoenixNap Guide](https://phoenixnap.com/kb/install-maven-windows)

## 2. Fix `pom.xml` File

- Switch from the `ubuntu22` branch in Git to the `macport` branch.
- Copy all the files from the `macport` branch and replace them in the `u22` branch.

## 3. Input Hash Password in Mosquitto Config

- Add your hashed password to the `mosquitto\config\mosquitto.conf` file.

## 4. Change `allow_anonymous` in Mosquitto Config

- In the `mosquitto\config\mosquitto.conf` file, change:

```bash
allow_anonymous false
```
to
```bash
allow_anonymous true
```

## 5. Update MQTTConfig.java

- In the directory microservices\iot_sensor\src\main\java\com\dreamsoftware\iotframesingest\config\MQTTConfig.java file, change the method provideMqttConnectOptions from:

```
public MqttConnectOptions provideMqttConnectOptions() {
    MqttConnectOptions options = new MqttConnectOptions();
    options.setAutomaticReconnect(true);
    options.setCleanSession(true);
    options.setConnectionTimeout(10);
    return options;
}
```

to

```
public MqttConnectOptions provideMqttConnectOptions(@Value("${sensor.mqtt.username}") String mqttUsername,
@Value("${sensor.mqtt.password}") String mqttPassword) {
    MqttConnectOptions options = new MqttConnectOptions();
    options.setAutomaticReconnect(true);
    options.setCleanSession(true);
    options.setConnectionTimeout(10);
    options.setUserName(mqttUsername);
    options.setPassword(mqttPassword.toCharArray());
    return options;
}
```

## 6. Update docker-compose.yml
- Modify the service configuration for iot_sensor_2 in your docker-compose.yml to:

```
# IoT Sensor 2
iot_sensor_2:
  build:
    context: ./microservices/iot_sensor
    args:
      - MQTT_SERVER=${MQTT_SERVER}
  container_name: iot_sensor_2
  restart: unless-stopped
  environment:
    - sensor.id=${IOT_SENSOR_2_ID}
    - sensor.name=${IOT_SENSOR_2_NAME}
    - sensor.place.id=${IOT_SENSOR_2_PLACE_ID}
    - sensor.mqtt.username=${IOT_SENSOR_2_USERNAME}
    - sensor.mqtt.password=${IOT_SENSOR_2_PASSWORD}
    - MQTT_SERVER=${MQTT_SERVER}
```

## 7. Add Environment Variables in .env File

- In your .env file, add the following environment variables:

```
MONGO_ROOT_USER=devroot
MONGO_ROOT_PASSWORD=devroot
MONGOEXPRESS_LOGIN=dev
MONGOEXPRESS_PASSWORD=dev
MONGO_DB=iotframes
API_PORT=8088

MQTT_SERVER={YOUR_IP_ADDRESS}

IOT_SENSOR_2_ID=21321434
IOT_SENSOR_2_NAME=iot_sensor_2
IOT_SENSOR_2_PLACE_ID=32347983
IOT_SENSOR_2_USERNAME={YOUR_USERNAME}
IOT_SENSOR_2_PASSWORD={YOUR_PASSWORD}
```

## 8. Build IoT Sensor Microservice

Use the following command in microservice/iot_sensor:

```
docker run --rm --name my-maven-project -v "${PWD}:/usr/src/mymaven" -w /usr/src/mymaven maven:3.8-openjdk-8 mvn clean install
```

## 9. Replace mosquitto:1883 with Your IP

Find and replace all instances of "mosquitto:1883" with your IP address, such as "172.16.46.21:1883".

## 10. Start iot_sensor_2 Service

```
docker compose up iot_sensor_2
```
