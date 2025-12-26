---
description: Kaymaya (drift) bir swerve sürüşünde her şey ve herhangi bir şey neden olabilir...
---

# Swerve Sürüş Kayması

Swerve sürüş kayması yıllardır ısrarcı bir sorun olmuştur ve neden olduğu konusunda birçok tartışma yapılmıştır. Bu sayfa, swerve sürüş kaymasının 3 yaygın neden kategorisi boyunca size rehberlik edecektir. Bu sorunların BİRÇOĞUNUN robotunuzda mevcut olabileceğini akılda tutmak önemlidir.

## Donanım

### Kablolama

Yanlış kablolama, swerve sürüşü için 3 kategoriye ayrılabilir. Bunlar, kablolamanın aşınmış, yanlış yönlendirilmiş veya bir yerde kopuk (özellikle konnektörlerde!) olması durumundaki belirtilerdir.

#### Enkoder

* [ ] Telemetri okumaları düzensiz ve anlamsız olacaktır.
* [ ] Motor kontrolden çıkabilir.
* [ ] Sürücü istasyonu konsolunda hatalar görünebilir.

#### Motor Kontrolcüsü

* [ ] Telemetrinin güncellenmesi yavaş olabilir.
* [ ] Motorlar aniden durabilir veya kontrolden çıkabilir.
* [ ] Motorlar komutlara yanıt vermeyebilir.
* [ ] Sürücü istasyonu konsolunda hatalar görünebilir.

#### Jiroskop/IMU

* [ ] Telemetrinin güncellenmesi yavaş olabilir.
* [ ] Alana Göre (Field Relative) robot kontrolü kullanılamaz olabilir.
* [ ] Otonom kontrolsüzce kayar.
* [ ] Sürücü istasyonunda hatalar görünebilir.
* [ ] Jiroskopunuz şiddetli bir şekilde hareket ediyor/sarsılıyorsa.
* [ ] Hareket sırasında jiroskopunuz kaydıysa.

### Fiziksel Bileşenler

#### Manyetik Enkoder

* [ ] Mıknatıs swerve modülüne sabitlenmemiş ve hareket halindeyken kayıyor.
  * Mıknatıs sabitlenene kadar mutlak enkoder ofsetlerinin sürekli olarak yeniden ayarlanması gerekir.
* [ ] Manyetik enkoder swerve modülüne sabitlenmemiş.

#### Motor

* [ ] Motorun swerve modül miline sağlam bir bağlantısı olmayabilir.
  * Bir amper limiti ayarlanmışsa motor çalışırken "seğirebilir" (twitch).
* [ ] Motor ölüyor.
  * Motor aynı hızları elde etmek için daha fazla amper çekiyor olabilir.

#### Swerve Modülü

* [ ] Tekerlekleriniz yanlış hizalanmışsa.
* [ ] Modüller aynı PID ile tutarsız.
  * Dişlilere gres uygulanması gerekebilir.

#### Robot

* [ ] Robot ağırlık merkezi ideal değil.

## Yazılım

* [ ] Kodunuzun diğer bölümleri nedeniyle sürekli `Command Scheduler loop overruns` (Komut Zamanlayıcı döngü aşımları).
* [ ] Maksimum fiziksel hız doğru ayarlanmamış.
* [ ] Açık döngü kullanılıyorsa, modüller farklı hızlarda çalışır.
* [ ] Kontrolcü giriş filtrelemesi.
* [ ] [`SwerveDrive.setCosineCompensator`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setCosineCompensator\(boolean\)) kullanımı
* [ ] [`SwerveDrive.setHeadingCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setHeadingCorrection\(boolean\)) kullanımı
* [ ] [`SwerveModule.setAntiJitter`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html#setAntiJitter\(boolean\)) kullanımı
* [ ] [`SwerveDrive.chassisVelocityCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#chassisVelocityCorrection) kullanımı
* [ ] [`SwerveDrive.setMaximumSpeeds`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setMaximumSpeeds\(double,double,double\)) kullanımı
* [ ] [`SwerveDrive.replaceSwerveModuleFeedforward`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#replaceSwerveModuleFeedforward\(edu.wpi.first.math.controller.SimpleMotorFeedforward\)) kullanımı
* [ ] [`SwerveDrive.setGyroOffset`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setMaximumSpeeds\(double,double,double\)) kullanımı
* [ ] [`SwerveDrive.updateCacheValidityPeriods`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#updateCacheValidityPeriods\(long,long,long\)) kullanımı
* [ ] [`SwerveDrive.setOdometryPeriod`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setOdometryPeriod\(double\)) kullanımı
* [ ] [`SwerveDrive.addVisionMeasurement`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#addVisionMeasurement\(edu.wpi.first.math.geometry.Pose2d,double\)) kullanımı
* [ ] `SwerveDrive.setChassisDiscretization` kullanımı

### PathPlanner

* [ ] PathPlanner `AutoBuilder` PID'leri iyi ayarlanmamış.
* [ ] Maksimum modül hızı çok yüksek veya çok düşük.
* [ ] Test yolu kavisli.
* [ ] PathPlanner otosu önceden ayarlanmış pozu (preset pose) tanımlamaz.
* [ ] PathPlanner yolu başlangıçta odometriyi sıfırlamaz.

## Konfigürasyon

* [ ] Modül konumları doğru tanımlanmamış.
  * Bunların robotun merkezinden modülün merkezine olduğunu unutmayın!
* [ ] Swerve Modül konfigürasyonları Mutlak Enkoder, Açı Motoru veya Sürüş motoru için doğru tanımlara sahip değil.
* [ ] Swerve modül konfigürasyon dosyalarında tanımlanan dönüşüm faktörü `physicalproperties.json` içindekinden farklı.
  * Swerve modül dosyalarındaki dönüşüm faktörleri tamamen **İSTEĞE BAĞLIDIR** ve bir nedeniniz olmadıkça tanımlanmaları gerekmez. Fazlalıktan kaçınmak için bunları yalnızca kodda tanımlamalı veya `physicalproperties.json` kullanmalısınız.
* [ ] Dönüşüm faktörü doğru değil.
  * Swerve sürüşünüzün pathplanner ile sürekli olması gerekenden daha uzağa gittiğini görüyorsanız muhtemelen durum budur.
  * Açı motorlarınız modülü asla doğru hizalamıyorsa bu da bunun bir nedeni olabilir.
* [ ] Sürüş ve dümenleme/azimut/açı motoru PID'leri yeterince iyi ayarlanmamış.
* [ ] Amper limiti çok düşük.
* [ ] [Öteleme ekseni robot oryantasyonu ile değişiyor.](the-eight-steps.md)
