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
/// LIB
#include <Wire.h>
#include <Adafruit_BMP280.h>
#include <Adafruit_MPU6050.h>
#include <SensirionI2cSht4x.h>
#include <Adafruit_NeoPixel.h>
#include <ESPNtpClient.h>
#include <PubSubClient.h>
#include <ArduinoJson.h>
#include <WiFiUdp.h>
#include <WiFi.h>
#include <SPI.h>

/// Set up WiFi config
//const char* ssid = "TP-Link_7F5E2"; //Chai.net
//const char* password = "P@ssw0rd";
const char* ssid = "TP-Link_7CC6"; //Pon.net
const char* password = "08378774";
//const char* ssid = "TP-Link_CA1E"; //JAE.net
//const char* password = "34397121"; 
//const char* ssid = "TP-Link_CA30";
//const char* password = "29451760";
//

const int mqtt_port = 1883;
/// Own user pass 
const char* mqtt_server = "172.16.47.1";
const char* mqtt_user = "iot-frames-3";
const char* mqtt_password = "1234";

// Pon User_pass 
//const char* mqtt_server = "172.16.46.11";
//const char* mqtt_user = "liam-sensor-6";
//const char* mqtt_password = "1q2w3e4r";

// Kong User_pass 
//const char* mqtt_server = "172.16.46.41";
//const char* mqtt_user = "iot-frames-4";
//const char* mqtt_password = "kong4";

// big User_pass 
//const char* mqtt_server = "172.16.46.101";
//const char* mqtt_user = "iot-b_b-frames-7";
//const char* mqtt_password = "1234";

// north User_pass 
//const char* mqtt_server = "172.16.46.55";
//const char* mqtt_user = "kinano05";
//const char* mqtt_password = "1234";

// jae User_pass 
//const char* mqtt_server = "172.16.46.37";
//const char* mqtt_user = "iot-frames-4";
//const char* mqtt_password = "nX7M";

// five User_pass 
//const char* mqtt_server = "172.16.46.111";
//const char* mqtt_user = "aimpree7";
//const char* mqtt_password = "aimpree";

// game User_pass 
//const char* mqtt_server = "172.16.46.55";
//const char* mqtt_user = "iot-sensor-4";
//const char* mqtt_password = "12345";

/// Net
const PROGMEM char* ntpServer = "172.16.47.1";

/// Sensor Config
// BMP280
Adafruit_BMP280 bmp280;

//DHT 11
SensirionI2cSht4x sensor;

int sensorPin = 5;
int analogValue = 1;

//Setup Notification LED
#define LED_PIN 18          // LED pin
#define LED_COUNT 60        // Number of LEDs in the strip
#define BRIGHTNESS 50       // Brightness level (0-255)

Adafruit_NeoPixel strip(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);

// Functions to control the LEDs with different colors (GRB)
void REDLED() {
  strip.fill(strip.Color(0, 255, 0), 0, LED_COUNT);
  strip.show();
}

void PURPLELED() {
  strip.fill(strip.Color(0, 255, 255), 0, LED_COUNT);
  strip.show();
}

void GREENLED() {
  strip.fill(strip.Color(150, 0, 0), 0, LED_COUNT);
  strip.show();
}

void BLUELED() {
  strip.fill(strip.Color(0, 0, 255), 0, LED_COUNT);
  strip.show();
}

void YELLOWLED() {
  strip.fill(strip.Color(255, 255, 0), 0, LED_COUNT);
  strip.show();
}

void LEDOFF(){
  strip.fill(strip.Color(0, 0, 0), 0, LED_COUNT); // Turn LED off
  strip.show();
}


/// const for error handle 
static char errorMessage[64];
static int16_t error;
#define NO_ERROR 0

/// Network config setup
WiFiClient espClient;
PubSubClient client(espClient);
WiFiServer server(1883);
IPAddress local_IP(172, 16, 47, 27);   // Static IP address
IPAddress gateway(172, 16, 46, 254);      // IP address of your router
IPAddress subnet(255, 255, 255, 192);

void LED_Setup(){
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
  strip.setBrightness(BRIGHTNESS);
}

/// WiFi void setup()
void setup_wifi() {
  delay(10);
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);

  /// Wait until connect
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print("_");
    PURPLELED();
    delay(50);
    LEDOFF();
  }

  // Report
  Serial.println(" ");
  Serial.println("Success to connect with WiFi!");
  Serial.println("IP address: ");
  REDLED();
  Serial.println(WiFi.localIP());
}

