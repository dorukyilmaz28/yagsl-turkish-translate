# Değişiklik Günlüğü

## Pull Request'ler her zaman incelenir!

YAGSL'i daha iyi hale getirmeye yardımcı olmak isteyen herkesi, yaşam kalitenizi artıran yaptığınız değişikliklerle pull request oluşturmaya şiddetle teşvik ediyorum.

{% embed url="https://github.com/BroncBotz3481/YAGSL-Example/pulls?q=is%3Apr+is%3Aclosed" %}

## Katkıda Bulunma

YAGSL geliştirmesi `src/main/java/swervelib` adresindeki YAGSL-Example deposunun `dev` dalında yapılır.

{% embed url="https://github.com/BroncBotz3481/YAGSL-Example/tree/dev" %}
YAGSL-Example dev branch
{% endembed %}

Tüm PR'lar buraya dayanmalı ve burada birleştirilmelidir. YAGSL sık sık diğer depolara dağıtılır.

## 2025.8.0

* Fırçalı SparkMAX'ler ile bağlı mutlak enkoderleri düzelt

## 2025.7.2

* setAbsoluteEncoderOffset() düzeltildi, [@MEisSCAMMER](https://github.com/MEisSCAMMER) tarafından [#338](https://github.com/BroncBotz3481/YAGSL-Example/pull/338) ile
* omegaPIDController için Sürekli Giriş (Continuous Input) etkinleştirildi, [@Sate04](https://github.com/Sate04) tarafından [#337](https://github.com/BroncBotz3481/YAGSL-Example/pull/337) ile
* Etkinleştirilmiş (enabled) halde başlarken çökme sorunu yamalandı.

## 2025.7.1

* `SwerveInputStream.allianceRelativeControl` düzeltildi
* Robot kodu yeniden başlarsa maç ortasında çökme önlendi.
* `SwerveInputStream.translationHeadingOffset` eklendi
* YAGSL başlangıcından jiro sıfırlama kaldırıldı. Artık `autonomousInit` üzerinde jiro'yu sıfırlamanız veya `RobotModeTriggers` kullanmanız gerekiyor.
* Örnek koda `Added RobotModeTriggers.autonomous().onTrue(Commands.runOnce(this::zeroGyroWithAlliance));` eklendi.

## 2025.7.0

* [ ] Eski dönüştürme faktörleri yöntemi uyarı vermek yerine istisna (exception) fırlatır hale getirildi.
* [ ] TalonFXS Desteği eklendi.
* [ ] <kbd>SwerveMotor.isAttachedAbsoluteEncoder</kbd>, <kbd>SwerveMotor.usingExternalFeedbackSensor</kbd> olarak yeniden adlandırıldı.
* [ ] <kbd>SwerveDrive.pushOffsetsToEncoders</kbd>, <kbd>SwerveDrive.useExternalFeedbackSensor</kbd> lehine kullanımdan kaldırıldı (deprecated).
* [ ] <kbd>SwerveDrive.restoreInternalOffset</kbd>, <kbd>SwerveDrive.useInternalFeedbackSensor</kbd> lehine kullanımdan kaldırıldı (deprecated).
* [ ] Shuffleboard referansları herhangi bir dashboard olarak güncellendi, [@DanPeled](https://github.com/DanPeled) tarafından.
* [ ] SparkFlex'lere bağlı Mutlak Enkoderler düzeltildi.
* [ ] Bağlı mutlak enkoderler artık geri bildirim cihazı (feedback device) olarak ayarlanmıyor, açıkça çağrılması gerekiyor.
* [ ] `SwerveInputStream.driveToPose` eklendi
* [ ] İleri besleme (feedforward) kullanan sürüş fonksiyonuna isteğe bağlı modül durumları optimizasyonu eklendi, [@clrozeboom](https://github.com/clrozeboom) tarafından [#314](https://github.com/BroncBotz3481/YAGSL-Example/pull/314) ile
* [ ] Tüm kapatılabilir öğelerin `AutoClosable` arayüzünü uygulaması sağlandı, [@kytpbs](https://github.com/kytpbs) tarafından [#317](https://github.com/BroncBotz3481/YAGSL-Example/pull/317) ile
* [ ] Gereksiz importlar ve değişkenler kaldırıldı, [@kytpbs](https://github.com/kytpbs) tarafından [#318](https://github.com/BroncBotz3481/YAGSL-Example/pull/318) ile
* [ ] PIDFConfigs'den oluşturulan PIDController'ların IZone'u ayarlandı, [@CoffeeCoder1](https://github.com/CoffeeCoder1) tarafından [#319](https://github.com/BroncBotz3481/YAGSL-Example/pull/319) ile
* [ ] Yazım hatası düzeltildi, [@fletch3555](https://github.com/fletch3555) tarafından [#323](https://github.com/BroncBotz3481/YAGSL-Example/pull/323) ile
* [ ] DIO üzerinden Rev Through bore, [@wackyvert](https://github.com/wackyvert) tarafından [#325](https://github.com/BroncBotz3481/YAGSL-Example/pull/325) ile
* [ ] setMotorBrake'in sürekli çalışması durduruldu, [@rakosi2](https://github.com/rakosi2) tarafından [#327](https://github.com/BroncBotz3481/YAGSL-Example/pull/327) ile
* [ ] Kontrolcü başlık girdileri axisDeadband'ı geçmezse rotasyonu önle, [@MrFast-js](https://github.com/MrFast-js) tarafından [#328](https://github.com/BroncBotz3481/YAGSL-Example/pull/328) ile

## 2025.3.0

* [ ] Daha kolay hata ayıklama sağlamak için `SwerveDrive.setModuleStateOptimization` eklendi.
* [ ] `sparkmax_analog` düzeltildi
* [ ] Vizyon sonuçları olmadığında Null pointer çökmesi, [@jwt388](https://github.com/jwt388) tarafından [#307](https://github.com/BroncBotz3481/YAGSL-Example/pull/307) ile
* [ ] PigeonViaTalonSRX ve bağlı SparkFlex eklendi, [@konnorreynolds](https://github.com/konnorreynolds) tarafından [#292](https://github.com/BroncBotz3481/YAGSL-Example/pull/292) ile
* [ ] Modül konfigürasyonları yanlışlıkla 0 olarak ayarlandığında hata fırlat, [@wackyvert](https://github.com/wackyvert) tarafından [#308](https://github.com/BroncBotz3481/YAGSL-Example/pull/308) ile
* [ ] rawAbsoluteEncoder konumu düzeltildi, [@konnorreynolds](https://github.com/konnorreynolds) tarafından [#309](https://github.com/BroncBotz3481/YAGSL-Example/pull/309) ile

## 2025.2.2

* [ ] Hem vx hem de vy raporlaması için `swerve/measuredChassisSpeeds` düzeltildi.
* [ ] `SwerveInputStream.robotRelative` düzeltildi, Team 151 tarafından.
* [ ] `SwerveDrive.drive` `fieldOriented` parametresinin uygulanması düzeltildi. Hata team 2508'den WispySparks tarafından yakalandı!
* [ ] `SwerveInputStream.headingOffset` eklendi

## 2025.2.1

* [ ] Bağıl enkoder kullanan optimizasyon düzeltildi
* [ ] `SparkMaxSwerve.isAbsoluteEncoderAttached()` içindeki mutlak enkoder algılaması null kontrolü `Optional.isPresent()` olarak değiştirilerek düzeltildi (Team 217 tarafından keşfedildi!)
* [ ] SparkMax'ler için `absoluteEncoder`, `Optional` olarak değiştirildi (Team 217 tarafından)
* [ ] Kendi etrafında dönerken sysId yapma yolu eklendi, parametreler `SwerveDriveTest.setDriveSysIdRoutine(new Config(),this, swerveDrive, 12, true)` olarak değiştirildi

## 2025.2.0

* [ ] Sürüş motoru ileri beslemesi için kA varsayılan olarak devre dışı bırakıldı.
* [ ] İleri beslemede kullanılan getMaxVelocity düzeltildi, [@jwt388](https://github.com/jwt388) tarafından [#286](https://github.com/BroncBotz3481/YAGSL-Example/pull/286) ile
* [ ] Maksimum hız ayarlarının robotu tam hızdan daha azına sınırlamasına izin vermemesi, [@clrozeboom](https://github.com/clrozeboom) tarafından [#277](https://github.com/BroncBotz3481/YAGSL-Example/pull/277) ile
* [ ] Sim modülleri SysId rutinleri & Yeni maple-sim sürümü, [@catr1xLiu](https://github.com/catr1xLiu) tarafından [#288](https://github.com/BroncBotz3481/YAGSL-Example/pull/288) ile

## 2025.1.3

* [ ] `Adjusted IMU Yaw` düzeltildi ve `SmartDashboard` altında yayınlanacak şekilde ayarlandı
* [ ] Modül çıktısına simülasyon hızları ve okumaları eklendi.
* [ ] Tek başına bir TalonSRX'e bağlı SRX Mag Enkoderleri için `srxmag_standalone` mutlak enkoder tipi eklendi.

## 2025.1.2

* [ ] WPILib 2025.1.1'e güncellendi
* [ ] CTRE/REV/Studica/Redux vendordep'leri güncellendi.
* [ ] Bazı javadocs hataları düzeltildi.
* [ ] Yorumlar düzenlendi, [@yapplejack](https://github.com/yapplejack) tarafından [#278](https://github.com/BroncBotz3481/YAGSL-Example/pull/278) ile

## 2025.1.1

* [ ] Telemetri yayınlama sorunu düzeltildi. Telemetri artık `SmartDashboard` ağ tablosu altında yayınlanıyor.
* [ ] Robot etkinken SparkMAX veya SparkFlex konfigürasyonu değişiklikleri yapıldığında hata fırlat.
* [ ] Örnek kod, sürüş motoru boşta kalma modunu (idle mode) ayarlamayacak şekilde değiştirildi.
* [ ] ThirftyNova desteği eklendi.
* [ ] `SwerveInputStream.robotRelative` ve `SwerveInputStream.allianceRelativeControl` eklendi

## 2025.1.0.1

* [ ] SparkMAX ve SparkFlex için konfigürasyon yedekliliği (redundancy) eklendi.
* [ ] driveWithSetpointGenerator için döngü süresini düzelt ve alan yönelimli kontrol kullan ([#271 ](https://github.com/BroncBotz3481/YAGSL-Example/pull/271) @[**jwt388**](https://github.com/jwt388) tarafından**)**
* [ ] Telemetriye döngü süreleri eklendi.
* [ ] Telemetri, yalnızca `SwerveDriveTelemetry.updateSettings` `true` olduğunda ayarları gönderecek şekilde optimize edildi.
* [ ] SparkMAX ve SparkFlex için yeniden deneme gecikmesi 10ms'den 5ms'e düşürüldü.
* [ ] Anında (on the fly) konfigürasyon gecikmesi 100ms'den 10ms'e düşürüldü.
* [ ] Başlangıç (init) sonrası anında konfigürasyon gecikmesi için uyarı eklendi.
* [ ] `SimpleMotorFeedForward.calculate`, yalnızca hızı kullanacak şekilde düzeltildi. Bu ne yazık ki ivmeyi yok sayar.
* [ ] `SmartDashboard.put`, NT4 Publisher'lara değiştirildi
* [ ] Kütüphane hız alımları lehine `IMUVelocity` kaldırıldı.
* [ ] `SwerveIMU.getRate()` -> `SwerveIMU.getYawAngularVelocity()` olarak yeniden adlandırıldı ve bir `AngularVelocity` nesnesi döndürmesi sağlandı.
* [ ] Kolay kontrolcü dönüşümleri için `SwerveInputStream` nesnesi eklendi.

## 2025.1.0

* [ ] Vizyon dosyası null-ptr istisnası düzeltildi.
* [ ] Maple-Sim 0.2.4'e güncellendi; `SwerveDrive.getMapleSimDrive()` eklendi, [@catr1xLiu](https://github.com/catr1xLiu) tarafından [#262](https://github.com/BroncBotz3481/YAGSL-Example/pull/262) ile
* [ ] Spark max fırçalı motor kontrolcüsü enkoder null-ptr istisnaları düzeltildi
* [ ] `SwerveMath.scaleTranslation` sorunu düzeltildi
* [ ] `resultLists` kontrolü ile `Vision` güncellemesi düzeltildi, @jwt388 FRC Team 151 tarafından
* [ ] `SwerveDrive.getMaximumVelocity()` -> `SwerveDrive.getMaximumChassisVelocity()` olarak değiştirildi
* [ ] `SwerveDrive.getMaximumAngularVelocity()` -> `SwerveDrive.getMaximumChassisAngularVelocity()` olarak değiştirildi
* [ ] Sürüş motoru ileri beslemesini hesaplamak için bilinen motor tipleri kullanıldı.
* [ ] Ayrıştırıcı (parser), motor kontrolcüsüne bağlı motor tipini bilecek şekilde genişletildi. (Fırçalı hariç)
* [ ] Şasi maksimum hızı modül maksimum hızından ayrıldı.
* [ ] `navx_mxp_serial` geri eklendi.
* [ ] Motor belirticileri eklendi: `krakenx60foc`, `krakenx60`, `falcon500foc`, `falcon500`, `sparkmax_neo550`, `sparkmax_neo`, `sparkflex_neo`, `sparkflex_vortex`, `sparkflex_neo550`
* [ ] Sürüş motoru ileri beslemesi `SwerveModule` yapıcısında (constructor) oluşturuldu.
* [ ] Modül maksimum hızları `SwerveModule.maxDriveVelocity` ve `SwerveModule.maxAngularVelocity`'ye eklendi
* [ ] Web konfigürasyonu güncellendi

## 2025.0.0

* [ ] AHRS imu değişkeni kurucu kapsamı (scope) bittikten sonra kayboluyor, [@clrozeboom](https://github.com/clrozeboom) tarafından [#254](https://github.com/BroncBotz3481/YAGSL-Example/pull/254) ile
* [ ] Maple-Sim Ekle, [@catr1xLiu](https://github.com/catr1xLiu) tarafından [#251](https://github.com/BroncBotz3481/YAGSL-Example/pull/251) ile
* [ ] kA desteği uygula, [@Etaash-mathamsetty](https://github.com/Etaash-mathamsetty) tarafından [#258](https://github.com/BroncBotz3481/YAGSL-Example/pull/258) ile
* [ ] WPILIb 2025 Beta-2'ye güncelle, [@thenetworkgrinch](https://github.com/thenetworkgrinch) tarafından [#257](https://github.com/BroncBotz3481/YAGSL-Example/pull/257) ile
* [ ] Talon SRX'e entegre mutlak enkoder desteği ekle, [@WispySparks](https://github.com/WispySparks) tarafından [#208](https://github.com/BroncBotz3481/YAGSL-Example/pull/208) ile
* [ ] DCMotor modelleme kullanarak Path Planner DriveFeedForward uygulandı, [@catr1xLiu](https://github.com/catr1xLiu) tarafından [#260](https://github.com/BroncBotz3481/YAGSL-Example/pull/260) ile
* [ ] NavX ters çevirme (inversion) düzeltildi.
* [ ] Team 457 Grease Monkeys yardımıyla MAXSwerve'de Mutlak Enkoder sorunu düzeltildi

## 2024.7.0 - 2024 WPILib için son sürüm

* [ ] SparkMAX ve SparkFlex'e ters çevirme yedeklilik (redundancy) kontrolü eklendi.
* [ ] Yol Bulma (Pathfinding) için Isınma (Warmup) Ekle (PR [#241](https://github.com/BroncBotz3481/YAGSL-Example/pull/241), [TechnologyMan00](https://github.com/Technologyman00) tarafından)

## 2024.6.1.0

* [ ] `Canandgyro` desteği eklendi.
* [ ] Örnek swerve alt sistemi kodundaki hoparlöre nişan alma komutunda küçük bir hata düzeltmesi (PR [#239](https://github.com/BroncBotz3481/YAGSL-Example/pull/239), [catr1xLiu](https://github.com/catr1xLiu) tarafından)

## 2024.6.0.0

* [ ] Swerve konfigürasyon test değişikliklerini birleştir (PR [#228](https://github.com/BroncBotz3481/YAGSL-Example/pull/228), [**clrozeboom**](https://github.com/clrozeboom) tarafından**)**
* [ ] Açısal hız düzeltmesi (YAGSL'i büyük ölçüde iyileştiren dev güncelleme!) (PR [#231](https://github.com/BroncBotz3481/YAGSL-Example/pull/231), [yapplejack](https://github.com/yapplejack) tarafından)
* [ ] Sparkmax optimizasyonları, avg filter değişiklikleri vb. (PR [#233](https://github.com/BroncBotz3481/YAGSL-Example/pull/233), [**yapplejack**](https://github.com/yapplejack) tarafından**)**
* [ ] Geçerli bir mutlak enkoder tipi olarak `sparkmax_analog5v` eklendi.
* [ ] desaturateWheelSpeeds() için desiredChassisSpeeds kullanma önerisi (PR [#232](https://github.com/BroncBotz3481/YAGSL-Example/pull/232), [**yapplejack**](https://github.com/yapplejack) tarafından**)**
* [ ] Otomatik senkronizasyon `SwerveDrive.setModuleEncoderAutoSynchronize` ile isteğe bağlı ve yapılandırılabilir hale getirildi
* [ ] `TalonFXSwerve` için yapılandırıcı sorunu düzeltildi

## 2024.5.0.4

* [ ] Örneğe PhotonVision `Vision` sınıfı eklendi ve örnek kodla entegre edildi.
* [ ] `Vision`'a `getAprilTagPose` yöntemi eklendi (PR [#226](https://github.com/BroncBotz3481/YAGSL-Example/pull/226), [**kreidljj**](https://github.com/kreidljj) tarafından)
* [ ] `Vision.updatePoseEstimation` üzerindeki vizyon simülasyonunu güncelle (PR [#224](https://github.com/BroncBotz3481/YAGSL-Example/pull/224), [**brandonzx3**](https://github.com/brandonzx3) tarafından**)**
* [ ] YAGSL SwerveDrive Poz Tahmincisi için Standart Sapmalar Ekle (PR [#222](https://github.com/BroncBotz3481/YAGSL-Example/pull/222), [**maxikyuu**](https://github.com/maxikyuu) tarafından**)**
* [ ] Vendordep'leri Güncelleme ve CanandCoder'ları CanandMag olarak yeniden adlandırma (PR [#219](https://github.com/BroncBotz3481/YAGSL-Example/pull/219), [**Turbojax07**](https://github.com/Turbojax07) ve YAGSL geliştiricileri tarafından)
* [ ] `SwerveDriveTelemetry` ile ilgili dokümantasyon sorunu düzeltildi (Issue [#233 ](https://github.com/BroncBotz3481/YAGSL-Example/issues/223), [**DanPeled**](https://github.com/DanPeled) tarafından )
* [ ] SparkMAX'e bağlı Throughbore gibi Mutlak Enkoderler düzeltildi.

## 2024.5.0.3

* [ ] `SparkMaxAnalogEncoder` sarmalayıcısının çalışması düzeltildi. Beklenen okuma değerleri volt cinsindendir, maks 3.3v. (Team 2377'den team Austin tarafından bulundu ve düzeltildi)
* [ ] Ürün yeniden adlandırması nedeniyle `CanandCoder` -> `CanandMag` olarak değiştirildi. ([TurboJax07](https://github.com/Turbojax07)'e teşekkürler)
* [ ] `SwerevDrive.pushOffsetsToEncoders` çağrılmadan bağlı bir mutlak enkoderi ayarlamanın varsayılan davranışı değiştirildi. Bu artık bir gereklilik yerine MAX Swerve modülleri için isteğe bağlı bir optimizasyondur. MAX Swerve artık `SwerveDrive.pushOffsetsToEncoders` kullanmıyorlarsa dönüşüm faktörü olarak `360` kullanmak zorunda değiller.

## 2024.5.0.1

* [ ] `SwerveDrive.setVisionMeasurementStdDevs(Matrix<N3, N1> visionMeasurementStdDevs)` eklendi
* [ ] IMU'dan dönüş oranını alma yeteneği ekle (PR [#216](https://github.com/BroncBotz3481/YAGSL-Example/pull/216), [@clrozeboom](https://github.com/clrozeboom) tarafından)

## 2024.5.0.0

* [ ] Girdi ölçeklendirmesi Polar koordinat büyüklüğü çarpımını kullanacak şekilde değiştirildi.
* [ ] placeInAppropriate0To360Scope basitleştirildi (PR [#213](https://github.com/BroncBotz3481/YAGSL-Example/pull/213), [GoldenStack](https://github.com/GoldenStack) tarafından)
* [ ] Otomatik merkezlenen modüller ayarı eklendi.
* [ ] Kompozit dönüşüm faktörleri geri eklendi.

## 2024.4.8.7

* [ ] Saha ve veriler için günlük (logging) modlarını tanıtmak amacıyla günlük ayrıntı düzeyi artırıldı. (PR [#185](https://github.com/BroncBotz3481/YAGSL-Example/pull/185), [5010](https://github.com/5010TigerDynasty) tarafından)
* [ ] Döngü süreleri arasında ayrık değerin değiştirilmesine izin vermek için `SwerveDrive.setChassisDiscretization` eklendi, bu kaymayı (drift) azaltmak için ayarlanabilir. (PR [#194](https://github.com/BroncBotz3481/YAGSL-Example/pull/194), [TechnologyMan00](https://github.com/Technologyman00) tarafından)
* [ ] `SwerveDrive.pushOffsetsToControllers` -> `SwerveDrive.pushOffsetsToEncoders` olarak yeniden adlandırıldı. (PR [#194](https://github.com/BroncBotz3481/YAGSL-Example/pull/194), [TechnologyMan00](https://github.com/Technologyman00) tarafından)
* [ ] Telemetride `Module[...]`, `swerve/modules` olarak değiştirildi.

## 2024.4.8.6

* [ ] `SwerveModule.getDrivePIDF` ve `SwerveModule.getAnglePIDF` ile birlikte PIDF yardımcı fonksiyonları `SwerveModule.setDrivePIDF` ve `SwerveModule.setAnglePIDF` eklendi.
* [ ] İleri besleme, doğrudan `SwerveModule.feedforward`'ı değiştirmek yerine `SwerveModule.setFeedforward` kullanacak şekilde değiştirildi
* [ ] `SwerveModule.feedforward`, `SwerveModule.driveFeedforward` olarak yeniden adlandırıldı.
* [ ] Motor kontrolcülerine gönderilen enkoder ofsetlerini de değiştiren `SwerveModule.setAntiJitter` aracılığıyla anti-jitter devre dışı bırakma seçeneği eklendi.
* [ ] Vendordep'ler güncellendi

## 2024.4.8.5

* [ ] NavX ters çevirme durumunun robot üzerinde herhangi bir etki yaratmaması düzeltildi.

## 2024.4.8.4

* [ ] Anti jitter, kosinüs telafisinden önce çalışacak şekilde güncellendi.

## 2024.4.8.3

* [ ] `Pigeon2Swerve`, CAN zaman aşımlarını işlemek yerine `imu.getRotation3d()` kullanacak şekilde güncellendi.
* [ ] Gerekli bellek ayak izi büyük ölçüde azaltıldı. ([@TheGamer1002](https://github.com/TheGamer1002) yardımıyla)

## 2024.4.8.2

* [ ] CTRE bekleme durumu süreleri, kullanıcı modifikasyonu için statik hale getirildi. `CANCoderSwerve.STATUS_TIMEOUT_SECONDS`, `TalonFXSwerve.STATUS_TIMEOUT_SECONDS` ve `Pigeon2Swerve.STATUS_TIMEOUT_SECONDS` istenen kullanım durumu için değiştirilebilir.

## 2024.4.8.1

* [ ] İstenildiği gibi kosinüs telafisini etkinleştirip devre dışı bırakabilen `SwerveDrive.setCosineCompensation` fonksiyonu eklendi, gerçek robotlarla olan tutarsızlıklar nedeniyle simülasyonda varsayılan olarak devre dışıdır.

## 2024.4.8

* [ ] SysId desteği eklendi. (PR [#160](https://github.com/BroncBotz3481/YAGSL-Example/pull/160) ve [#165](https://github.com/BroncBotz3481/YAGSL-Example/pull/165), [Team 5010](https://github.com/5010TigerDynasty) tarafından)
* [ ] Varsayılan 20ms zaman aşımları ile `refresh` yerine `waitForStatusUpdate` kullanılır.
* [ ] İşlemeyi hızlandıracak ve CAN kullanımını azaltacak bir `validityPeriod` boyunca değişkenleri önbelleğe almak için `Cache` sınıfı eklendi.
* [ ] Kullanıcının önbellek geçerlilik süresini istediği gibi değiştirebilmesi için `SwerveDrive.updateCacheValidityPeriods` eklendi.
* [ ] Tüm `SwerveModule`'leri, anahtarın `.json` olmayan modül dosya adı olduğu bir HashMap olarak getirecek `SwerveDrive.getModuleMap()` eklendi, böylece `frontleft.json`, `frontleft` anahtarına sahip olur.

## 2024.4.7

* [ ] İstenen hız 0 ise modüller önceki konumda kalacaktır.
* [ ] Kosinüs telafisi artık beklendiği gibi telemetri yoluyla raporlanıyor.

## 2024.4.6.3

* [ ] Başlık düzeltmesi `getYaw()` yerine `getOdometryHeading()` kullanacak şekilde güncellendi (PR [#150](https://github.com/BroncBotz3481/YAGSL-Example/pull/150), [@Blargleflakes](https://github.com/Blargleflakes) tarafından). Bu, `controllerproperties.json` içindeki başlık düzeltme PID değerlerini etkiler ve bu değerlerin 50 kat artırılması GEREKEBİLİR.
* [ ] Konfigürasyon dosyaları aracılığıyla kosinüs dengeleyiciyi devre dışı bırakma yeteneği eklendi. (PR [#148](https://github.com/BroncBotz3481/YAGSL-Example/pull/148), [@fovea1959](https://github.com/fovea1959) tarafından)
* [ ] `SwerveIMU` döndürmek için `SwerveDrive.getGyro()` eklendi.
* [ ] SysId ile gelecekteki kullanım için `SwerveMotor` sarmalayıcısına `SwerveMotor.setVoltage` ve `SwerveMotor.getVoltage` ve `SwerveMotor.getAppliledOutput` eklendi.
* [ ] Tüm swerve modül motorlarının voltajını ayarlamayı test etmek için fonksiyonlar eklendi.
* [ ] Tüm swerve modüllerinin kuplaj oranını bulmak için fonksiyon eklendi.
* [ ] Tüm swerve modüllerinin steering/azimuth/angle (açı) ayarını yapmak için fonksiyon eklendi.
* [ ] Sürüş motorlarının hareket etmesi için kV bulma fonksiyonu eklendi.
* [ ] Açı motoru bağıl enkoder konumu, dönüşüm faktörünü değiştirdikten SONRA ayarlandı. (Issue [#155](https://github.com/BroncBotz3481/YAGSL-Example/issues/155))
* [ ] Modüle `maxSpeed` göndererek modül açık döngü kontrolü düzeltildi. (@nstrike ve [@MarshallTappen](https://github.com/MarshallTappen) tarafından)
* [ ] Yalnızca X ivmesini kullanan Pigeon2Swerve düzeltildi (PR [#146](https://github.com/BroncBotz3481/YAGSL-Example/pull/146#event-11577147896), [@dezash123](https://github.com/dezash123) tarafından)
* [ ] `absoluteEncoderOffset` ayarlanmadığında sürüş motorlarının hareket etmesi önlendi. ([@fovea1959](https://github.com/fovea1959) tarafından bulundu)
* [ ] `SwerveDrive.addVisionMeasurement` için javadoclar en son değişiklikleri yansıtacak şekilde güncellendi.

## 2024.4.6.1

* [ ] `SwerveDrive.resetOdometry` düzeltildi ve bunun yerine poz tahmini kullanıldı. (PR [#142](https://github.com/BroncBotz3481/YAGSL-Example/pull/142), [@MarshallTappen](https://github.com/MarshallTappen) ve @nstrike tarafından [commit](https://github.com/BroncBotz3481/YAGSL-Example/commit/039e5c2867690cfdd5ebd0c1e84eefc6b165adee))
* [ ] IMU ters çevirmesi işlevselleştirildi (PR [#140](https://github.com/BroncBotz3481/YAGSL-Example/pull/140), [@TechnologyMan00](https://github.com/Technologyman00) ve @nstrike tarafından)
* [ ] `SwerveDrive.getOdometryHeading()` eklendi
* [ ] Vizyon standart sapmaları ile `SwerveDrive.addVisionMeasurement` düzeltildi.
* [ ] `Raw IMU Yaw` (ters çevirme uygulanmış jiro) ve `Adjusted IMU Yaw` (poz tahmini rotasyonu) aracılığıyla SmartDashboard'a IMU okumaları eklendi.
* [ ] MXP üzerinden seri olduğunu belirtmek için `navx_mxp`, `navx_mxp_serial` olarak değiştirildi.
* [ ] `navx_mxp_serial` veya `navx_usb` kullanılırken uyarı eklendi.
* [ ] Tekerlek hızı doygunluk giderme (desaturation) geri eklendi.

## 2024.4.6

* [ ] `SwerveMath.calculateDegreesPerRotation` ve `SwerveMath.calculateMetersPerRotation`, enkoder çözünürlüğünü hariç tutacak ve bir varsayılan ekleyecek şekilde basitleştirildi.
* [ ] `Module[...] Raw Motor Encoder`, `Module[...] Raw Angle Encoder` olarak değiştirildi.
* [ ] `Module[...] Raw Drive Encoder` eklendi

## 2024.4.5

* [ ] TalonFX Açı motor kontrolü için düzeltme ([@bhall-ctre](https://github.com/bhall-ctre) ve @Wackyvert 2225 Mentor tarafından) .
  1. TalonFX'lerin dönüşüm faktörünü dişli oranı + birim dönüşümü yerine dişli oranı olarak kullanması gerekiyordu.
  2. Dönüşüm faktörünün tersine çevrilmesi gerekiyordu.
  3. setPosition güncellemesi mevcut konumu yansıtacak şekilde.
* [ ] `ma3` enkoderleri analog giriş üzerinden okunacak şekilde değiştirildi. ([@CoZm0](https://github.com/CoZ-m0) tarafından keşfedildi)
* [ ] PathPlanner yardımcı fonksiyonu ile 3 tekerlekli swerve modül kurulumları desteklendi. (PR #139, [@TechnologyMan00](https://github.com/Technologyman00) tarafından)
* [ ] `SwerveModule.getAbsoluteEncoder()`, `SwerveDrive.getMaximumVelocity()` ve `SwerveDrive.getMaximumAngularVelocity()` eklendi.
* [ ] Uyumlu bir Tuner X yapılandırması kullanıldığında Tuner X öner.
* [ ] Başlık düzeltme ölü bandını (deadband) değiştirebilme özelliği eklendi.

## 2024.4.2

* [ ] SparkMAX'lere ileri besleme (feedforward) eklendi.
* [ ] Ağ Uyarıları Eklendi ([ @TheGamer1002](https://github.com/TheGamer1002) PR [#136](https://github.com/BroncBotz3481/YAGSL-Example/pull/136) tarafından yapıldı)
* [ ] TalonFX'lere ileri besleme eklendi
* [ ] TalonFX dönüşüm faktörü düzeltildi ([@jkbo6](https://github.com/jbko6) PR [#128](https://github.com/BroncBotz3481/YAGSL-Example/pull/128) tarafından yapıldı)
* [ ] CanAndCoder ince ayarları ([@guineahawk](https://github.com/guineawheek) PR [#134](https://github.com/BroncBotz3481/YAGSL-Example/pull/134) tarafından yapıldı)
* [ ] Eksik SparkMAX durum çerçeveleri eklendi ([@RoboPenguin7](https://github.com/RoboPenguin7) PR [#130](https://github.com/BroncBotz3481/YAGSL-Example/pull/130) tarafından yapıldı)
* [ ] Daha az hassas hale getirmek için Başlık Düzeltme güncellemesi ([@balien-12](https://github.com/balien-12) PR [#132](https://github.com/BroncBotz3481/YAGSL-Example/pull/132) tarafından yapıldı)
* [ ] Kosinüs dengeleyici hatası düzeltildi ([@jkbo6](https://github.com/jbko6) PR [#129](https://github.com/BroncBotz3481/YAGSL-Example/pull/129) tarafından yapıldı)
* [ ] İttifaka dayalı PathPlanner yolu güncellendi ([@MarshalTappen](https://github.com/MarshallTappen) PR [#122](https://github.com/BroncBotz3481/YAGSL-Example/pull/122) tarafından yapıldı)
* [ ] Rotasyonun kapalı olması düzeltildi, getDriveBaseMeters güncellemesi ([@TechnologyMan00](https://github.com/Technologyman00) tarafından yapıldı)
