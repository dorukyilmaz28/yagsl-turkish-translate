---
description: >-
  YAGSL-Example, varsayılan olarak tam simülasyon desteğine sahiptir ve ek
  kurulum gerektirmez.
---

# Simülasyon

## Nasıl çalışır?

YAGSL, üreticilerin sunduğu simülasyon modüllerini kullanarak robotun tamamını simüle eder. Gerekli veriler, tamamen simüle edilmiş `SwerveModuleSimulation`  ve  `SwerveIMUSimulation`  sınıfları tarafından sağlanır.&#x20;

## Nasıl etkinleştiririm?

{% hint style="warning" %}
Simülasyon çalıştırılırken kosinüs telafisi ve başlık düzeltmesi devre dışı bırakılmalıdır, aksi takdirde simülasyon kontrol edilemez olabilir!
{% endhint %}

Simülasyonun düzgün çalışması için tek yapmanız gereken, aşağıdaki örnekte olduğu gibi başlık telafisinin (heading compensation) ve kosinüs telafisinin (cosine compensation) devre dışı bırakıldığından emin olmaktır.

<pre class="language-java"><code class="lang-java"> /**
   * Initialize {@link SwerveDrive} with the directory provided.
   *
   * @param directory Directory of swerve drive config files.
   */
  public SwerveSubsystem(File directory)
  {
    // Configure the Telemetry before creating the SwerveDrive to avoid unnecessary objects being created.
    SwerveDriveTelemetry.verbosity = TelemetryVerbosity.HIGH;
    swerveDrive = new SwerveParser(directory).createSwerveDrive(Constants.MAX_SPEED);
<strong>    swerveDrive.setHeadingCorrection(false); // Başlık düzeltmesi yalnızca robot açı ile kontrol edilirken kullanılmalıdır.
</strong><strong>    swerveDrive.setCosineCompensator(false); // Gerçek hayatta görülmeyen tutarsızlıklara neden olduğu için simülasyonlar için kosinüs telafisini devre dışı bırakır.
</strong>  }
</code></pre>

Daha sonra simülasyonu WPILiB'de normalde yaptığınız gibi çalıştırın.

Daha fazla bilgi için simülasyon hakkındaki WPILib dokümantasyonuna göz atın!

{% embed url="https://docs.wpilib.org/en/stable/docs/software/wpilib-tools/robot-simulation/introduction.html" %}