///MQTT Connection Error handle
void mqtt_handle() {
  //wait for mqtt
  while (!client.connected()) {
    Serial.print("Connecting with MQTT...");

    if (client.connect("Form_Chai", mqtt_user, mqtt_password)) {
      Serial.println("Already connected");
      GREENLED();
      client.subscribe("esp32/sensorData");
    } else {
      Serial.print("Fails to connect with MQTT");
      Serial.print("Client State: ");
      Serial.println(client.state());
      Serial.println("Try...");
      GREENLED();
      delay(1000);
      LEDOFF();
    }
  }
}

///Sensor Init
void init_BMP280() {
  if (!bmp280.begin(0x76)) {
    Serial.println(F("BMP280 Down"));
    while (1) delay(10);
  }

  bmp280.setSampling(Adafruit_BMP280::MODE_NORMAL,
                     Adafruit_BMP280::SAMPLING_X2,
                     Adafruit_BMP280::SAMPLING_X16,
                     Adafruit_BMP280::FILTER_X16,
                     Adafruit_BMP280::STANDBY_MS_500);
  Serial.println("BMP280 ready");
  BLUELED();
  delay(200);
  LEDOFF();
}

void init_SHT4x() {
  sensor.begin(Wire, SHT40_I2C_ADDR_44);
  sensor.softReset();
  delay(10);
  uint32_t serialNumber = 0;
  error = sensor.serialNumber(serialNumber);
  checkError(error, "Error to call serialNumber()");
  Serial.print("serialNumber: ");
  Serial.println(serialNumber);
  BLUELED();
  delay(200);
  LEDOFF();
}

/// Handle Error
void checkError(int16_t error, const char* errorMsg) {
  if (error != NO_ERROR) {
    Serial.print(errorMsg);
    errorToString(error, errorMessage, sizeof errorMessage);
    Serial.println(errorMessage);
    BLUELED();
    delay(100);
    LEDOFF();
  }
}

void init_NTP() {
  NTP.setTimeZone(TZ_Asia_Bangkok);
  NTP.setInterval(600);
  NTP.setNTPTimeout(5000);
  NTP.begin(ntpServer);
}

// Setup 
void setup()
{
  Wire.begin(41, 40);
  Serial.begin(115200);

  /// Network
  setup_wifi();
  client.setServer(mqtt_server, mqtt_port);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  server.begin();

  //// Check if wifi fail
  if (!WiFi.config(local_IP, gateway, subnet)) {
    Serial.println("Wifi Failed to configure");
  }

  /// inot sensor
  init_BMP280();
  init_SHT4x();

  // NTP
  init_NTP();
}

///Setup Time
unsigned long Get_EpochTime() {
    time_t now;
    struct tm timeinfo;
    if (!getLocalTime(&timeinfo)) {
      return 0;
    }
    time(&now);
    return now;
}

/// Main void loop()
void loop(){
  if (WiFi.status() != WL_CONNECTED){
    setup_wifi();
  }
  if (!client.connected()) {
    mqtt_handle();
  }

  client.loop();
  YELLOWLED();
  delay(5000);
  LEDOFF();
  /// Data assign 
  float temp = bmp280.readTemperature();
  float pressure = bmp280.readPressure() /100;
  float aTemperature = 0.0;
  float humid = 0.0;
  error = sensor.measureLowestPrecision(temp, humid);
  checkError(error, "Error to call STHX4");
  int analogval = analogRead(sensorPin);
  unsigned long epochTime = Get_EpochTime();

  Serial.println(temp);
  Serial.println(pressure);
  Serial.println(humid);
  Serial.println(analogval);
  /// json output
  StaticJsonDocument<512> jsonDoc;
  jsonDoc["id"] = "65476587"; //43245253
  jsonDoc["name"] = "iot-sensor-2";
  jsonDoc["place_id"] = "32347983"; //42343243
  jsonDoc["date"] = NTP.getTimeDateString(time(NULL), "%Y-%m-%dT%H:%M:%S"); // ISO 8601 format
  jsonDoc["timestamp"] = epochTime;

  JsonObject payload = jsonDoc.createNestedObject("payload");
  payload["temperature"] = temp;
  payload["humidity"] = humid;
  payload["pressure"] = pressure;
  payload["luminosity"] = analogval;

  char jsonData[512];
  serializeJson(jsonDoc, jsonData);

  // Export MQTT data
  client.publish("iot-frames", jsonData);

  Serial.print("Time:");
  Serial.print(NTP.getTimeDateString(time(NULL), "%Y-%m-%dT%H:%M:%S"));
  Serial.println("TimeStamp:");
  Serial.println(epochTime);
  Serial.println("");
}
```
