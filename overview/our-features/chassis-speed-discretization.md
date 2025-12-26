---
description: Daha fazla matematik...
---

# Şasi Hızı Ayrıklaştırma (Chassis Speed Discretization)

## Şasi Hızı Ayrıklaştırma (Discretization) Nedir?

Şasi Hızı ayrıklaştırma (discretization), Swerve Sürüşünün öteleme hareketindeki sapmayı (skew) azaltmak için kullanılır. Yalnızca [`SwerveDrive.chassisVelocityCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#chassisVelocityCorrection) `true` ise çağrılır.

## Şasi Hızı Ayrıklaştırmayı Nasıl Kullanırım?

Şasi Hızı ayrıklaştırma, WPILib'deki [`ChassisSpeeds.discretize`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/ChassisSpeeds.html#discretize\(edu.wpi.first.math.kinematics.ChassisSpeeds,double\)) için kendi değerlerinizi ayarlamanıza olanak tanır, varsayılan `0.02`dt değeri çoğu takım için yeterince iyi olmalıdır. Ayrıklaştırmayı etkinleştirmek ve özelleştirmek için tek yapmanız gereken aşağıda gösterildiği gibi [`SwerveDrive.setChassisDiscretization`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setChassisDiscretization\(boolean,double\))'ı çağırmaktır.

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
<strong>    swerveDrive.setChassisDiscretization(true, 0.02);
</strong>  }
</code></pre>
