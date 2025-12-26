# Jiroskop

YAGSL, her bütçeden takıma en iyi şekilde yardımcı olmak amacıyla çok çeşitli Jiroskopları destekler; NavX veya Pigeon2'yi önersek ve resmi olarak destekleyip test etmiş olsak da, diğerlerini de değişen başarı dereceleriyle desteklemeye çalışıyoruz.

## Jiroskop Kontrol Listesi

* [ ] [Jiroskop okumaları saat yönünün tersine döndürüldüğünde artar](#user-content-fn-1)[^1].
* [ ] Yaw okuması robotun başlığıdır (heading).
* [ ] Jiroskop `0`, istenen robot "önü"dür.

## Swerve IMU sarıcısı (Wrapper)

YAGSL, bir Swerve Sürüşünün çalışması için gereken verileri standart bir şekilde almak ve ayarlamak için desteklenen tüm Jiroskop tipleri üzerinde sarıcılar oluşturur, bu sarıcıya [`SwerveIMU`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/imu/SwerveIMU.html) denir. Tüm Jiroskoplar, verilen `swervedrive.json` dosyasından oluşturulan [`SwerveDriveConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveDriveConfiguration.html) nesnesi aracılığıyla [`SwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#swerveDriveConfiguration) nesnesinden alınabilir. Bir kullanıcı programının ham jiroskop nesnesini alması için tek yapmanız gereken aşağıdaki gibi nesneyi doğru tipe dönüştürmektir (cast), bizim durumumuzda bu bir NavX `AHRS` sınıfı olacaktır.

<pre class="language-java"><code class="lang-java">   /**
   * Initialize {@link SwerveDrive} with the directory provided.
   *
   * @param directory Directory of swerve drive config files.
   */
  public SwerveSubsystem(File directory)
  {
    // Angle conversion factor is 360 / (GEAR RATIO * ENCODER RESOLUTION)
    //  In this case the gear ratio is 12.8 motor revolutions per wheel rotation.
    //  The encoder resolution per motor revolution is 1 per motor revolution.
    double angleConversionFactor = SwerveMath.calculateDegreesPerSteeringRotation(12.8, 1);
    // Motor conversion factor is (PI * WHEEL DIAMETER IN METERS) / (GEAR RATIO * ENCODER RESOLUTION).
    //  In this case the wheel diameter is 4 inches, which must be converted to meters to get meters/second.
    //  The gear ratio is 6.75 motor revolutions per wheel rotation.
    //  The encoder resolution per motor revolution is 1 per motor revolution.
    double driveConversionFactor = SwerveMath.calculateMetersPerRotation(Units.inchesToMeters(4), 6.75, 1);

    // Configure the Telemetry before creating the SwerveDrive to avoid unnecessary objects being created.
    SwerveDriveTelemetry.verbosity = TelemetryVerbosity.HIGH;
    try
    {
      swerveDrive = new SwerveParser(directory).createSwerveDrive(maximumSpeed, angleConversionFactor, driveConversionFactor);
    } catch (Exception e)
    {
      throw new RuntimeException(e);
    }
    swerveDrive.setHeadingCorrection(false); // Heading correction should only be used while controlling the robot via angle.

    <a data-footnote-ref href="#user-content-fn-2">AHRS</a> navx = (<a data-footnote-ref href="#user-content-fn-3">AHRS</a>)swerveDrive.getGyro().getIMU();

  }
</code></pre>

## Önerilen Jiroskoplar

Bu jiroskoplar kapsamlı bir şekilde test edilmiştir ve birçok FRC takımı tarafından kullanılmaktadır. Genel olarak konuşursak, bunlar size en iyi performansı ve güvenilirliği sağlamanın yanı sıra topluluktan yardım almanızı da sağlayacaktır.

### Studica tarafından [NavX2 MXP](gyroscope/navx.md)

{% embed url="https://www.studica.ca/en/navx-2-mxp-robotics-navigation-sensor" %}

## CTRE tarafından [Pigeon2 IMU](gyroscope/pigeon-2.0.md)

{% embed url="https://store.ctr-electronics.com/pigeon-2/" %}

## Jiroskop Konfigürasyonu

{% hint style="warning" %}
Şu anda yalnızca CTRE cihazları `canbus` seçeneğini desteklemektedir, cihazınız roboRIO `canbus` kullanıyorsa desteklenen CTRE cihazları için `null` veya `"rio"` değerini kullanmalısınız. Bir CANivore kullanıyorsanız ve cihaz CANivore veriyolundaysa, ad CANivore adıyla eşleşmelidir.
{% endhint %}

`swervedrive.json` içinde jiroskopu şöyle belirlersiniz

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": "<a data-footnote-ref href="#user-content-fn-4">pigeon2</a>",
    <a data-footnote-ref href="#user-content-fn-5">"id"</a>: <a data-footnote-ref href="#user-content-fn-6">13</a>,
    <a data-footnote-ref href="#user-content-fn-7">"canbus"</a>: "<a data-footnote-ref href="#user-content-fn-8">canivore</a>"
  },
  "invertedIMU": true,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

{% hint style="warning" %}
Eğer robotunuz herhangi bir kontrolcü girişi olmadan kontrolden çıkıyorsa muhtemelen IMU'nuzu burada ters çevirmeniz gerekiyordur.
{% endhint %}

### Olası Jiroskop Tipleri

| Cihaz                                                                   | type                | İletişim                                          |
| ----------------------------------------------------------------------- | ------------------- | ------------------------------------------------- |
| [Pigeon](gyroscope/pigeon.md)                                           | `pigeon`            | CAN; CANivore desteklemez.                       |
| [Pigeon2](gyroscope/pigeon-2.0.md)                                      | `pigeon2`           | CAN; CANivore destekler                             |
| [Canandgyro](https://docs.reduxrobotics.com/canandgyro/getting-started) | `canandgyro`        | CAN; CANivore desteklemez.                       |
| [NavX](gyroscope/navx.md)                                               | `navx` , `navx_spi` | roboRIO MXP SPI                                   |
| [NavX](gyroscope/navx.md)                                               | `navx_i2c`          | roboRIO MXP üzerindeki I2C portu. Önerilmez!      |
| [NavX](gyroscope/navx.md)                                               | `navx_usb`          | roboRIO'ya USB Kablosu üzerinden Seri (önerilmez) |
| [NavX](gyroscope/navx.md)                                               | `navx_mxp_serial`   | roboRIO MXP üzerinden Seri                        |
| [ADIS16448](gyroscope/adis16448.md)                                     | `adis16448`         | roboRIO MXP                                       |
| [ADIS16470](gyroscope/adis16470.md)                                     | `adis16470`         | roboRIO SPI portu                                  |
| [ADXRS450](gyroscope/adxrs450.md)                                       | `adxrs450`          | roboRIO SPI portu.                                 |
| Analog Gyro                                                             | `analog`            | AnalogInput                                       |

[^1]: Saat Yönünün Tersi Pozitif veya CCW+ olarak da bilinir

[^2]: Java'da NavX'i temsil etmek ve onunla iletişim kurmak için kullanılan NavX `AHRS` sınıfı.

[^3]: Java `Object`'ini `AHRS` sınıfına dönüştürür (casts), bu Jiroskopunuz için yerel sınıf ne ise onunla değiştirilmelidir.

[^4]: Örneklendirmek ve kullanmak için `pigeon2` IMU cihazını seçer.

[^5]: Bu durumda CAN ID'ye atıfta bulunur ancak seçilen tipe bağlı olarak roboRIO'nun AnalogInput'una da atıfta bulunabilir.

[^6]: Pigeon 2'nin CAN ID'si 13'tür

[^7]: CAN veriyolu her zaman kullanılmaz ve normalde `"rio"` olan varsayılan (roboRIO) CAN veriyolunu seçmek için `null` veya `""` olabilir

[^8]: cihaz o CAN veriyolundaysa ad canivore adıyla eşleşmelidir, aksi takdirde roboRIO CAN veriyolunu belirtmek için `"rio"` veya `null` veya `""` olmalıdır.
