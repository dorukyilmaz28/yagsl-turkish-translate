# Swerve Drive

## Swerve Drive (`swervedrive.json`)

Swerve Drive JSON konfigürasyon dosyası, genel Swerve Drive ile ilgili her şeyi yapılandırır. [`SwerveDrive`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/SwerveDrive.java) nesnesini oluşturmak için kullanılan bir [`SwerveDriveConfiguration`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/SwerveDriveConfiguration.java) oluşturan [`SwerveDriveJson.java`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/json/SwerveDriveJson.java) ile 1:1 eşleşir.

## JSON Alanları

| İsim          | Birimler                                                                | Gerekli | Açıklama                                                             |
| ------------- | ----------------------------------------------------------------------- | ------- | -------------------------------------------------------------------- |
| `imu`         | [Device](../../configuring-yagsl/configuration/device-configuration.md) | E       | Robotun yönünü belirlemek için kullanılan robot IMU'su.              |
| `invertedIMU` | Boolean                                                                 | E       | IMU'nun ters çevrilme durumu.                                        |
| `modules`     | String dizisi                                                           | E       | Sol ön taraftan başlayarak saat yönünde sırayla modül JSON'ları.     |
