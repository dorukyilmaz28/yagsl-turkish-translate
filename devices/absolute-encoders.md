# Mutlak Enkoderler

YAGSL, en yaygın FRC mutlak enkoderlerini destekler. Fırçalı motor kullanıyorsanız mutlak enkoderler gereklidir.

Mutlak enkoder değeri sürücü panelinizde `swerve/modules/.../Raw Absolute Encoder` altında görünecektir ve çoğu durumda modül JSON konfigürasyon dosyalarında `absoluteEncoderOffset` ayarını yapmak için kullanılabilir.

## Mutlak Enkoder Kontrol Listesi

* [ ] Tüm Mutlak Enkoderler saat yönünün tersine pozitif döner.
* [ ] Manyetik Mutlak enkoderler, mıknatıs üzerindeyken ve çalışırken (robot hareket ederken) iyi bir okumaya sahiptir.
* [ ] Mutlak Enkoderler benzersiz CAN ID'lerine veya Analog Giriş Kanallarına sahiptir.
* [ ] Mutlak Enkoderler doğru ID veya Analog Giriş Kanalı ile tanımlanmıştır.
* [ ] Mutlak Enkoderler tam aralığa sahiptir (`0`-`360`)

## Swerve Mutlak Enkoder Sarıcısı (Wrapper)

YAGSL, bir Swerve Modülünün çalışması için gereken verileri standart bir şekilde almak ve ayarlamak için desteklenen tüm Mutlak Enkoderler üzerinde sarıcılar (wrappers) oluşturmuştur. Bu sarıcıya [`SwerveAbsoluteEncoder`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/encoders/SwerveAbsoluteEncoder.html) denir. Tüm [`SwerveAbsoluteEncoder`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/encoders/SwerveAbsoluteEncoder.html)'lar [`SwerveModule`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html#configuration) konfigürasyon nesnesi [`SwerveModuleConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html) mutlak enkoder özelliği [`absoluteEncoder`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html#absoluteEncoder) aracılığıyla alınabilir. [`SwerveModule`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html) [`SwerveDrive.getModules()`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#getModules\(\)) ile kolayca alınabilir.

YAGSL, bir Swerve Sürüşünün çalışması için gereken verileri standart bir şekilde almak ve ayarlamak için desteklenen tüm Motor Kontrolcüleri üzerinde sarıcılar oluşturmuştur. Bu sarıcıya [`SwerveMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/motors/SwerveMotor.html) denir. Tüm [`SwerveMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/motors/SwerveMotor.html)'lar [`SwerveModule`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html#configuration) konfigürasyon nesnesi [`SwerveModuleConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html) motor tanımları [`angleMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html#angleMotor) ve [`driveMotor`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html#driveMotor) aracılığıyla alınabilir. [`SwerveModule`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html) [`SwerveDrive.getModules()`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#getModules\(\)) ile kolayca alınabilir.

