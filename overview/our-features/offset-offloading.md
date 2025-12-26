---
description: Bu yalnızca bazı motor kontrolcülerinde desteklenir!
---

# Ofset Yükleme (Offset Offloading)

## Offset Offloading Nedir?

Offset Offloading, mutlak enkoder ofsetinin roboRIO yerine mutlak enkoderde (veya mutlak enkoder motor sürücüye bağlıysa motor sürücüde) saklanmasıdır. Bu normalde roboRIO'da daha hızlı bir döngü süresi sağlar, ancak CAN veriyolu veya düşük voltaj (brown-out) gibi bir maç sırasında herhangi bir şey bozulursa Swerve Sürüşüne biraz kararsızlık ekleyebilir.

## Offset Offloading'i Nasıl Etkinleştiririm?

Offset offloading, [`SwerveDrive.pushOffsetsToEncoders`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#pushOffsetsToEncoders\(\)) ile etkinleştirilir ve [`SwerveDrive.restoreInternalOffset`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#restoreInternalOffset\(\)) ile devre dışı bırakılır; bunların her ikisi de her örneklenen modül için `SwerveModule`'deki aynı adlı bir fonksiyonu çağırır.

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
<strong>    swerveDrive.pushOffsetsToEncoders();
</strong>  }
</code></pre>
