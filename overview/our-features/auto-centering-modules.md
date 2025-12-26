---
description: >-
  Otomatik merkezlenen modüller istenmeyen titremelere neden olabilir, bu yüzden varsayılan olarak devre dışıdır!
---

# Otomatik Merkezlenen Modüller

## Otomatik merkezlenen modüller nedir?

Otomatik merkezleme, herhangi bir girdi sağlanmadığında robotunuzun tekerlekleri merkeze almasıdır. Otomatik merkezleme etkinleştirildiğinde, Swerve Modülü kontrolcüden veya otonomdan girdi gelmediği her seferde `0`'a "sabitlenir" (snap). Bu bazı takımlar tarafından istenebilir ancak hiçbir şekilde önerilmez. Otomatik merkezleme, başlangıçta bazen robotunuzu otonom için yanlış hizalayan sorunlara neden olur, bu da normalden daha fazla kaymaya (drift) neden olabilir. Otomatik merkezlenen modüller [`SwerveModule.setAntiJitter(false)`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveModule.html#setAntiJitter\(boolean\)) çağrısı yaparak çalışır, bu nedenle bu eylemin tüm yan etkileri bunu kullanan swerve sürüşlerinde mevcuttur!

## Otomatik merkezlenen modülleri nasıl etkinleştiririm?

Otomatik merkezlemeyi `SwerveDrive.setAutoCenteringModules(true)` kullanarak etkinleştirirsiniz.

<pre class="language-java"><code class="lang-java">  /**
   * Initialize {@link SwerveDrive} with the directory provided.
   *
   * @param directory Directory of swerve drive config files.
   */
  public SwerveSubsystem(File directory)
  {
    // Gereksiz nesnelerin oluşturulmasını önlemek için SwerveDrive'ı oluşturmadan önce Telemetriyi yapılandırın.
    SwerveDriveTelemetry.verbosity = TelemetryVerbosity.HIGH;
    swerveDrive = new SwerveParser(directory).createSwerveDrive(Constants.MAX_SPEED);
<strong>    swerveDrive.setAutoCenteringModules(true);
</strong>  }
</code></pre>

