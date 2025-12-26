---
description: Bu bazen yararlıdır
---

# Kosinüs Telafisi

## Kosinüs Telafisi nasıl çalışır?

Kosinüs telafisi, tekerleğinizin hızını swerve modülünün açı deltasının kosinüsüyle ölçeklendirir.

## Nasıl etkinleştiririm?

{% hint style="warning" %}
Kosinüs telafisi **simülasyonda çalışmaz** ve YALNIZCA robot üzerinde kullanım içindir! Yarışmada kullanmaya karar vermeden önce lütfen iyice test edin.
{% endhint %}

Kosinüs telafisini etkinleştirmek kolaydır! Tek gereken `SwerveDrive.setCosineCompensator` fonksiyonudur!

<pre class="language-java"><code class="lang-java"> /**
   * Initialize {@link SwerveDrive} with the directory provided.
   *
   * @param directory Directory of swerve drive config files.
   */
  public SwerveSubsystem(File directory)
  {
    // Gereksiz nesnelerin oluşturulmasını önlemek için SwerveDrive'ı oluşturmadan önce Telemetriyi yapılandırın.
    SwerveDriveTelemetry.verbosity = TelemetryVerbosity.HIGH;
    swerveDrive = new SwerveParser(directory).createSwerveDrive(Constants.MAX_SPEED);
<strong>    swerveDrive.setCosineCompensator(false); // Gerçek hayatta görülmeyen tutarsızlıklara neden olduğu için simülasyonlar için kosinüs telafisini devre dışı bırakır.
</strong>  }
</code></pre>
