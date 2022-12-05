# RP2040_SD Library

[![arduino-library-badge](https://www.ardu-badge.com/badge/RP2040_SD.svg?)](https://www.ardu-badge.com/RP2040_SD)
[![GitHub release](https://img.shields.io/github/release/khoih-prog/RP2040_SD.svg)](https://github.com/khoih-prog/RP2040_SD/releases)
[![GitHub](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/khoih-prog/RP2040_SD/blob/main/LICENSE)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](#Contributing)
[![GitHub issues](https://img.shields.io/github/issues/khoih-prog/RP2040_SD.svg)](http://github.com/khoih-prog/RP2040_SD/issues)


<a href="https://www.buymeacoffee.com/khoihprog6" title="Donate to my libraries using BuyMeACoffee"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Donate to my libraries using BuyMeACoffee" style="height: 50px !important;width: 181px !important;" ></a>
<a href="https://www.buymeacoffee.com/khoihprog6" title="Donate to my libraries using BuyMeACoffee"><img src="https://img.shields.io/badge/buy%20me%20a%20coffee-donate-orange.svg?logo=buy-me-a-coffee&logoColor=FFDD00" style="height: 20px !important;width: 200px !important;" ></a>


---
---

## Table of Contents

* [Why do we need this RP2040_SD library](#why-do-we-need-this-rp2040_sd-library)
  * [Features](#features)
  * [Currently supported Boards](#currently-supported-boards)
* [Changelog](changelog.md)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
  * [Use Arduino Library Manager](#use-arduino-library-manager)
  * [Manual Install](#manual-install)
  * [VS Code & PlatformIO](#vs-code--platformio)
* [Examples](#examples)
  * [  1. CardInfo](examples/CardInfo)
  * [  2. DataLogger](examples/DataLogger)
  * [  3. DumpFile](examples/DumpFile)
  * [  4. Files](examples/Files)
  * [  5. ListFiles](examples/ListFiles)
  * [  6. NonBlockingWrite](examples/NonBlockingWrite)
  * [  7. ReadWrite](examples/ReadWrite)
* [Example ReadWrite](#example-readwrite)
  * [ 1. File ReadWrite.ino](#1-file-readwriteino)
* [Debug Terminal Output Samples](#debug-terminal-output-samples)
  * [ 1. CardInfo on MBED RaspberryPi Pico](#1-cardinfo-on-mbed-raspberrypi-pico)
  * [ 2. DumpFile on MBED RaspberryPi Pico](#2-dumpfile-on-mbed-raspberrypi-pico)
  * [ 3. ListFiles on MBED RaspberryPi Pico](#3-listfiles-on-mbed-raspberrypi-pico)
  * [ 4. ReadWrite on MBED RaspberryPi Pico](#4-readwrite-on-mbed-raspberrypi-pico)
  * [ 5. Files on MBED RaspberryPi Pico](#5-files-on-mbed-raspberrypi-pico)
  * [ 6. CardInfo on RASPBERRY_PI_PICO](#6-cardinfo-on-raspberry_pi_pico)
  * [ 7. DumpFile on RASPBERRY_PI_PICO](#7-dumpfile-on-raspberry_pi_pico)
  * [ 8. ListFiles on RASPBERRY_PI_PICO](#8-listfiles-on-raspberry_pi_pico)
  * [ 9. ReadWrite on RASPBERRY_PI_PICO](#9-readwrite-on-raspberry_pi_pico)
  * [10. Files on RASPBERRY_PI_PICO](#10-files-on-raspberry_pi_pico)
* [Debug](#debug)
* [Troubleshooting](#troubleshooting)
* [Issues](#issues)
* [TO DO](#to-do)
* [DONE](#done)
* [Contributions and Thanks](#contributions-and-thanks)
* [Contributing](#contributing)
* [License](#license)
* [Copyright](#copyright)

---
---

### Why do we need this [RP2040_SD library](https://github.com/khoih-prog/RP2040_SD)

## Features

This is an Arduino library for **RP2040-based SPI SD Cards**.

It's based on and modified from :

1. [Bill Greiman's SdFat library](https://github.com/greiman/SdFat)
2. [Adafruit SD library](https://github.com/adafruit/SD)

Have a look at [SdFat's README](https://github.com/greiman/SdFat/blob/master/README.md)

```
SdFat Version 2 supports FAT16/FAT32 and exFAT SD cards. It is mostly backward compatible with SdFat Version 1 for FAT16/FAT32 cards.

exFAT supports files larger than 4GB so files sizes and positions are type uint64_t for classes that support exFAT.

exFAT has many features not available in FAT16/FAT32.  exFAT has excellent support for contiguous files on flash devices and supports preallocation.

If the SD card is the only SPI device, use dedicated SPI mode. This can greatly improve performance.
```

This library was created as an effort to use SD Card while the `arduino-pico` core still has issue [**SD card FILE_WRITE issue** #214](https://github.com/earlephilhower/arduino-pico/issues/214), which has been fixed from core v1.8.6.

It's better to use the built-in [SD library](https://github.com/earlephilhower/arduino-pico/tree/master/libraries/SD) for [**Earle Philhower's arduino-pico core v1.8.6+**](https://github.com/earlephilhower/arduino-pico). 

But if you need to write codes to be used in both [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed) and [**Earle Philhower's arduino-pico core**](https://github.com/earlephilhower/arduino-pico) without having to modify the code, you can have the option to use this library.

---

### Currently supported Boards

1. RP2040-based boards such as **NANO_RP2040_CONNECT, RASPBERRY_PI_PICO, ADAFRUIT_FEATHER_RP2040 and GENERIC_RP2040**, etc. using either [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed) or [**Earle Philhower's arduino-pico core**](https://github.com/earlephilhower/arduino-pico).


---
---

## Prerequisites

1. [`Arduino IDE 1.8.19+` for Arduino](https://github.com/arduino/Arduino). [![GitHub release](https://img.shields.io/github/release/arduino/Arduino.svg)](https://github.com/arduino/Arduino/releases/latest)
2. [`Arduino mbed_rp2040 core 3.4.1+`](https://github.com/arduino/ArduinoCore-mbed) for Arduino (Use Arduino Board Manager) RP2040-based boards, such as **Arduino Nano RP2040 Connect, RASPBERRY_PI_PICO, etc.**. [![GitHub release](https://img.shields.io/github/release/arduino/ArduinoCore-mbed.svg)](https://github.com/arduino/ArduinoCore-mbed/releases/latest)
3. [`Earle Philhower's arduino-pico core v2.6.3+`](https://github.com/earlephilhower/arduino-pico) for RP2040-based boards such as **RASPBERRY_PI_PICO, ADAFRUIT_FEATHER_RP2040 and GENERIC_RP2040**, etc. [![GitHub release](https://img.shields.io/github/release/earlephilhower/arduino-pico.svg)](https://github.com/earlephilhower/arduino-pico/releases/latest)

---
---

## Installation

### Use Arduino Library Manager

The best and easiest way is to use `Arduino Library Manager`. Search for [**RP2040_SD**](https://github.com/khoih-prog/RP2040_SD), then select / install the latest version.
You can also use this link [![arduino-library-badge](https://www.ardu-badge.com/badge/RP2040_SD.svg?)](https://www.ardu-badge.com/RP2040_SD) for more detailed instructions.

### Manual Install

Another way to install is to:

1. Navigate to [**RP2040_SD**](https://github.com/khoih-prog/RP2040_SD) page.
2. Download the latest release `RP2040_SD-main.zip`.
3. Extract the zip file to `RP2040_SD-main` directory 
4. Copy whole `RP2040_SD-main` folder to Arduino libraries' directory such as `~/Arduino/libraries/`.

### VS Code & PlatformIO

1. Install [VS Code](https://code.visualstudio.com/)
2. Install [PlatformIO](https://platformio.org/platformio-ide)
3. Install [**RP2040_SD** library](https://registry.platformio.org/libraries/khoih-prog/RP2040_SD) by using [Library Manager](https://registry.platformio.org/libraries/khoih-prog/RP2040_SD/installation). Search for **RP2040_SD** in [Platform.io Author's Libraries](https://platformio.org/lib/search?query=author:%22Khoi%20Hoang%22)
4. Use included [platformio.ini](platformio/platformio.ini) file from examples to ensure that all dependent libraries will installed automatically. Please visit documentation for the other options and examples at [Project Configuration File](https://docs.platformio.org/page/projectconf.html)


---
---

### Examples 

 1. [CardInfo](examples/CardInfo)
 2. [DataLogger](examples/DataLogger)
 3. [DumpFile](examples/DumpFile)
 4. [Files](examples/Files)
 5. [ListFiles](examples/ListFiles)
 6. [NonBlockingWrite](examples/NonBlockingWrite)
 7. [ReadWrite](examples/ReadWrite)


---
---

### Example [ReadWrite](examples/ReadWrite)

#### 1. File [ReadWrite.ino](examples/ReadWrite/ReadWrite.ino)

https://github.com/khoih-prog/RP2040_SD/blob/c1c62cc86fcfac3f90614888e4aa41c409c5505e/examples/ReadWrite/ReadWrite.ino#L26-L167

---
---

### Debug Terminal Output Samples

#### 1. CardInfo on MBED RaspberryPi Pico

The following is the sample terminal output when running example [CardInfo](examples/CardInfo) on MBED RaspberryPi Pico using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed)

```cpp
Starting SD Card CardInfo on MBED RaspberryPi Pico
MBED RP2040_SD v1.0.1
Initializing SD card with SS = 5
SCK = 2
MOSI = 3
MISO = 4
Wiring is correct and a card is present.

Card type:         SDHC
Clusters:          982896
Blocks x Cluster:  64
Total Blocks:      62905344

Volume type is:    FAT32
Volume size (Kb):  31452672
Volume size (Mb):  30715
Volume size (Gb):  30.00
Initialization done.

Files found on the card (name, date and size in bytes): 
DATALOG.TXT		144
TEST.TXT		36
NEWTEST.TXT		36
NEWTEST1.TXT		18
MYDATA~1.TXT		0
NEWTEST2.TXT		54
NEWTEST3.TXT		54
NEWTEST4.TXT		72
NEWTEST0.TXT		297
NEWDATA.TXT		18
```

---

#### 2. DumpFile on MBED RaspberryPi Pico

The following is the sample terminal output when running example [DumpFile](examples/DumpFile) on MBED RaspberryPi Pico using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed)

```cpp
Starting SD Card DumpFile on MBED RaspberryPi Pico
MBED RP2040_SD v1.0.1
Initializing SD card with SS = 5
SCK = 2
MOSI = 3
MISO = 4
Initialization done.
====== Data ======
Testing RP2040 SD
====== Data ======
[SD] Closed " newdata.txt ", nfilecount =  0
```

---

#### 3. ListFiles on MBED RaspberryPi Pico

The following is the sample terminal output when running example [ListFiles](examples/ListFiles) on MBED RaspberryPi Pico using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed)

```cpp
Starting SD Card ListFiles on MBED RaspberryPi Pico
MBED RP2040_SD v1.0.1
Initializing SD card with SS = 5
SCK = 2
MOSI = 3
MISO = 4
Initialization done.
DATALOG.TXT		126
TEST.TXT		36
NEWTEST.TXT		36
NEWTEST1.TXT		18
MYDATA~1.TXT		0
NEWTEST2.TXT		54
NEWTEST3.TXT		54
NEWTEST4.TXT		72
NEWTEST0.TXT		297
Print Directory done!
writeData = Testing RP2040 SD
readData = Testing RP2040 SD
DATALOG.TXT		144
TEST.TXT		36
NEWTEST.TXT		36
NEWTEST1.TXT		18
MYDATA~1.TXT		0
NEWTEST2.TXT		54
NEWTEST3.TXT		54
NEWTEST4.TXT		72
NEWTEST0.TXT		297
NEWDATA.TXT		18
Print Directory done!
```

---

#### 4. ReadWrite on MBED RaspberryPi Pico

The following is the sample terminal output when running example [ReadWrite](examples/ReadWrite) on MBED RaspberryPi Pico using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed)


```cpp
Starting SD Card ReadWrite on MBED RaspberryPi Pico
MBED RP2040_SD v1.0.1
Initializing SD card with SS = 5
SCK = 2
MOSI = 3
MISO = 4
initialization done.
Writing to newtest0.txt ==> Testing writing to newtest0.txt
[SD] Closed " newtest0.txt ", nfilecount =  0
done.
Reading from newtest0.txt
===============
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
[SD] Closed " newtest0.txt ", nfilecount =  0
===============
```

---

#### 5. Files on MBED RaspberryPi Pico

The following is the sample terminal output when running example [Files](examples/Files) on MBED RaspberryPi Pico using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed)


```cpp
Starting SD Card Files on MBED RaspberryPi Pico
MBED RP2040_SD v1.0.1
Initializing SD card with SS = 5
SCK = 2
MOSI = 3
MISO = 4
Initialization done.
example.txt doesn't exist.
Creating example.txt
writeData = 0xDEADBEEF
[SD] Closed " example.txt ", nfilecount =  0
readData = 0xDEADBEEF
[SD] Closed " example.txt ", nfilecount =  0
example.txt exists.
Removing example.txt...
example.txt doesn't exist.
```

---
---

#### 6. CardInfo on RASPBERRY_PI_PICO

The following is the sample terminal output when running example [CardInfo](examples/CardInfo) on RASPBERRY_PI_PICO using [**arduino-pico core**](https://github.com/earlephilhower/arduino-pico)

```cpp
Starting SD Card CardInfo on RASPBERRY_PI_PICO
RP2040_SD v1.0.1
Initializing SD card with SS = 17
SCK = 18
MOSI = 19
MISO = 16
Wiring is correct and a card is present.

Card type:         SDHC
Clusters:          1965597
Blocks x Cluster:  32
Total Blocks:      62899104

Volume type is:    FAT32
Volume size (Kb):  31449552
Volume size (Mb):  30712
Volume size (Gb):  29.99
Initialization done.

Files found on the card (name, date and size in bytes): 
DATALOG.TXT		267
DEMO.TXT		360960
CANADA~1.JPG		11156
TEST.TXT		72
NEWTEST4.TXT		132
NEWTEST0.TXT		330
NEWDATA.TXT		54
```

---

#### 7. DumpFile on RASPBERRY_PI_PICO

The following is the sample terminal output when running example [DumpFile](examples/DumpFile) on RASPBERRY_PI_PICO using [**arduino-pico core**](https://github.com/earlephilhower/arduino-pico)


```cpp
Starting SD Card DumpFile on RASPBERRY_PI_PICO
RP2040_SD v1.0.1
Initializing SD card with SS = 17
SCK = 18
MOSI = 19
MISO = 16
Initialization done.
====== Data ======
Testing RP2040 SD
====== Data ======
[SD] Closed " newdata.txt ", nfilecount =  0
```

---

#### 8. ListFiles on RASPBERRY_PI_PICO

The following is the sample terminal output when running example [ListFiles](examples/ListFiles) on RASPBERRY_PI_PICO using [**arduino-pico core**](https://github.com/earlephilhower/arduino-pico)

```cpp
Starting SD Card ListFiles on RASPBERRY_PI_PICO
RP2040_SD v1.0.1
Initializing SD card with SS = 17
SCK = 18
MOSI = 19
MISO = 16
Initialization done.
DATALOG.TXT		249
DEMO.TXT		82432
CANADA~1.JPG		11156
TEST.TXT		72
NEWTEST4.TXT		132
NEWTEST0.TXT		330
NEWDATA.TXT		36
Print Directory done!
writeData = Testing RP2040 SD
readData = Testing RP2040 SD
DATALOG.TXT		267
DEMO.TXT		82432
CANADA~1.JPG		11156
TEST.TXT		72
NEWTEST4.TXT		132
NEWTEST0.TXT		330
NEWDATA.TXT		54
Print Directory done!
```

---

#### 9. ReadWrite on RASPBERRY_PI_PICO

The following is the sample terminal output when running example [ReadWrite](examples/ReadWrite) on RASPBERRY_PI_PICO using [**arduino-pico core**](https://github.com/earlephilhower/arduino-pico)

```cpp
Starting SD Card ReadWrite on RASPBERRY_PI_PICO
RP2040_SD v1.0.1
Initializing SD card with SS = 17
SCK = 18
MOSI = 19
MISO = 16
initialization done.
Writing to newtest0.txt ==> Testing writing to newtest0.txt
[SD] Closed " newtest0.txt ", nfilecount =  0
done.
Reading from newtest0.txt
===============
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
Testing writing to newtest0.txt
[SD] Closed " newtest0.txt ", nfilecount =  0
===============
```

---

#### 10. Files on RASPBERRY_PI_PICO

The following is the sample terminal output when running example [Files](examples/Files) on RASPBERRY_PI_PICO using [**arduino-pico core**](https://github.com/earlephilhower/arduino-pico)

```cpp
Starting SD Card Files on RASPBERRY_PI_PICO
RP2040_SD v1.0.1
Initializing SD card with SS = 17
SCK = 18
MOSI = 19
MISO = 16
Initialization done.
example.txt doesn't exist.
Creating example.txt
writeData = 0xDEADBEEF
[SD] Closed " example.txt ", nfilecount =  0
readData = 0xDEADBEEF
[SD] Closed " example.txt ", nfilecount =  0
example.txt exists.
Removing example.txt...
example.txt doesn't exist.
```

---
---

### Debug

Debug is enabled by default on Serial.

You can also change the debugging level (_RP2040_SD_LOGLEVEL_) from 0 to 4

```cpp
// These define's must be placed at the beginning before #include "RP2040_SD.h"
// _RP2040_SD_LOGLEVEL_ from 0 to 4
#define _RP2040_SD_LOGLEVEL_       0
```

---

### Troubleshooting

If you get compilation errors, more often than not, you may need to install a newer version of the core for Arduino boards.

Sometimes, the library will only work if you update the board core to the latest version because I am using newly added functions.


---
---

### Issues

Submit issues to: [RP2040_SD issues](https://github.com/khoih-prog/RP2040_SD/issues)

---

## TO DO

1. Search for bug and improvement.


---

## DONE

1. Basic SD-wrapper library for **RP2040-based boards, such as NANO_RP2040_CONNECT, RASPBERRY_PI_PICO, ADAFRUIT_FEATHER_RP2040 and GENERIC_RP2040**, using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed) or [**Earle Philhower's arduino-pico core**](https://github.com/earlephilhower/arduino-pico).
2. Add Version String 
3. Add Table of Contents
4. Add astyle using `allman` style. Restyle the library

---
---

### Contributions and Thanks

Many thanks for everyone for bug reporting, new feature suggesting, testing and contributing to the development of this library.

1. Based on and modified from the [Bill Greiman's SdFat library](https://github.com/greiman/SdFat) to add support to RP2040-based boards using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed) or [**Earle Philhower's arduino-pico core**](https://github.com/earlephilhower/arduino-pico).
2. Based on and modified from the [Adafruit SD library](https://github.com/adafruit/SD) to add support to RP2040-based boards using [**Arduino-mbed RP2040** core](https://github.com/arduino/ArduinoCore-mbed) or [**Earle Philhower's arduino-pico core**](https://github.com/earlephilhower/arduino-pico).



<table>
  <tr>
    <td align="center"><a href="https://github.com/greiman"><img src="https://github.com/greiman.png" width="100px;" alt="greiman"/><br /><sub><b>⭐️ Bill Greiman</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/adafruit"><img src="https://github.com/adafruit.png" width="100px;" alt="adafruit"/><br /><sub><b>⭐️ Adafruit</b></sub></a><br /></td>
  </tr> 
</table>

---

## Contributing

If you want to contribute to this project:

- Report bugs and errors
- Ask for enhancements
- Create issues and pull requests
- Tell other people about this library

---

### License

- The library is licensed under [MIT](https://github.com/khoih-prog/RP2040_SD/blob/main/LICENSE)

---

## Copyright

- (C) Copyright 2009 by William Greiman
- (C) Copyright 2010 SparkFun Electronics
- (C) Copyright 2021 by Khoi Hoang




