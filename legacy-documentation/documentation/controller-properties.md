# Kontrolcü Özellikleri

## Swerve Kontrolcüsü (`controllerproperties.json`)

Swerve Kontrolcüsü, bir joystick'e dayalı olarak robotun yönünü ayarlayan otonom ve sürüş modları sırasında swerve sürüşünün nasıl çalıştığına ilişkin konfigürasyon seçeneklerini saklar. JSON dosyaları, bir [`SwerveControllerConfiguration`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/SwerveControllerConfiguration.java) oluşturan [`ControllerPropertiesJson.java`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/parser/json/ControllerPropertiesJson.java) ile 1:1 eşleşir. Otonom fonksiyonların çalışması için robot başlığı PID'sinin doğru şekilde ayarlanması gerektiğinden buradaki değerler otonom için **SON DERECE** önemlidir.

## Alanlar

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>angleJoystickRadiusDeadband</code></td><td>Double</td><td>E</td><td>Robotun yön ayarına izin vermek için açı kontrol joystick'inin minimum yarıçapı.</td></tr><tr><td><code>heading</code></td><td><a href="../../configuring-yagsl/configuration/pidf-properties-configuration/pidf.md">PID</a></td><td>E</td><td>Robot yönünü kontrol etmek için kullanılan PID.</td></tr></tbody></table>