<pre class="language-java"><code class="lang-java">import com.ctre.phoenix6.hardware.CANcoder;
 
   /**
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
      <a data-footnote-ref href="#user-content-fn-1">CANcoder</a> absoluteEncoder = (<a data-footnote-ref href="#user-content-fn-2">CANcoder</a>)m.configuration.absoluteEncoder.getAbsoluteEncoder();
    }
  }
</code></pre>

## Mutlak Enkoder Konfigürasyonu

{% hint style="warning" %}
Şu anda yalnızca CTRE cihazları `canbus` seçeneğini desteklemektedir, cihazınız roboRIO `canbus` kullanıyorsa desteklenen CTRE cihazları için `null` veya `"rio"` değerini kullanmalısınız. Bir CANivore kullanıyorsanız ve cihaz CANivore veriyolundaysa, ad CANivore adıyla eşleşmelidir.
{% endhint %}

{% hint style="success" %}
Mutlak enkoderiniz SparkMAX'ınıza bağlıysa, en iyi performans için [`SwerveDrive.pushOffsetsToEncoders()`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#pushOffsetsToEncoders\(\)) fonksiyonunu kullanın. Bu, yerleşik PID sensörünü bağlı enkoder olarak ayarlar!
{% endhint %}

`frontleft.json`,`frontright.json`,`backleft.json`,`backright.json` gibi herhangi bir modül JSON dosyasında, bir mutlak enkoderi yapılandırmak için göreceğiniz şey budur.

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
    "type": <a data-footnote-ref href="#user-content-fn-9">"cancoder"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-10">11</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-11">null</a>
  },
  "inverted": {
    "drive": <a data-footnote-ref href="#user-content-fn-12">false</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-13">false</a>
  },
  "absoluteEncoderOffset": <a data-footnote-ref href="#user-content-fn-14">-18.281</a>,
  "absoluteEncoderInverted": <a data-footnote-ref href="#user-content-fn-15">false</a>,
  "location": {
    "front": <a data-footnote-ref href="#user-content-fn-16">-12</a>,
    "left": <a data-footnote-ref href="#user-content-fn-17">-12</a>
  }
}
</code></pre>

## Olası Mutlak Enkoder Tipleri

{% hint style="warning" %}
Modülünüz dönmeye devam ediyorsa dümenleme/açı/azimut motorunuzu ters çevirmeyi deneyin.
{% endhint %}

<table data-full-width="true"><thead><tr><th width="538">Cihaz</th><th width="269">type</th></tr></thead><tbody><tr><td>None</td><td><code>none</code></td></tr><tr><td><a href="https://docs.revrobotics.com/brushless/spark-max/encoders/absolute#data-port-connector-information">Integrated/Attached</a> (SparkMAX DutyCycle aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-18"><code>attached</code></a></td></tr><tr><td><a href="https://docs.revrobotics.com/brushless/spark-max/encoders/absolute#data-port-connector-information">SparkMax Analog</a> (SparkMAX Analog Pin aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-19"><code>sparkmax_analog</code></a></td></tr><tr><td><a href="https://docs.revrobotics.com/brushless/spark-max/encoders/absolute#data-port-connector-information">SparkMax Analog</a> (5V güç ile SparkMAX Analog Pin aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-20"><code>sparkmax_analog5v</code></a></td></tr><tr><td><a href="https://docs.reduxrobotics.com/canandmag/spark-max#using-the-pwm-output-with-spark-max">Canandmag</a> (SparkMAX aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-21"><code>canandmag</code></a></td></tr><tr><td><a href="https://docs.reduxrobotics.com/canandmag/getting-started">Canandmag </a>(CAN aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-22"><code>canandmag_can</code></a></td></tr><tr><td><a href="https://pro.docs.ctr-electronics.com/en/latest/docs/hardware-reference/cancoder/index.html">CANcoder</a></td><td><a data-footnote-ref href="#user-content-fn-23"><code>cancoder</code></a></td></tr><tr><td><a href="https://www.revrobotics.com/rev-11-1271/">Throughbore</a> (DIO aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-24"><code>throughbore</code></a></td></tr><tr><td><a href="https://www.thethriftybot.com/products/thrifty-absolute-magnetic-encoder">Thrifty Absolute Magnetic Encoder</a> (Analog Input aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-25"><code>thrifty</code></a></td></tr><tr><td><a href="https://www.andymark.com/products/ma3-absolute-encoder-with-cable">MA3</a> (Analog Input aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-26"><code>ma3</code></a></td></tr><tr><td><a href="https://store.ctr-electronics.com/srx-mag-encoder/">SRX Mag</a> (PWM aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-27"><code>ctre_mag</code></a></td></tr><tr><td><a href="https://www.andymark.com/products/am-mag-encoder">AM Mag</a> (PWM aracılığıyla)</td><td><a data-footnote-ref href="#user-content-fn-28"><code>am_mag</code></a></td></tr><tr><td>PWM DutyCycle</td><td><code>dutycycle</code></td></tr><tr><td>Analog Encoder</td><td><code>analog</code></td></tr></tbody></table>

[^1]: Phoenix 6'dan [`CANcoder`](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/CANcoder.html), konfigürasyonlardan CAN veriyolu ve CAN ID kullanılarak başlatılır.

[^2]: Phoenix 6'dan [`CANcoder`](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/CANcoder.html), konfigürasyonlardan CAN veriyolu ve CAN ID kullanılarak başlatılır. `Object`'i [`CANcoder`](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/CANcoder.html)'a dönüştürün (cast).

[^3]: SparkMAX fırçasız (brushless) modu seçili.

[^4]: SparkMAX'ın CAN ID'si `5`'tir.

[^5]: SparkMAX, CANivore ile uyumlu değildir, bu nedenle `canbus` `null` veya `""` olmalıdır.

[^6]: SparkMAX fırçasız (brushless) modu seçili.

[^7]: SparkMAX'ın CAN ID'si `6`'dır.

[^8]: SparkMAX, CANivore ile uyumlu değildir, bu nedenle `canbus` `null` veya `""` olmalıdır.

[^9]: [`CANcoder`](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/CANcoder.html), aşağıdaki CAN ID ve veriyolu kullanılarak seçilir.

[^10]: Bu modül için [`CANcoder`](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/CANcoder.html) ID'si.

[^11]: [`CANcoder`](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/CANcoder.html)'ın üzerinde bulunduğu CANivore adı.

[^12]: Sürüş motoru, herhangi bir ters çevirme olmadan saat yönünün tersine pozitif döner.

[^13]: Dümenleme/açı/azimut motoru, ters çevrilmeden saat yönünün tersine pozitif döner.

[^14]: Tekerlek düz bakarken ve konik dişliler aynı yöndeyken `Module[...] Raw Absolute Encoder`dan okunan ofset.\
    \
    Ofsetler derece cinsindendir.

[^15]: Bu nadiren, hatta hiç doğru olmamalıdır.

[^16]: Bu modülün merkezi, robotun merkezinden "ön tarafa" doğru `-12` inçtir.

[^17]: Bu modülün merkezi, robotun merkezinden "sola" doğru `-12` inçtir.

[^18]: ```json
    "encoder": {
        "type": "attached",
        "id": 11,
        "canbus": null
      },
    ```

[^19]: ```json
    "encoder": {
        "type": "sparkmax_analog",
        "id": 11,
        "canbus": null
      },
    ```

[^20]: ```json
    "encoder": {
        "type": "sparkmax_analog5v",
        "id": 11,
        "canbus": null
      },
    ```

[^21]: ```json
    "encoder": {
        "type": "canandmag",
        "id": 11,
        "canbus": null
      },
    ```

[^22]: ```json
    "encoder": {
        "type": "canandmag_can",
        "id": 11,
        "canbus": null
      },
    ```

[^23]: ```json
    "encoder": {
        "type": "cancoder",
        "id": 11,
        "canbus": null
      },
    ```

[^24]: ```json
    "encoder": {
        "type": "throughbore",
        "id": 11,
        "canbus": null
      },
    ```

[^25]: ```json
    "encoder": {
        "type": "thrifty",
        "id": 11,
        "canbus": null
      },
    ```

[^26]: ```json
    "encoder": {
        "type": "ma3",
        "id": 11,
        "canbus": null
      },
    ```

[^27]: ```json
    "encoder": {
        "type": "ctre_mag",
        "id": 11,
        "canbus": null
      },
    ```

[^28]: ```json
    "encoder": {
        "type": "am_mag",
        "id": 11,
        "canbus": null
      },
    ```
