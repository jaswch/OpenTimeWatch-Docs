This guide is for people who want to manually configure the firmware settings via the PlatformIO IDE.

!!! note 

    This guide is not recommended for beginners please refer to the automatic version of this guide.

## Requirements
1. PlatformIO

## WiFi and Time configuration
Changes in ```src/osVariables/osVariables.cpp``` :-

1. To configure your WiFi network enter your SSID (network name) in line 40 
```const char* ssid  = "yourSSID";``` (replace
yourSSID with your network name) and in line 42 replace yourPassword with your network password ```const char* password = "yourPassword";```
2. To setup time enter the GMT offset of your region in line 46 ```const long  gmtOffset_sec = 0;``` and daylight offset
in line 48 ```const int   daylightOffset_sec = 0;``` and make sure both of them are in seconds. If you can't get the time
properly even after setting the GMT and daylight offset then you might have to change the URL of the NTP server to a URL
which is closer to your location in line 44 ```const char* ntpServer = "pool.ntp.org";```.
Below are a few common NTP server URLs:-
<br>

Area          | HostName
:-------------|:-------------------------
Asia          | asia.pool.ntp.org
Europe        | europe.pool.ntp.org
North America | north-america.pool.ntp.org
Oceania       | oceania.pool.ntp.org
South America | south-america.pool.ntp.org

## Configuration for TQT pro N4R2 (Flash: 4MB, PSRAM: 2MB)
Just upload the code without any changes to the ```platformio.ini``` file. It should look like this:
<br>
```ini title="platformio.ini" linenums="1"
; PlatformIO Project Configuration File


[platformio]
boards_dir = ./board
;default_envs = T-QT-Pro-N8
default_envs = T-QT-Pro-N4R2
description = Open source watch OS for ESP32 based watches

;[env:T-QT-Pro-N8]
[env:T-QT-Pro-N4R2]
platform = espressif32@6.6.0
board = esp32-s3-t-qt-pro
framework = arduino
build_flags = 
	-DBOARD_HAS_PSRAM
lib_deps = 
	lennarthennigs/Button2@^2.3.3
	adafruit/Adafruit GFX Library@^1.11.11
	adafruit/Adafruit MPU6050 @ ^2.0.3
    adafruit/Adafruit Unified Sensor @ ^1.1.4
```

Note:- PlatformIO is currently assuming we have total 1MB of flash and not detecting the PSRAM.


## Configuration for TQT pro N8 (Flash: 8MB, PSRAM: none)
You will need to do some changes in the ```platformio.ini``` file before uploading the code. It should look like this:
<br>
```ini title="platformio.ini" linenums="1"
; PlatformIO Project Configuration File


[platformio]
boards_dir = ./board
default_envs = T-QT-Pro-N8
;default_envs = T-QT-Pro-N4R2
description = Open source watch OS for ESP32 based watches

[env:T-QT-Pro-N8]
;[env:T-QT-Pro-N4R2]
platform = espressif32@6.6.0
board = esp32-s3-t-qt-pro
framework = arduino
build_flags = 
;	-DBOARD_HAS_PSRAM
lib_deps = 
	lennarthennigs/Button2@^2.3.3
	adafruit/Adafruit GFX Library@^1.11.11
	adafruit/Adafruit MPU6050 @ ^2.0.3
    adafruit/Adafruit Unified Sensor @ ^1.1.4
```

After configuring the firmware source code you can upload it to the watch.
