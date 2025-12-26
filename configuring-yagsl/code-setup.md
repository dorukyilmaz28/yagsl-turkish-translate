# Kod Kurulumu

## YAGSL İçe Aktarma (Import)

### Çevrimiçi

Kurmak için WPILib satıcı deps (bağımlılıklarını) kullanın.

{% embed url="https://docs.wpilib.org/en/stable/docs/software/vscode-overview/3rd-party-libraries.html#rd-party-libraries" %}

YAGSL vendordep URL'si:

```
https://broncbotz3481.github.io/YAGSL-Lib/yagsl/yagsl.json
```

### Çevrimdışı

Projeye `src/main/java` içine [YAGSL-Example'dan `swervelib` dizinini](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java) kopyalayın.

{% hint style="warning" %}
Çevrimdışı ve çevrimiçi sürümlerin aynı anda yüklü olması mümkün değildir! Hatalar oluşacaktır!
{% endhint %}

{% hint style="info" %}
[Tüm bağımlılıkları da kurduğunuzdan](dependency-installation.md) emin olun!
{% endhint %}

## Bir swerve sürüşü nasıl oluşturulur?

YAGSL, tamamen JSON konfigürasyon dosyalarına dayalı bir swerve sürüşü oluşturabilmeniz bakımından benzersizdir. JSON konfigürasyon dosyaları [`deploy`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/deploy/swerve/neo) dizininde bulunmalıdır. Ayrıca Konfigürasyon nesnelerini manuel olarak oluşturabilir ve Swerve Sürüşünüzü bu şekilde somutlaştırabilirsiniz.

### JSON kullanarak bir SwerveDrive nasıl oluşturulur.

Bu örnek program, [`SwerveSubsystem`](https://github.com/BroncBotz3481/YAGSL-Example/blob/main/src/main/java/frc/robot/subsystems/swervedrive/SwerveSubsystem.java) içinde [`SwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html)'ı oluşturur, çünkü komut tabanlı programlama kullanıyorsanız [`SwerveSubsystem`](https://github.com/BroncBotz3481/YAGSL-Example/blob/main/src/main/java/frc/robot/subsystems/swervedrive/SwerveSubsystem.java) içinde yalnızca onunla etkileşim kurmanız gerekir.

<pre class="language-java"><code class="lang-java">import java.io.File;
import edu.wpi.first.wpilibj.Filesystem;
import swervelib.parser.SwerveParser;
import swervelib.SwerveDrive;
import edu.wpi.first.math.util.Units;


double <a data-footnote-ref href="#user-content-fn-1">maximumSpeed </a>= Units.feetToMeters(4.5)
File swerveJsonDirectory = new File(Filesystem.getDeployDirectory(),"swerve");
SwerveDrive  swerveDrive = new SwerveParser(directory).createSwerveDrive(<a data-footnote-ref href="#user-content-fn-2">maximumSpeed</a>);

</code></pre>

Bu yol hızlı ve kolaydır, artık endişelenecek büyük, bakımı zor ve ürkütücü sabitler dosyası yok! Bir JSON dizini oluşturmak için [konfigürasyon dokümantasyonuna](configuration/) bakın.

## Telemetri

Telemetri istediğinizde harika olabilir ve YAGSL'de sürücü panelinde göreceğiniz `Module[...]` alanları gibi çok sayıda yararlı telemetri vardır. Ancak Telemetri programda gecikmelere ve yavaşlamalara neden olur, bu nedenle bazen bunları kapatmak en iyisidir. Bunu yapmak için şunu değiştirin:

<pre class="language-java"><code class="lang-java">import swervelib.telemetry.SwerveDriveTelemetry;
import swervelib.telemetry.SwerveDriveTelemetry.TelemetryVerbosity;

<a data-footnote-ref href="#user-content-fn-3">SwerveDriveTelemetry.verbosity</a> = <a data-footnote-ref href="#user-content-fn-4">TelemetryVerbosity.HIGH</a>;
</code></pre>

## Örneği buradan takip edin!

{% embed url="https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/frc/robot" %}

{% hint style="info" %}
Bazen örneğe gerçekten gelişmiş özellikler eklemeyi severim (geçen yıl noktaya sürüş komutum olduğu gibi) bu yüzden tekrar kontrol edip ne yaptığımızı gördüğünüzden emin olun!
{% endhint %}

## Sürüş Kodu

`SwerveSubsystem` içinde kendi sürüş kodunuzu birkaç satır kadar kolay hale getirebilirsiniz.

```java
  /**
   * Command to drive the robot using translative values and heading as a setpoint.
   *
   * @param translationX Translation in the X direction.
   * @param translationY Translation in the Y direction.
   * @param headingX     Heading X to calculate angle of the joystick.
   * @param headingY     Heading Y to calculate angle of the joystick.
   * @return Drive command.
   */
  public Command driveCommand(DoubleSupplier translationX, DoubleSupplier translationY, DoubleSupplier headingX,
                              DoubleSupplier headingY)
  {
    return run(() -> {

      Translation2d scaledInputs = SwerveMath.scaleTranslation(new Translation2d(translationX.getAsDouble(),
                                                                                 translationY.getAsDouble()), 0.8);

      // Make the robot move
      driveFieldOriented(swerveDrive.swerveController.getTargetSpeeds(scaledInputs.getX(), scaledInputs.getY(),
                                                                      headingX.getAsDouble(),
                                                                      headingY.getAsDouble(),
                                                                      swerveDrive.getOdometryHeading().getRadians(),
                                                                      swerveDrive.getMaximumVelocity()));
    });
  }

  /**
   * Command to drive the robot using translative values and heading as angular velocity.
   *
   * @param translationX     Translation in the X direction.
   * @param translationY     Translation in the Y direction.
   * @param angularRotationX Rotation of the robot to set
   * @return Drive command.
   */
  public Command driveCommand(DoubleSupplier translationX, DoubleSupplier translationY, DoubleSupplier angularRotationX)
  {
    return run(() -> {
      // Make the robot move
      swerveDrive.drive(new Translation2d(translationX.getAsDouble() * swerveDrive.getMaximumVelocity(),
                                          translationY.getAsDouble() * swerveDrive.getMaximumVelocity()),
                        angularRotationX.getAsDouble() * swerveDrive.getMaximumAngularVelocity(),
                        true,
                        false);
    });
  }
```

[^1]: Maksimum hız Metre cinsinden OLMALIDIR!

[^2]: Maksimum hız Metre cinsinden OLMALIDIR!

[^3]: Bu [değer](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/telemetry/SwerveDriveTelemetry.html#verbosity) statiktir ve DriverStation ve SmartDashboard'a verilen telemetriyi değiştirir.

[^4]: [Telemetri Ayrınıtısı (Verbosity)](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/telemetry/SwerveDriveTelemetry.TelemetryVerbosity.html) birkaç farklı modda gelir.
