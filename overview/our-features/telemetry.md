# Telemetri

## Nasıl çalışır?

YAGSL, konsolidasyon için `SwerveDrive` ve `SwerveModule`'de telemetri kullanır. [`SwerveDrive.updateOdometry()`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#updateOdometry\(\))'den gönderilen birkaç telemetri kalıntısı vardır. Tüm Telemetri, [`SwerveDriveTelemtry.verbosity`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/telemetry/SwerveDriveTelemetry.html#verbosity) içinde statik bir değişken olarak bir ayrıntı (verbosity) düzeyine bağlıdır. Aşağıdakiler kullanabileceğiniz seçeneklerdir.

```java
/**
 * Verbosity of telemetry data sent back.
 */
 public enum TelemetryVerbosity
{
  /**
   * No telemetry data is sent back.
   */
  NONE,
  /**
   * Low telemetry data, only post the robot position on the field.
   */
  LOW,
  /**
   * Medium telemetry data, swerve directory
   */
  INFO,
  /**
   * Info level + field info
   */
  POSE,
  /**
   * Full swerve drive data is sent back in both human and machine readable forms.
   */
  HIGH,
  /**
   * Only send the machine readable data related to swerve drive.
   */
  MACHINE
}
```

## Nasıl etkinleştiririm?

{% hint style="warning" %}
Daha yüksek telemetri, robotta biraz gecikmeye (lag) neden olabilir ve döngü sürelerini yavaşlatabilir. Bu yüzden ne seçtiğinize dikkat edin!
{% endhint %}

Telemetriyi yapılandırmak için lütfen [`SwerveDriveTelemetry.verbosity`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/telemetry/SwerveDriveTelemetry.html#verbosity)'yi istediğiniz [enum değerlerinden](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/telemetry/SwerveDriveTelemetry.TelemetryVerbosity.html) biriyle değiştirin.

<pre class="language-java"><code class="lang-java">  /**
   * Initialize {@link SwerveDrive} with the directory provided.
   *
   * @param directory Directory of swerve drive config files.
   */
  public SwerveSubsystem(File directory)
  {
    // Gereksiz nesnelerin oluşturulmasını önlemek için SwerveDrive'ı oluşturmadan önce Telemetriyi yapılandırın.
<strong>    SwerveDriveTelemetry.verbosity = TelemetryVerbosity.HIGH;
</strong>    swerveDrive = new SwerveParser(directory).createSwerveDrive(Constants.MAX_SPEED);
  }
</code></pre>

## Ne işe yarar?

Telemetri, ilgili Swerve Sürüş verilerini roboRIO'daki NetworkTables'a çıkarır. Bunları istediğiniz herhangi bir kontrol panelini (dashboard) kullanarak görüntüleyebilirsiniz!

Bazı gösterge panelleri (dashboard), `SmartDashboard/swerve` NetworkTable girdisine dayalı swerve sürüş widget'larını destekler.

Tüm Swerve Modül verileri, kurulum sırasında çok değerli olan `SmartDashboard/swerve/modules/` altındaki ilgili modüllerin altında saklanır.

### Swerve Modülü

<figure><img src="../../.gitbook/assets/image (3).png" alt="Shuffleboard Tree"><figcaption><p>Shuffleboard'da Swerve Modül Telemetrisi</p></figcaption></figure>

### Swerve Sürüşü

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Shuffleboard'da Swerve Sürüş Telemetrisi (ilgili anahtarlar daire içine alınmış)</p></figcaption></figure>

## Önerilen Shuffleboard Düzeni

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Solda Ham Mutlak Enkoder grubu, sağda Ham Açı Enkoderi grubu.</p></figcaption></figure>

Tüm modüllerin CCW+ (Saat yönünün tersine pozitif) okuduğundan emin olmak için kurulum sırasında bu düzeni kullanıyorum. Bu, swerve sürüşlerini yapılandırırken en çok gözden kaçan kısımdır.

Eğer **Raw Angle Encoder** (Ham Açı Enkoderi) CCW- ise (saat yönünün tersine çevrilirken azalıyorsa), o modül için konfigürasyon dosyasında açı motorunun ters çevrilmesi (inverted) gerekir.

Eğer **Raw Absolute Encoder** (Ham Mutlak Enkoder) CCW- ise (tekerlek saat yönünün tersine çevrilirken azalıyorsa), o modül için mutlak enkoderin ters çevrilmesi gerekebilir.

## Alternatif Dashboard Desteği

YAGSL widget'larını da destekleyen birkaç dashboard var! Bu geliştiriciler harika ve işlerine kesinlikle göz atmalısınız!

* [Elastic Dashboard](https://github.com/Gold872/elastic-dashboard)
* [FRC Web Components](https://github.com/frc-web-components/app/releases/latest)
* [Advantage Scope](https://github.com/Mechanical-Advantage/AdvantageScope)
