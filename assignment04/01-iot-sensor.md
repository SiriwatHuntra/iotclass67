# Ingest and store real-time data from IoT sensors.

## MQTT Topic


## MQTT Payload


## ESP32


#include <Wire.h>
#include <Arduino.h>
#include <Adafruit_BMP280.h>
#include <SensirionI2cSht4x.h>
#include <Adafruit_Sensor.h>

Adafruit_BMP280 bmp280;
SensirionI2cSht4x sht4x;

#ifdef NO_ERROR
#undef NO_ERROR
#endif
#define NO_ERROR 0
static char errorMessage[64];
static int16_t error;

void setup() {

  Wire.begin(41, 40);
  Serial.begin(115200);

  if (bmp280.begin(0x76)) {  // prepare BMP280 sensor
    Serial.println("BMP280 sensor ready");
  }  

  bmp280.setSampling(Adafruit_BMP280::MODE_NORMAL,
                     Adafruit_BMP280::SAMPLING_X2,
                     Adafruit_BMP280::SAMPLING_X16,
                     Adafruit_BMP280::FILTER_X16,
                     Adafruit_BMP280::STANDBY_MS_500);

  sht4x.begin(Wire, SHT40_I2C_ADDR_44);
  sht4x.softReset();
  uint32_t serialNumber = 0;
  error = sht4x.serialNumber(serialNumber);
  if (error != NO_ERROR) {
      Serial.print("Error trying to execute serialNumber(): ");
      errorToString(error, errorMessage, sizeof errorMessage);
      Serial.println(errorMessage);
      return;
    }
    //Serial.print("serialNumber: ");
    //Serial.print(serialNumber);
    //Serial.println();
}

void loop() {

  Serial.print(F("Temperature = "));
  Serial.print(bmp280.readTemperature());
  Serial.println(" degC");
  Serial.print(F("Pressure = "));
  Serial.print(bmp280.readPressure());
  Serial.println(" Pa");

  float aTemperature = 0.0;
  float aHumidity = 0.0;
  error = sht4x.measureHighPrecision(aTemperature, aHumidity);
  if (error != NO_ERROR) {
      Serial.print("Error trying to execute measureLowestPrecision(): ");
      errorToString(error, errorMessage, sizeof errorMessage);
      Serial.println(errorMessage);
      return;
  }
  //Serial.print("aTemperature: ");
  //Serial.print(Temperature);
  //Serial.print("\t");
  Serial.print("Humidity: ");
  Serial.print(aHumidity);
  Serial.println(" ");
  Serial.println(" ");

  delay(2000);
}


/*
light sensor io5 ADC_CH4
*/