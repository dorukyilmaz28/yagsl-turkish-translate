---
description: Bu biraz karışık
---

# Maksimum Hız

## Maksimum Hız Nedir?

YAGSL maksimum hızı saklar ve aşağıdaki fonksiyonlarda kullanır:

* [ ] [`SwerveDriveKinematics.desaturateWheelSpeeds`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveDriveKinematics.html#desaturateWheelSpeeds\(edu.wpi.first.math.kinematics.SwerveModuleState\[],double\))
* [ ] [`SwerveMath.calculateMaxAngularVelocity`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/math/SwerveMath.html#calculateMaxAngularVelocity\(double,double,double\))
* [ ] [`SwerveDriveTelemetry.maxSpeed`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/telemetry/SwerveDriveTelemetry.html#maxSpeed)
* [ ] [`SwerveMath.antiJitter`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/math/SwerveMath.html#antiJitter\(edu.wpi.first.math.kinematics.SwerveModuleState,edu.wpi.first.math.kinematics.SwerveModuleState,double\))
* [ ] [`SwerveMath.createDriveFeedforward`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/math/SwerveMath.html#createDriveFeedforward\(double,double,double\))

Maksimum hız, robotun fiziksel maksimum hızını temsil eder.

## Maksimum Hızımı Nasıl Değiştiririm?

Maksimum hızınızı `SwerveDrive.setMaximumSpeed` kullanarak değiştirebilirsiniz. İlk maksimum hız, maksimum açısal hız, sürüş ileri beslemesi (drive feedforward) ve telemetri maksimum hızı gibi başlangıç değerleri için [`SwerveParser.createSwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveParser.html#createSwerveDrive\(double\)) içinde verilir.

{% hint style="info" %}
Telemetrideki maksimum hız değişmez çünkü çoğu araç (widgets) bunu desteklemez ve onları bozabilir!
{% endhint %}

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
<strong>    swerveDrive.setMaximumSpeed(Units.feetToMeters(12.4)); // 12.4ft/s to m/s
</strong>  }
</code></pre>
