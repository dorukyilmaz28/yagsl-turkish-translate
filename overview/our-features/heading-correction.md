# Başlık (Heading) Düzeltme

## Heading Correction Nedir?

Heading Correction, robot hareket ederken (dönme hareketi yaparken) yönünün önceki heading değerinde kalmasını sağlamak için kullanılan bir kontrol mekanizmasıdır. Robot ileri–geri veya yana doğru giderken, kendi etrafında istemsiz dönmesini engeller.\
Bu sistem oldukça **agresif** çalışır ve bu nedenle açısal dönüşe dayalı kontrol şemalarıyla (örneğin joystick ile dönme) birlikte kullanıldığında çakışmalara neden olabilir.

Heading Correction, YAGSL’e Team 1466 tarafından eklenmiş; daha sonra 7525 Pioneers ve 6036’dan BoiledBurntBagel tarafından geliştirilmiştir.

## Nasıl etkinleştiririm?

Heading Correction, [`SwerveDrive.setHeadingCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setHeadingCorrection\(boolean\))  metodu kullanılarak istenilen yerden açılıp kapatılabilir. Burada kullanılan deadband değeri, hem metre/saniye cinsinden doğrusal hızları hem de radyan/saniye cinsinden açısal hızları temsil eden eşik değeridir.

## Heading Correction kodda ne yapar?

Heading Correction, [`SwerveDrive.drive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#drive\(edu.wpi.first.math.kinematics.ChassisSpeeds,boolean,edu.wpi.first.math.geometry.Translation2d\))  metodu içinde kullanılarak,  [`SwerveDrive.setHeadingCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setHeadingCorrection\(boolean,double\))  ile tanımlanan deadband üzerinden robotun yönünü kontrol eder. Bu süreçte, `controllerproperties.json` dosyasında tanımlı heading PID değerleri ve robotun anlık yaw bilgisi kullanılarak,  [`SwerveController.headingCalculate`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveController.html#headingCalculate\(double,double\)) metodu aracılığıyla bir açısal hız (omega) hesaplanır.

```java
    // Heading Angular Velocity Deadband, might make a configuration option later.
    // Başlık Açısal Hız Ölü Bandı, daha sonra bir konfigürasyon seçeneği yapılabilir.
    // Originally made by Team 1466 Webb Robotics.
    // Modified by Team 7525 Pioneers and BoiledBurntBagel of 6036
    if (headingCorrection)
    {
      if (Math.abs(velocity.omegaRadiansPerSecond) < HEADING_CORRECTION_DEADBAND
          && (Math.abs(velocity.vxMetersPerSecond) > HEADING_CORRECTION_DEADBAND
              || Math.abs(velocity.vyMetersPerSecond) > HEADING_CORRECTION_DEADBAND))
      {
        if (!correctionEnabled)
        {
          lastHeadingRadians = getYaw().getRadians();
          correctionEnabled = true;
        }
        velocity.omegaRadiansPerSecond =
            swerveController.headingCalculate(lastHeadingRadians, getYaw().getRadians());
      } else
      {
        correctionEnabled = false;
      }
    }
```
