# Swerve Modülü

## Swerve Modülü Konfigürasyonu (`module/x.json`)

Swerve modülü konfigürasyonu, her swerve modülünün benzersiz özelliklerini yapılandırır. [`SwerveModuleConfiguration`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/SwerveModuleConfiguration.java) oluşturmak için kullanılan [`ModuleJson.java`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/json/ModuleJson.java) ile 1:1 eşleşir. Bu konfigürasyon dosyası doğrudan swerve kinematiği ile etkileşime girer.

## Alanlar

| İsim                      | Birimler                                                                | Gerekli | Açıklama                                                                                                                                                                                                 |
| ------------------------- | ----------------------------------------------------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `drive`                   | [Device](../../configuring-yagsl/configuration/device-configuration.md) | E       | Sürüş motoru cihaz konfigürasyonu.                                                                                                                                                                       |
| `angle`                   | [Device](../../configuring-yagsl/configuration/device-configuration.md) | E       | Açı motoru cihaz konfigürasyonu.                                                                                                                                                                         |
| `encoder`                 | [Device](../../configuring-yagsl/configuration/device-configuration.md) | E       | Mutlak enkoder cihaz konfigürasyonu.                                                                                                                                                                     |
| `inverted`                | [MotorConfig](swerve-module.md#motorconfig)                             | E       | Boolean olarak her motorun ters çevrilme durumu.                                                                                                                                                         |
| `absoluteEncoderOffset`   | Derece                                                                  | E       | Derece cinsinden 0'dan mutlak enkoder ofseti. Negatif bir sayı olması gerekebilir.                                                                                                                       |
| `absoluteEncoderInverted` | Bool                                                                    | H       | Mutlak Enkoderin ters çevrilme durumu.                                                                                                                                                                   |
| `location`                | [Location](swerve-module.md#location)                                   | E       | İnç cinsinden robotun merkezinden swerve modülünün konumu. +x robotun önüne doğrudur ve +y robotun soluna doğrudur.                                                                                      |
| `conversionFactor`        | [MotorConfig](swerve-module.md#motorconfig)                             | H       | _GEÇERSİZ KILMA (OVERRIDE)_ [`swervedrive.json`](https://github.com/BroncBotz3481/YAGSL/wiki/Swerve-Drive) içindeki bu ayarı geçersiz kılmak için kullanılan, yerleşik PID için motor kontrolcüsüne uygulanan dönüşüm faktörü |

#### MotorConfig

| İsim    | Birimler | Gerekli | Açıklama        |
| ------- | -------- | ------- | --------------- |
| `drive` | Değer    | E       | Sürüş motoru değeri. |
| `angle` | Değer    | E       | Açı motoru değeri.   |

#### Location

| İsim    | Birimler | Gerekli | Açıklama                                         |
| ------- | -------- | ------- | ------------------------------------------------ |
| `front` | Değer    | E       | İleri yönde robot merkezinden modüle inç.        |
| `left`  | Değer    | E       | Sol yönde robot merkezinden modüle inç.          |
