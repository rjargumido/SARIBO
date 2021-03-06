# Overview
  
**SARIBO** or ***Systematic and Automated Regulation of Irrigation systems for Backyard farming Operations*** is an internet-of-things (IOT) Irrigation System designed for Backyard Farming created using ESP8266 NodeMCU 12E v3 (LoLin). SARIBO is a waray-waray (Waray) term for "to water" especially for plants.

SARIBO contains two modules:

1. **SARIBO Leaf Module (SARIBO Leaf).** The SARIBO Leaf Module which controls the connected sensors and is placed on the field.
2. **SARIBO Root Module (SARIBO Root).** The SARIBO Root Module is the main controller module which controls the watering process, activation of relays for the pump and valves, water level among others.


# Stable Version

See the official stable version @ **[Official Stable Release SARIBO version 1.2.7](https://github.com/rjargumido/SARIBO/releases/tag/v.1.2.7)** Source codes for the module are available at the "*Releases*" folder.


# Pin Configuration

**Leaf Pin Configuration:**

| **Label** | **Pin** | **Part** |
| ------------- | ------------- | ------------- |
| VCC | VCC/VIN | All with VCC/VIN 5VDC+ |
| GND | Gnd | Ground Pin |
| A0 | A0, Analog | Soil Moisture Sensor |
| SCL | D1/GPIO 5 | RTC Module |
| SDA | D2/GPIO 4, PWM | RTC Module |
| CS | D8/GPIO 15, PWM | SD Card |
| SCK | D5/GPIO 14, PWM | SD Card |
| MOSI | D7/GPIO 13 | SD Card |
| MISO | D6/GPIO 12, PWM | SD Card |


# Root Diagram

![Root Fritzing Diagram](https://github.com/rjargumido/SARIBO/blob/master/Fritzing/Root%20Diagram.png)

# Leaf Diagram

![SARIBO Leaf Diagram (April 5, 2020 Design)](https://github.com/rjargumido/SARIBO/blob/master/Fritzing/SARIBO%20Leaf%20April%205%2C%202020%20Design.png)


# Hardware Requirements
The following are the hardware requirements for SARIBO:

| **Hardware** | **Description** |
| ------------- | ------------- |
| NodeMCU V3 ESP8266 ESP-12E (LoLin)  | Serves as the micro controller unit (MCU) that performs the functionality of the system. |
| 12V DC Plastic Solenoid Water Valve (Normally Closed) 1/2"| Used in opening individual Leaf Distribution Lines. |
| Plastic Water Flow Sensor 1/2" | Used to determine the water flow rate. |
| MicroSD Card Reader Module | Data logging functions. |
| 2, 4-Channel 5V Low Level Trigger 10A 250 VAC Relay with Optocoupler | Relays used in controlling the pump and other higher voltage devices. |
| DS3231 RTC Real Time Clock and EEPROM AT24C32 Module | Provides the date and time functionalities. |
| HC-SR04 Ultrasonic Ranging Sensor | Used in determining the water level in the tank/reservoir.  |
| Soil Moisture Sensor Module | Used in determining the soil moisture level. |
| 74HC595 Shift-Out Register | Additional output pins. |


# Software Requirements
The following are the software requirements for SARIBO:

| **Software** | **Specification** | **Description** |
| ------------- | ------------- | ------------- |
| Arduino IDE | Version 1.8.10 | Serves as the Integrated Development Environment (IDE) of the Arduino wherein codes during the development are written using the software. |
| ArduinoJSON Library for Arduino | Built using [<ArduinoJson.h> ArduinoJson Library version 6.14.1 by Benoit Blanchon](https://github.com/bblanchon/ArduinoJson). | An Arduino library used as the parser/decoder (serializer/deserializer) of data of the system that will be sent via the Wi-Fi communication of the modules of the system. |
| SD Library for Arduino | Built using [<SD.h> SD Library version 1.2.4 by Arduino.cc and SparkFun](https://www.arduino.cc/en/Reference/SD). | An Arduino library used for the data logging purposes. |
| SPI Library for Arduino | Built using [<SPI.h> Serial Peripheral Interface Library by Arduino](https://www.arduino.cc/en/Reference/SPI). | An Arduino library used for transferring data between microcontrollers and other small devices. |
| Real Time Clock (RTC) Library for Arduino | [<RTClib.h> Version 1.3.3 by AdaFruit](https://github.com/adafruit/RTClib) | Provides the functionality for the setting and accessing of date and time. |
| HCSR04 Ultrasonic Ranging Sensor Library for Arduino | Built using [<HCSR04.h> version 2.0.2 by gamegine](https://github.com/gamegine/HCSR04-ultrasonic-sensor-lib). | Provides the functionality for the control and use of the HCSR04 Ultrasonic Ranging Sensor Module used in determining the water level in the tank. |
| ESP8266 Board for Arduino | Version 2.6.3 by the ESP8266 Community [ESP8266 Libraries](https://github.com/esp8266/Arduino) and [ESP8266 Board](http://arduino.esp8266.com/stable/package_esp8266com_index.json). | Provides the Wi-Fi communication and Web Server functionality. |
| ESP8266 Wi-Fi Library for ESP8266 NodeMCU | <ESP8266WiFi.h> Based on WiFi.h from Arduino WiFi shield library. Copyright (c) 2011-2014 Arduino. Modified by Ivan Grokhotkov, December 2014. Provided in the esp8266 Arduino board. | This provides the functionality in configuring the network settings such as setting the network SSID, the SSID password, ports to be used, IP address, the subnet and other communication related settings. |
| ESP8266 Web Server Library for ESP8266 NodeMCU | <ESP8266WebServer.h> Copyright (c) 2014 Ivan Grokhotkov. Provided in the esp8266 Arduino board. | This provides the network router or the web server that serves as the address or the routes wherein date could be sent or retrieved. |


# Data Management Service
SARIBO does not implement any database management systems (DBMS) in managing its data. Data are managed through the use of [*ArduinoJson Library v6.14.1 by Benoit Blanchon*](https://arduinojson.org/v6/assistant/) and saving it in a plain text file (.txt).

Data Management Service is further divided into the following content flaggers:
1. **DMS-Meta-Data**
2. **DMS-FSS**
3. **DMS-Body**


**1. DMS-Meta-Data** The *DMS Meta-Data* contains the information about the file.

| **Data** | **Description** | **Sample Value** | **Data Type** |
| ------------- | ------------- | ------------- | ------------- |
| header | What data is stored in the file. | LEAF-SETTINGS | String |
| dmsversion | What DMS version is used. | 1.2.3 | String |
| dcreated | The date the file is created in local format. | April 1, 2020 | String |
| tcreated | The time the file is created in local format. | 16:05:32 | String |
| owner | Who created the file (user id). | ADMIN04072020160532 | String |
| dmodified | The date where the file is last modified. | April 1, 2020 | String |
| tmodified | The time where the file is last modified. | 16:22:47 | String |
| modifiedby | Who modified the file (user id). | ADMIN04072020162012 | String |
| umode | How the file is updated*. | SD-SIGNED | String |

**Update Mode:**
1. ***SD-SIGNED.*** Happens when the Leaf's MicroSD Card is inserted in to the Root's Leaf SD Setup Port.
2. ***NET-SIGNED*** Happens when the Leaf's Settings File (SysConfig.txt) is being updated automatically via the network during Leaf POST.



**2. DMS-FSS** The *DMS-FSS* or the Data Management Service - File Structuring Standard (as can be seen in the next chapter), are the file structuring scheme used in the current SARIBO device/version. DMS-FSS complies with the File Structuring Standard as can be seen in the next chapter.


| **Data** | **Description** | **Sample Value** | **Data Type** |
| ------------- | ------------- | ------------- | ------------- |
| device | SARIBO Module | LEAF | String |
| repdir | Replication directory name. | Replication | String |
| coredir | The Core Configuration Directory name. | System | String |
| logsdir | The POST Log directory name. | Logs | String |
| corefn | Core configuration file name. | CoreConfig.txt | String |



**3. DMS-Body** This contains all the data neccessary for the device (device @ DMS-FSS).

| **Data** | **Description** | **Sample Value** | **Data Type** |
| ------------- | ------------- | ------------- | ------------- |
| local | The Leaf's HID | 2J41F7FQ | String |
| root | The Root's HID | HSDOSSUR| String |
| ssid | SARIBO WiFi Access Point | SARIBO - NwSSU | String |
| key | WAP Password | 123456789 | String |
| host | Host IP Address | 192.168.4.1 | String |
| reqpath | URL Path | /requests/?data= | String |
| port | Port where requests is to be sent. | 80 | Integer |
| coredir | The core configuration directory. | 
| wut | The time when the Leaf module should wake up. | 6:00:00 | String
| maxdryness | Maximum soil dryness | 1001 | Integer |
| mindryness | Minimum soil dryness | 600 | Integer |
| idealmoist | Ideal soil moisture | 450 | Integer |


# File Structuring Standard
The SARIBO modules strictly follow file structuring schemes:

**Leaf File Structuring:**

    FileSystem:
    |
    +---Core
    |   |
    |   +--- "Source Codes for the Leaf Module"
    |
    +---Documentation
    |   |
    |   +--- SARIBO User Manual.pdf
    |
    +---Logs
    |   |
    |   +--- CSV
    |   |     |
    |   |     + --- "CSV-2J41F7FQ-00001.csv"
    |   |
    |   +--- POST
    |        |
    |        + --- "POST-2J41F7FQ-00001.txt"
    |
    +---Replication
    |   |
    |   +--- Logs
    |   |
    |   +--- Root
    |
    +---System
        |
        +--- CoreConfig.txt


**Root File Structuring:**

    FileSystem:
    |
    +---Core
    |    |
    |    +--- "Source Codes for the Leaf and Root Modules"
    |
    +---Documentation
    |    |
    |    +--- SARIBO User Manual.pdf
    |
    +---Leaf
    |    |
    |    +---"Leaf's Hardware Id"
    |        |
    |        +--- Configuration
    |        |
    |        +--- POST
    |
    +---Logs
    |    |
    |    +--- POST
    |
    +---System
         |
         +--- Resources
         |
         +---HID.txt
         |
         +---SysConfig.txt

**Note:**
1. ***HID.txt*** contains all Hardware Ids in the network. Database of Hardware Ids.
2. ***SysConfig.txt*** or the system configuration database contains all the settings of the Root module.



# Data Exchange Standard (DES)

The Data Exchange Standard (DES) is used as the core data exchange, transfer, response, and processing rules used to ensure that the data is being processed the same way throughout the system. It is further divided into five:

1. **Data Exchange Standard Guidelines** Is the set of rules and guidelines for the Data Exchange Standard.
2. **Exchange Table** Is the table used in exchanging requests and responses in the network.
3. **Requests Code** Are 2-digit integer code used for determining what type of request is being sent or data to be send.
4. **Request** Is the table used in a request.
5. **Response** Is a table used in response to a request.



**1. Data Exchange Standard Guidelines**

1. ***For every request, there should be a response.***
2. The Transaction Id has the format of: *leafHID-YYYYMMMDD-HHMMSS* e.g. HC7E9701-2020Apr1-70209
3. Hardware Ids should comply with the Hardware ID Management Service (HIMS).
4. The Date object is in the format: MMMM dd, YYYY e.g. April 1, 2020 without the zero padding in the day object.
5. The Time object is in the format: hh:mm:ss SS e.g. 7:02:09 AM with the zero padding on both minute and second objects only.
6. Request codes complies with the recent Request Code Table under the Data Exchange Standard.
7. For ****requests only***, all space characters ' ' should always be replaced with the plus character '+' for URI/URL compliance.


**2. Exchange Table**
The Exchange Table is the standard table used in exchanging requests and responses in the network.
Exchange Table v2.3 revision April 1, 2020


| **Data**  | **Description** | **Data Type** |
| ------------- | ------------- | ------------- |
| transid | the Transaction Id signed by the Requesting module | String |
| origin | The Hardware ID of the requesting module | String |
| destination | The Hardware ID of the destination module of the request | String |
| datesent | The current date of the requesting module | String |
| timesent | The current time of the requesting module | String |
| request | The request code | Integer |
| value | The value being exchange as a validation/required data | String |


**3. Requests Code**
The following are the request codes under Request Code Table v2.1 revision March 31, 2020:

| **Request Code**  | **Description** |
| ------------- | ------------- |
| 10 | General Leaf Distribution Line Response |
| 11 | Leaf Distribution Line, Open |
| 12 | Leaf Distribution Line, Close |
| 20 | Get Leaf Water Flow Rate Reading |
| 21 | Read current Leaf Water Flow Rate |
| 30 | Power Reading Only |
| 40 | Date and Time reading |
| 41 | Synchronize with Root Date and Time settings |
| 50 | Network Reading |
| 51 | Ping Request |
| 61 | Pull Root Settings |
| 62 | Pull Leaf Settings |
| 71 | Soil moisture reading only |
| 72 | Request for a Hardware ID |


**4. Request**
The following is a sample request:

| **Data** | **Content** |
| ------------- | ------------- |
| transid | HC7E9701-2020Apr1-70209 |
| origin | HC7E9701 |
| destination | RBF0928J |
| datesent | April 1, 2020 |
| timesent | 7:02:09 AM |
| request | 11 |
| value | 892 |

The above request generates a string value of:
*{"transid":"HC7E9701-2020Apr1-70209","origin":"HC7E9701","destination":"RBF0928J","datesent":"April+1,+2020","timesent":7:02:09+AM","request":11,"value":892"}*


**5. Response**
The following is a sample response to the above sample request:

| **Data** | **Content** |
| ------------- | ------------- |
| transid | HC7E9701-2020Apr1-70209 |
| origin | RBF0928J |
| destination | HC7E9701 |
| datesent | April 1, 2020 |
| timesent | 7:02:48 AM |
| request | 10 |
| value | Leaf01 Open Distribution Line request approved. |

The above request generates a string value of:
*{"transid":"HC7E9701-2020Apr1-70209","origin":"RBF0928J","destination":"HC7E9701","datesent":"April 1, 2020","timesent":7:02:48 AM","request":10,"value":"Leaf01 Open Distribution Line request approved."}*



# Hardware ID Management Service (HIMS)

The Hardware ID Management Service (HIMS) is the core function that process the naming of modules *(giving of hardware Id)*, and the decoding of HIDs present in the Data Exchange Table for the processing of requests.

**HIDs are 8 pseudo-random generated alphanumeric codes used to name modules for easier network data exchange.*** HIMS serves as the central registration authority of hardware Ids within a specific SARIBO network and ensures that generated HIDs only belongs to the network, and are uniquely generated.

**The Generate Hardware ID Algorithm**
The following is the algorithm used in generating HIDs:

1. To create a psuedo-random number, the randomSeed() in the setup() function is placed
2. Randomize between 0 & 1. If value is 1 store a psuedo-random uppercase alphabet character, otherwise a psuedo-random numeric character.
3. Repeat step #2 until 8 alphanumeric characters are generated.
4. Return the character array as a String

The source code for the generation of hardware id is here at [Generate Hardware Id](https://github.com/rjargumido/SARIBO/blob/master/Individual%20Systems/generateHardwareID/generateHardwareID.ino).


# Soil Moisture Reading Guidelines
The following is the algorithm employed in reading and processing of the soil moisture:

**1.** Read the soil moisture value once every second for one minute for accuracy and save it in a *long int* data type variable.

**2.** After 1 minute, compute the final soil moisture value and divide it by 60.

**3.** Load user soil moisture level configuration such as the *maxsoildryness*, *minsoildryness* and the *idealsoilmoist* values from SD card.

**4.** Perform additional processes based on the following:

   **a.** When the **final soil moisture is above the maximum soil dryness**, repeat reading of the soil moisture. ***Go to step 1***;
   **b.** When the **final soil moisture is between the maximum soil dryness and the minimum soil dryness** (*means that the soil is dry*), trigger the **OPEN distribution request**, ***Go to step 5***;
   **c.** When the **final soil moisture is between the minimum soil dryness and the ideal soil moisture** (*means that the soil is in the ideal soil moisture*),:
          **c.1.** Check if there is already a sent open distribution line request, if true, ***Go to step 6***, else, trigger the **Soil Moisture Reporting Only**;

**5.** After 4 minutes from the *OPEN distribution request*, ***repeat steps 1-4***;

**6.** Send **CLOSE distribution request**;

***Note:*** Always create a high verbosity log.
