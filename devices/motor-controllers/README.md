# Motor Kontrolcüleri

YAGSL, çoğu yaygın FRC motor kontrolcüsünü destekler ([Venom](https://www.playingwithfusion.com/productview.php?pdid=99\&catid=1014)'lar hariç) ve mümkünse entegre enkoderli fırçasız bir motor kullanmanızı önersek de, harici kare (quadrature) enkoderli fırçalı motorları da **YALNIZCA** SparkMAX'larla destekliyoruz.

Entegre enkoder değeri, sürücü panelinizde `swerve/modules/.../Raw Motor Encoder` altında, doğrudan motordan enkoder değerini çıktı olarak gösterir.

## Motor Kontrol Listesi

* [ ] Tüm motorlar saat yönünün tersine pozitif döner, değilse bunu sağlamak için gerekli ters çevirmeleri belgeleyin.
* [ ] PID yeteneklerinizin en iyisine göre ayarlanmıştır.
* [ ] Motor en son ürün yazılımına güncellenmiştir.
* [ ] Motorun benzersiz CAN ID'si vardır.
* [ ] Motor tipi ayarlanmıştır.
* [ ] Verilen CAN ID, JSON modülündekiyle uyuşur.
* [ ] Tekerlekler ileriye doğru hizalanmış ve tüm konik dişliler aynı yöne bakıyor.

## Swerve Motor Sarıcısı (Wrapper)

YAGSL, bir Swerve Sürüşünün çalışması için gereken verileri standart bir şekilde almak ve ayarlamak için desteklenen tüm Motor Kontrolcüleri üzerinde sarıcılar oluşturmuştur. Bu sarıcıya [`SwerveMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/motors/SwerveMotor.html) denir. Tüm [`SwerveMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/motors/SwerveMotor.html)'lar [`SwerveModule`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html#configuration) konfigürasyon nesnesi [`SwerveModuleConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html) motor tanımları [`angleMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html#angleMotor) ve [`driveMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html#driveMotor) aracılığıyla alınabilir. [`SwerveModule`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html) [`SwerveDrive.getModules()`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#getModules\(\)) ile kolayca alınabilir.

<pre class="language-java" data-full-width="true"><code class="lang-java"> /**
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

    for(SwerveModule m : swerveDrive.getModules())
    {
      System.out.println("Module Name: "+m.configuration.name);
      CANSparkMax steeringMotor = (<a data-footnote-ref href="#user-content-fn-1">CANSparkMax</a>)m.getAngleMotor().getMotor(); 
      CANSparkMax driveMotor = (<a data-footnote-ref href="#user-content-fn-2">CANSparkMax</a>)m.getDriveMotor().getMotor(); 
    }
  }
</code></pre>

## Motor Kontrolcüsü Konfigürasyonu

{% hint style="warning" %}
Şu anda yalnızca CTRE cihazları `canbus` seçeneğini desteklemektedir, cihazınız roboRIO `canbus` kullanıyorsa desteklenen CTRE cihazları için `null` veya `"rio"` değerini kullanmalısınız. Bir CANivore kullanıyorsanız ve cihaz CANivore veriyolundaysa, ad CANivore adıyla eşleşmelidir.
{% endhint %}

`frontleft.json`,`frontright.json`,`backleft.json`,`backright.json` gibi herhangi bir modül JSON dosyası içinde bir motor kontrolcüsünü yapılandırmak için göreceğiniz şey budur.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": <a data-footnote-ref href="#user-content-fn-3">"sparkmax"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-4">5</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-5">null</a>
  },
  "angle": {
    "type": <a data-footnote-ref href="#user-content-fn-6">"sparkmax"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-7">6</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-8">null</a>
  },
  "encoder": {
    "type": "cancoder",
    "id": 11,
    "canbus": null
  },
  "inverted": {
    "drive": <a data-footnote-ref href="#user-content-fn-9">false</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-10">false</a>
  },
  "absoluteEncoderOffset": -18.281,
  "location": {
    "front": <a data-footnote-ref href="#user-content-fn-11">-12</a>,
    "left": <a data-footnote-ref href="#user-content-fn-12">-12</a>
  }
}
</code></pre>

## Olası Motor Kontrolcüsü Tipleri

| Cihaz                     | type                                                                                  |
| ------------------------- | ------------------------------------------------------------------------------------- |
| [SparkMAX](sparkmax.md)   | `sparkmax` (aynı `neo`);`neo` ; `neo550`                                              |
| [SparkFlex](sparkflex.md) | `sparkflex` (aynı `vortex`); `vortex`; `sparkflex_neo`; `sparkflex_vortex`            |
| [TalonFX](talonfx.md)     | `talonfx`(aynı `krakenx60`);`falcon500`;`falcon500foc`;`krakenx60`; `krakenx60foc`    |
| TalonSRX                  | `talonsrx`                                                                            |
| SparkMAX Brushed          | `sparkmax_brushed`                                                                    |

{% hint style="warning" %}
Şu anda `sparkmax_brushed` ve `talonsrx` gibi fırçalı motor kullanımı hakkında dokümantasyon sağlamıyorum.
{% endhint %}

[^1]: `SwerveMotor`'un sardığı motor kontrolcüsü nesnesini orijinal sınıfa, bu durumda `CANSparkMax`'a geri dönüştürün (cast).

[^2]: `SwerveMotor`'un sardığı motor kontrolcüsü nesnesini orijinal sınıfa, bu durumda `CANSparkMax`'a geri dönüştürün (cast).

[^3]: SparkMAX fırçasız (brushless) modu seçili.

[^4]: SparkMAX'ın CAN ID'si `5`'tir.

[^5]: SparkMAX, CANivore ile uyumlu değildir, bu nedenle `canbus` `null` veya `""` olmalıdır.

[^6]: SparkMAX fırçasız (brushless) modu seçili.

[^7]: SparkMAX'ın CAN ID'si `6`'dır.

[^8]: SparkMAX, CANivore ile uyumlu değildir, bu nedenle `canbus` `null` veya `""` olmalıdır.

[^9]: Sürüş motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^10]: Dümenleme/azimut/açı motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^11]: Bu modülün merkezi, robotun merkezinden "ön tarafa" doğru `-12` inçtir.

[^12]: Bu modülün merkezi, robotun merkezinden "sola" doğru `-12` inçtir.
