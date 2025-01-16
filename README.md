# EmbeddedDevices_CAN_Theorie_Fellner_Princ_Pollak_Wallpach

MCP2515 CAN Controller auf Raspberry Pi Pico

## Projektübersicht

Das Ziel dieses Projekts ist die Implementierung der MCP2515 CAN-Bus-Schnittstelle auf einem Raspberry Pi Pico. Es umfasst die Einrichtung des benötigten Repositories, die Dokumentation des CAN-Controllers sowie die Nutzung eines Logic-Analyzers zur Übertragung und Analyse von Nachrichten auf dem CAN-Bus.

### Aufgabenbereiche:
- **GKü/GKv**: Dokumentation der Inbetriebnahme des Repositories, Code-Dokumentation und Erläuterung des CAN-Controllers.
- **EKü/EKv**: Einsatz eines Logic-Analyzers und Test der Nachrichtenübertragung auf dem CAN-Bus.

---

## Inhaltsverzeichnis

1. [Voraussetzungen](#voraussetzungen)
2. [Installation](#installation)
3. [Verwendete Bibliotheken und Templates](#verwendete-bibliotheken-und-templates)
4. [Code-Struktur](#code-struktur)
5. [Verwendung](#verwendung)
6. [Ressourcen](#ressourcen)
7. [Contributing](#contributing)
8. [Lizenz](#lizenz)

---

## Voraussetzungen

- **Hardware**:  
  - Raspberry Pi Pico  
  - MCP2515 CAN-Controller  
  - Logic-Analyzer zur Protokollüberwachung  
- **Software/Tools**:  
  - CMake  
  - ARM GCC Compiler  
  - OpenOCD  
  - Picotool (für Arch Linux verfügbar)  

---

## Installation

### 1. Raspberry Pi Pico SDK installieren

```bash
git clone https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init
echo export PICO_SDK_PATH=$PWD >> ~/.bashrc
source ~/.bashrc
```

### 2. Abhängigkeiten installieren

#### Debian-basierte Systeme:
```bash
sudo apt update && sudo apt install -y cmake make gcc g++ openssl libssl-dev cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib
```

#### Arch Linux:
```bash
sudo pacman -S arm-none-eabi-gcc arm-none-eabi-binutils arm-none-eabi-newlib cmake autoconf git
yay -S picotool openocd-picoprobe
```

#### macOS (HomeBrew):
```bash
brew install cmake
brew install gcc-arm-embedded
```

---

## Verwendete Bibliotheken und Templates

1. **[pico-template](https://github.com/raspberrypi/pico-template)**  
   Ein Template für die schnelle Entwicklung mit Raspberry Pi RP2040.  
2. **[adamczykpiotr/pico-mcp2515](https://github.com/adamczykpiotr/pico-mcp2515)**  
   Eine optimierte MCP2515 CAN-Bibliothek für den Raspberry Pi Pico.  
3. **[a-kipp/RP2040-CAN-Driver](https://github.com/a-kipp/RP2040-CAN-Driver)**  
   Ein Treiber für den MCP2515 CAN-Controller.  

---

## Code-Struktur

Der Quellcode ist so aufgebaut, dass er einfach kompiliert und getestet werden kann. Die wichtigsten Komponenten sind:  
- **`main.c`**: Hauptlogik der CAN-Bus-Kommunikation.  
- **`mcp2515.c`**: Schnittstellenfunktionen für den MCP2515 CAN-Controller.  
- **`CMakeLists.txt`**: Build-Konfiguration.  

---

## Verwendung

### 1. Projekt kompilieren
Stellen Sie sicher, dass die gewünschten Beispiele in der `CMakeLists.txt` Datei aktiviert sind:
```cmake
add_subdirectory(src)
```

Bauen Sie das Projekt:
```bash
mkdir build && cd build
cmake ..
make
```

### 2. Programm auf den Pico flashen
Setzen Sie den Pico in den BOOTSEL-Modus und mounten Sie ihn:
```bash
sudo mount /dev/sda1 /mnt/pico
sudo cp build/example.uf2 /mnt/pico
sync
```

### 3. CAN-Nachrichten senden und empfangen
Der Quellcode enthält Beispiele zur Initialisierung des MCP2515 und zum Senden/Empfangen von Nachrichten. Ein Logic-Analyzer kann verwendet werden, um die Kommunikation auf dem CAN-Bus zu überwachen.

---

## Quellen

### Raspberry Pi Pico
- [Offizielle Dokumentation](https://www.raspberrypi.com/documentation/microcontrollers/)  
- [Getting Started Guide](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)  

### CAN-Bibliotheken
- [adamczykpiotr/pico-mcp2515](https://github.com/adamczykpiotr/pico-mcp2515)  
- [a-kipp/RP2040-CAN-Driver](https://github.com/a-kipp/RP2040-CAN-Driver)  

### Weitere Ressourcen
- [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)  
- [FreeRTOS Demos](https://github.com/FreeRTOS/FreeRTOS-SMP-Demos/tree/main/FreeRTOS/Demo/CORTEX_M0%2B_RP2040)  

