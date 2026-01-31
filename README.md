# FramPartitionManager (AlphaAlpha - not yet published)

[![CRA Status](https://img.shields.io/badge/CRA-Exempt%20(pure%20OSS)-informational)](./CRA-EXEMPTION.md)
[![Attention – Alpha Version](https://img.shields.io/badge/Attention-Alpha%20Version-red?style=flat-square)](https://github.com/dein-benutzer/dein-repo#readme)

**Author:** Thomas Walloschke (<artkeller@gmx.de>)  
**License:** MIT  
**Platform:** ESP32-C3 (I2C-FRAM MB85RC256V)  
**Version:** 1.0.0

## Übersicht

`FramPartitionManager` ist eine Arduino-kompatible Bibliothek für die sichere Partitionierung und Verwaltung von I2C-FRAMs, z. B. des Fujitsu MB85RC256V.  
Die Bibliothek unterstützt:

- Partitionstabelle mit mehreren Einträgen
- CRC32-Schutz für Header und Nutzdaten
- AES-Verschlüsselung auf Wunsch (basierend auf MAC-Adresse)
- Schreibschutz-Flags je Partition
- Backup & Restore via SD-Karte oder Serial (CSV oder Binär)
- TLV-artiges Mini-Dateisystem mit JSON-Unterstützung
- Automatisches Längen-Tracking bei Schreiboperationen

## Features

- Partition anlegen, lesen, schreiben, kopieren, exportieren
- Serial Interface für Setup und Diagnose
- AES128 optional aktivierbar
- Backup/Restore im Serial- oder SD-Modus
- Kleiner Dateizähler (Dateisystem-light)

## Abhängigkeiten

Diese Bibliothek nutzt:

- [AESLib](https://github.com/DavyLandman/AESLib)
- [CRC32](https://github.com/bakercp/CRC32)
- SD.h für Backup auf SD-Karte (ESP32 intern)

## Beispiel

```cpp
#include <FramPartitionManager.h>

FramPartitionManager framManager(Wire, 0x50);

void setup() {
  Serial.begin(115200);
  framManager.begin();
  framManager.createPartition("config", 128, true);
  framManager.writeToPartition("config", (uint8_t*)"hello", 5);
}
