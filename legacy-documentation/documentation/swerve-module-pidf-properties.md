# Swerve Modülü PIDF Özellikleri

## Swerve Modülü PID Konfigürasyonu (`pidfpropreties.json`)

Bu dosya, her swerve modülü için sürüş ve motor modüllerinin integral bölgesi ve maksimum çıktısı ile PIDF değerlerini yapılandırır. [`PIDFPropertiesJson.java`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/json/PIDFPropertiesJson.java) ile 1:1 eşleşir ve `SwerveDriveConfiguration` nesnesi başlatılırken kullanılır.

## Alanlar

| İsim    | Birimler                                                                                                                | Gerekli | Açıklama                                                            |
| ------- | ----------------------------------------------------------------------------------------------------------------------- | ------- | ------------------------------------------------------------------- |
| `drive` | [Integral Bölgesi ve Çıkış limiti ile PIDF](../../configuring-yagsl/configuration/pidf-properties-configuration/pidf.md) | E       | Sürüş motorundaki PIDF için kullanılacak konfigürasyon.             |
| `angle` | [Integral Bölgesi ve Çıkış limiti ile PIDF](../../configuring-yagsl/configuration/pidf-properties-configuration/pidf.md) | E       | Açı motorundaki PIDF için kullanılacak konfigürasyon.               |
