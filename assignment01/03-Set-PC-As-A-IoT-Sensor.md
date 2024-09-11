1. install apache Maven into a pc

this is a ref
https://hub.docker.com/_/maven

https://phoenixnap.com/kb/install-maven-windows




2. Fix pom.xml file in target folder from ubuntu22 branch git to macport branch git (Copy all macport and paste it on to your u22 branch)




3. Input your hash password file into mosquitto\config\mosquitto.conf




4. Change the "allow_anonymous" in mosquitto\config\mosquitto.conf file from
-----
allow_anonymous false
-----

to

-----
allow_anonymous true
-----




5. in microservices\iot_sensor\src\main\java\com\dreamsoftware\iotframesingest\config\MQTTConfig.java file change


----------
    public MqttConnectOptions provideMqttConnectOptions() {
        MqttConnectOptions options = new MqttConnectOptions();
        options.setAutomaticReconnect(true);
        options.setCleanSession(true);
        options.setConnectionTimeout(10);
        return options;
    }
----------

to

----------
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
----------




6. in docker-compose.yml
change your "iot_sensor_2" to this

  # # # IoT Sensor 2
  iot_sensor_2:
    # image: ssanchez11/iot_sensor:0.0.1-SNAPSHOT
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




7. in your .env file input your Username, Password, MQTT_server like this for reference

--------------------
MONGO_ROOT_USER=devroot
MONGO_ROOT_PASSWORD=devroot
MONGOEXPRESS_LOGIN=dev
MONGOEXPRESS_PASSWORD=dev
MONGO_DB=iotframes
API_PORT=8088

MQTT_SERVER={YOUR_IP_ARRDESS}

IOT_SENSOR_2_ID=21321434
IOT_SENSOR_2_NAME=iot_sensor_2
IOT_SENSOR_2_PLACE_ID=32347983
IOT_SENSOR_2_USERNAME={YOUR_USERNAME}
IOT_SENSOR_2_PASSWORD={YOUR_PASSWORD}
--------------------




8. use this command in microservice/iot_sensor
`````
docker run --rm --name my-maven-project -v "${PWD}:/usr/src/mymaven" -w /usr/src/mymaven maven:3.8-openjdk-8 mvn clean install
`````




9. change all the file that had "mosquitto:1883" to your ip such as "172.16.46.21:1883"




10. use this command to start your iot_sensor_2
````` 
docker compose up iot_sensor_2
`````