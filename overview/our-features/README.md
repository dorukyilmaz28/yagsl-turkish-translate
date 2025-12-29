# Özelliklerimiz

## Dokümantasyon

{% embed url="https://broncbotz3481.github.io/YAGSL/" %}
YAGSL için Javadocs
{% endembed %}

{% embed url="https://broncbotz3481.github.io/YAGSL-Example/" %}
Konfigürasyonları oluşturmak için ayarlama (tuning) web sayfası
{% endembed %}

{% embed url="https://github.com/BroncBotz3481/YAGSL-Example" %}
Örnek kod deposu
{% endembed %}

## Kolay kurulum

Sadece bu listeden tüm vendordep'leri WPILib online'dan indirin: [#vendor-urls](../../configuring-yagsl/dependency-installation.md#vendor-urls "mention") ve şu adresteki süreci izleyin:

{% embed url="https://docs.wpilib.org/en/stable/docs/software/vscode-overview/3rd-party-libraries.html#rd-party-libraries" %}

## Donanım Desteği

### Motorlar

* [Neo](https://www.revrobotics.com/rev-21-1650/)
* [Falcon 500](https://store.ctr-electronics.com/falcon-500-powered-by-talon-fx/) / [Kraken X60](https://wcproducts.com/products/kraken)
* [SparkMAX tarafından kontrol edilen Fırçalı Motorlar](https://www.andymark.com/products/rs775-5-motor-with-encoder-for-pg71-pg188-gearbox) ile [bağlı](https://www.mouser.com/ProductDetail/Grayhill/63R256) [bir](https://store.ctr-electronics.com/srx-mag-encoder/) [enkoder](https://www.revrobotics.com/rev-11-1271/). Açı motorları quadrature enkoder gerektirmez ve spark max'in veri portuna bağlı duty cycle enkoderler kullanmalıdır.

### Mutlak Enkoderler

* [Thrifty Absolute Encoders](https://www.thethriftybot.com/bearings/Thrifty-Absolute-Magnetic-Encoder-p421607500)
* [CANCoder](https://store.ctr-electronics.com/cancoder/)
* [REV Through Bore](https://www.revrobotics.com/rev-11-1271/)
* [Canandcoder (SparkMAX üzerinden)](https://docs.reduxrobotics.com/canandcoder/spark-max#using-the-pwm-output-with-spark-max)
* [Canandcover (CAN üzerinden)](https://docs.reduxrobotics.com/canandcoder/getting-started)
* [Throughbore](https://www.revrobotics.com/rev-11-1271/) (PWM üzerinden)
* [Thrifty Absolute Magnetic Encoder](https://www.thethriftybot.com/products/thrifty-absolute-magnetic-encoder) (AnalogInput üzerinden)
* [MA3](https://www.andymark.com/products/ma3-absolute-encoder-with-cable)
* [SRX Mag](https://store.ctr-electronics.com/srx-mag-encoder/)
* [AM Mag](https://www.andymark.com/products/am-mag-encoder)
* Herhangi bir PWM Mutlak Enkoder!
* Herhangi bir Analog Mutlak Enkoder

### IMU'lar (Jiroskoplar)

#### Tüm jiroskoplarda, saat yönünün tersi (counter-clockwise) pozitif yön olarak tanımlanmalıdır.

* [Pigeon IMU](https://store.ctr-electronics.com/pigeon-2/)
* [Pigeon 2 IMU](https://store.ctr-electronics.com/pigeon-2/)
* [NavX](https://www.studica.com/nav2-mxp-robotics-navigation-sensor)
* [NavX 2](https://www.studica.com/nav2-mxp-robotics-navigation-sensor)
* [NavX Micro](https://www.studica.com/navx-2-micro-9-axis-inertialmagnetic-sensor)
* [NavX 2 Micro](https://www.studica.com/navx-2-micro-9-axis-inertialmagnetic-sensor)
* [ADIS16448](https://wiki.analog.com/first/adis16448_imu_frc)
* [ADIS16470](https://wiki.analog.com/first/adis16470_imu_frc)
* Herhangi bir analog jiroskop

## Simülasyon

* `YAGSl-Example` ek bir yapılandırma gerektirmeden tam simülasyon desteği ile birlikte gelir.

## Kontrol

* PathPlanner desteklenir ve `YAGSL-Example` içinde bir örnek vardır.
* Kontrol, tamamen mevcut açıya kıyasla istenen açıya dayalı olabilir (`SwerveController.getTargetSpeeds`) veya doğrudan doğru birimlerle `SwerveDrive`'a iletilebilir.
* `SwerveDrive.lockPose` fonksiyonu robotu neredeyse hareket ettirilemez hale getirmek için tüm tekerlekleri içe bakacak şekilde hareket ettirir.
* Sürüş motorları `SwerveDrive.setMotorIdleMode` fonksiyonu kullanılarak coast (serbest) veya brake (fren) moduna ayarlanabilir.
* Swerve Modülü sürüş motoru feedforward (ileri besleme) değerleri `SwerveDrive.replaceSwerveModuleFeedforward` fonksiyonu kullanılarak değiştirilebilir.
* Robotun kontrolünü iyileştirmek için `SwerveController.getTargetSpeeds`'e `SwerveController.addSlewRateLimiters` ile slew rate limiter'lar eklenebilir.
* Robotun hızını sınırlamak ve devrilmeyi önlemek için uzaydaki nesneleri kullanan Momentum hesaplayıcısı `Matter` sınıfı ile temsil edilir.
* CAN trafiği, sadece değişen açı ve hız değerleriyle sınırlandırılmıştır.
* `SwerveDrive.setMaximumSpeed` ve `SwerveController.setMaximumAngularVelocity` veya `SwerveDrive.setMaximumSpeeds` yardımcı fonksiyonları ile maksimum hızları üzerine yazma (overwrite) yeteneği.
* Sadece `SwerveDrive.drive` fonksiyonlarını etkileyen `SwerveDrive.chassisVelocityCorrection` kullanarak Şasi Hız Düzeltmesi kullanma yeteneği.
* `SwerveDrive.drive` ile farklı dönüş merkezleri kullanarak kontrol yeteneği.
* Ofsetleri motor kontrolcülerine `SwerveDrive.pushOffsetsToControllers` ile gönderme.
* `SwerveDrive.setChassisSpeedsDisctretization` aracılığıyla `ChassisSpeeds.discretize` üzerinde kontrol.
* `SwerveDrive.setCosineCompensator` aracılığıyla kosinüs telafisi.
* `SwerveDrive.setHeadingCorrection` ile başlık (heading) düzeltmesi.
* Otomatik merkezlenen modüller, girdi verilmediğinde modüllerin 0'a merkezlenmesini sağlar. Bu, `SwerveDrive.setAutoCenteringModules` ile kontrol edilebilir.

## Güvenlik Özellikleri

* Mutlak enkoder okumada bir hata ile karşılaşırsa, mutlak enkoder okumaları bağıl enkoder okumalarına geri döner.
* Açı motorları, motorları korumaya yardımcı olmak için varsayılan olarak coast (serbest) modundadır.
* Motor açıları en yakın eşdeğer açıya dönecek şekilde optimize edilmiştir.
* `SwerveMath.limitVelocity` içinde robot ağırlığınıza ve ağırlık merkezinize göre hızınızı sınırlayabilirsiniz.
* JSON konfigürasyonunda akım limitleri.
* JSON konfigürasyonunda ramp rate (ivmelenme oranı) limitleri.
* Sadece SparkMAX'ler ve TalonFX'ler için motor kontrolcülerinde kapalı döngü (Closed-loop) PID.
* Robot 100ms boyunca hareket etmediğinde mutlak enkoderler ve bağıl enkoderler senkronize edilir.
* PID girdileri süreklidir veya -180 ile 180 arasında sürekli olacak şekilde emüle edilir.

## Odometri

* `SwerveDrive.updateOdometry` her 20ms'de bir çağrılır, periyot `SwerveDrive.setOdometryPeriod` ile değiştirilebilir.
* Odometri thread'ini durdurmak için `SwerveDrive.stopOdometryThread` kullanın ve odometriyi periyodik içinde güncelleyin.
* Jiroskobu sıfırlamak için `SwerveDrive.zeroGyro` çağırın.
* Robot merkezli hız `SwerveDrive.getRobotVelocity` ile ve alan merkezli hız `SwerveDrive.getFieldVelocity` ile alınabilir.
* Robot pozu `SwerveDrive.getPose` ile alınabilir.
* Robot jiroskop okumaları `SwerveDrive.getGyroRotation3d` veya `SwerveDrive.getYaw`, `SwerveDrive.getPitch`, `SwerveDrive.getRoll` ile alınabilir.
* Robot pozu, `SwerveDrive.addVisionMeasurement` ile vizyon girdileri kullanılarak güncellenebilir (isteğe bağlı standart sapma geçişi ile).
* Jiroskop ofseti `SwerveDrive.setGyroOffset` ile yapılandırılabilir ve pathplanner için kullanılmalıdır.
* Eğer translasyonel (öteleme) odometriniz kapalı (hatalı) ama kontrolleriniz doğruysa, translasyonel odometrinizi `SwerveDrive.invertOdometry` özelliği ile tersine çevirebilirsiniz.

## Telemetri

* Swerve telemetrisi [frc-web-components](https://github.com/frc-web-components/frc-web-components/tree/version4) [uygulaması](https://github.com/frc-web-components/app) ile çalışacak şekilde güncellenmiştir.
* Her modül açısı hem bağıl hem de mutlak enkoderler için raporlanır.
* Her modül hızı raporlanır.
* İstenen şasi hızı raporlanır.
* Robotun sahadaki mevcut konumunu ve yönünü temsil etmek için sürekli olarak oluşturulan ve güncellenen bir Field2d vardır.
* Test ederken `SwerveDrive.postTrajectory` ile sahaya yörüngeler ekleyebilirsiniz.
