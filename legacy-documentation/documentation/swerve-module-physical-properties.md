# Swerve Modülü Fiziksel Özellikleri

## Swerve Modülü Fiziksel Özellikleri (`physicalproperties.json`)

Bu JSON, tüm Swerve Modülleriyle paylaşılan fiziksel özellikleri yapılandırır. [`SwerveModulePhysicalCharacteristics.java`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/SwerveModulePhysicalCharacteristics.java) oluşturan [`PhysicalPropertiesJson.java`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/json/PhysicalPropertiesJson.java) ile 1:1 eşleşir.

## Alanlar

| İsim                             | Birimler                                                        | Gerekli | Açıklama                                                                                                     |
| -------------------------------- | --------------------------------------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------ |
| `conversionFactor`               | [MotorConfig](swerve-module-physical-properties.md#motorconfig) | H       | Yerleşik PID için motor kontrolcüsüne uygulanan dönüşüm faktörü.                                             |
| `optimalVoltage`                 | Voltaj                                                          | E       | Telafi edilecek ve ileri besleme (feedforward) hesaplamalarının temel alınacağı optimum voltaj.              |
| `currentLimit`                   | [MotorConfig](swerve-module-physical-properties.md#motorconfig) | H       | Motorlara uygulanacak AMPER cinsinden akım sınırı.                                                           |
| `rampRate`                       | [MotorConfig](swerve-module-physical-properties.md#motorconfig) | H       | Motorun 0'dan tam gaza geçmesi için geçen minimum saniye sayısı.                                             |
| `wheelGripCoefficientOfFriction` | Halı üzerinde Sürtünme Katsayısı                                | H       | Halı üzerindeki kavrama bandı sürtünme katsayısı. Pratik maksimum ivmeyi hesaplamak için kullanılır.         |

#### MotorConfig

| İsim    | Birimler | Gerekli | Açıklama          |
| ------- | -------- | ------- | ----------------- |
| `drive` | Sayı     | E       | Sürüş motoru değeri. |
| `angle` | Sayı     | E       | Açı motoru değeri.   |
