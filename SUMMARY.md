# İçindekiler

* [Yet Another Swerve Document'a Hoş Geldiniz](README.md)
  * [Kaynaklar](readme/resources.md)

## Genel Bakış

* [Ne yapıyoruz](overview/what-we-do.md)
* [Özelliklerimiz](overview/our-features/README.md)
  * [Telemetri](overview/our-features/telemetry.md)
  * [Simülasyon](overview/our-features/simulation.md)
  * [Pose Kilitleme](overview/our-features/lock-pose.md)
  * [Maksimum Hız](overview/our-features/max-speed.md)
  * [Şasi Hızı Ayrıklaştırma](overview/our-features/chassis-speed-discretization.md)
  * [Görüntü Odometrisi](overview/our-features/vision-odometry.md)
  * [Başlık (Heading) Düzeltme](overview/our-features/heading-correction.md)
  * [Otomatik Merkezlenen Modüller](overview/our-features/auto-centering-modules.md)
  * [Ofset Yükleme (Offset Offloading)](overview/our-features/offset-offloading.md)
  * [Kosinüs Telafisi](overview/our-features/cosine-compensation.md)
  * [Modül Otomatik Senkronizasyonu](overview/our-features/module-auto-synchronization.md)
  * [Açısal Hız Telafisi](overview/our-features/angular-velocity-compensation.md)
* [Değişiklik Günlüğü](overview/changelog.md)
* [Java API](https://yet-another-software-suite.github.io/YAGSL/javadocs/)
* [Örnek Kod](https://github.com/Yet-Another-Software-Suite/YAGSL/tree/main/examples)
* [Konfigürasyon Oluşturucu](https://yet-another-software-suite.github.io/YAGSL/config_generator/)
* [💸 Bağışlar](https://yetanothersoftwaresuite.com/)
* [👕 Ürünler](https://yagsl.com/)
* [Discord](https://discord.gg/yass)

## Temel Bilgiler

* [Swerve Sürüşü](fundamentals/swerve-drive.md)
* [Swerve Modülleri](fundamentals/swerve-modules.md)

## Swerve Kurulumu

* [Önsöz](bringing-up-swerve/preface.md)
* [Swerve Bilgileri](bringing-up-swerve/swerve-information.md)
* [Jiroskobunuzu Kontrol Edin](bringing-up-swerve/check-your-gyroscope.md)
* [Motorlarınızı Kontrol Edin](bringing-up-swerve/check-your-motors.md)
* [İlk Konfigürasyonunuzu Oluşturma](bringing-up-swerve/creating-your-first-configuration.md)

## YAGSL Konfigürasyonu

* [Robotunuzu Tanıma](configuring-yagsl/getting-to-know-your-robot/README.md)
  * [Dişli Oranı](fundamentals/swerve-modules.md#conversion-factor)
* [Bağımlılık Kurulumu](configuring-yagsl/dependency-installation.md)
* [Konfigürasyon](configuring-yagsl/configuration/README.md)
  * [Swerve Sürüş Konfigürasyonu](configuring-yagsl/configuration/swerve-drive-configuration.md)
  * [Fiziksel Özellikler Konfigürasyonu](configuring-yagsl/configuration/physical-properties-configuration.md)
  * [PIDF Özellikleri Konfigürasyonu](configuring-yagsl/configuration/pidf-properties-configuration/README.md)
    * [PIDF](configuring-yagsl/configuration/pidf-properties-configuration/pidf.md)
  * [Swerve Modül Konfigürasyonu](configuring-yagsl/configuration/swerve-module-configuration.md)
  * [Kontrolcü Özellikleri Konfigürasyonu](configuring-yagsl/configuration/controller-properties-configuration.md)
  * [Cihaz Konfigürasyonu](configuring-yagsl/configuration/device-configuration.md)
* [Kod Kurulumu](configuring-yagsl/code-setup.md)
* [Standart Dönüşüm Faktörleri](configuring-yagsl/standard-conversion-factors.md)
* [PIDF Nasıl Ayarlanır](configuring-yagsl/how-to-tune-pidf.md)
* [Ne Zaman Ters Çevrilmeli?](configuring-yagsl/when-to-invert.md)
* [Akış Şemaları](configuring-yagsl/flowcharts.md)
* [Sekiz Adım](configuring-yagsl/the-eight-steps.md)
* [Swerve Sürüş Kayması (Drift)](configuring-yagsl/swerve-drive-drift.md)
* [SparkMax ve SparkFlex Yaygın Sorunlar](configuring-yagsl/sparkmax-common-problems.md)
* [Modül Konumlarınızı Doğrulama](configuring-yagsl/verifying-your-module-locations.md)
* [Kaymayı (Drift) Ayarlama](configuring-yagsl/tuning-out-drift.md)

## Cihazlar

* [Jiroskop](devices/gyroscope.md)
  * [NavX](devices/gyroscope/navx.md)
  * [Pigeon](devices/gyroscope/pigeon.md)
  * [Pigeon 2.0](devices/gyroscope/pigeon-2.0.md)
  * [ADXRS450](devices/gyroscope/adxrs450.md)
  * [ADIS16448](devices/gyroscope/adis16448.md)
  * [ADIS16470](devices/gyroscope/adis16470.md)
* [Motor Sürücüler](devices/motor-controllers/README.md)
  * [SparkMAX](devices/motor-controllers/sparkmax.md)
  * [SparkFlex](devices/motor-controllers/sparkflex.md)
  * [TalonFX](devices/motor-controllers/talonfx.md)
* [Mutlak Enkoderler](devices/absolute-encoders.md)

## Analiz ve Hata Ayıklama

* [FRC Web Bileşenleri](analytics-and-debugging/frc-web-components.md)
* [Advantage Scope](analytics-and-debugging/advantage-scope.md)

## Ürün Kılavuzları

* [Java API](https://broncbotz3481.github.io/YAGSL/)
* [PathPlanner](https://pathplanner.dev/home.html)
* [❌ REV Hardware Client ile PID Ayarlama](product-guides/tuning-pid-with-rev-hardware-client.md)
* [❌ Sürüş Kodu](product-guides/drive-code.md)

## Eski Dokümantasyon

* [Dokümantasyon](legacy-documentation/documentation/README.md)
  * [JSON](legacy-documentation/documentation/json.md)
  * [Swerve Sürüşü](legacy-documentation/documentation/swerve-drive.md)
  * [Swerve Modülü](legacy-documentation/documentation/swerve-module.md)
  * [Swerve Modülü Fiziksel Özellikleri](legacy-documentation/documentation/swerve-module-physical-properties.md)
  * [Swerve Modülü PIDF Özellikleri](legacy-documentation/documentation/swerve-module-pidf-properties.md)
  * [Kontrolcü Özellikleri](legacy-documentation/documentation/controller-properties.md)
  * [Test Edilmiş Konfigürasyonlar](legacy-documentation/documentation/tested-configurations.md)
