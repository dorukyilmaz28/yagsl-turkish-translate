# Başlık (Heading) Düzeltme

## Başlık Düzeltme Nedir?

Başlık düzeltme, robot öteleme (translating) yaparken robot başlığını (yönünü) önceki başlık ile aynı tutmak için kullanılır. Agresiftir ve açısal rotasyon tabanlı kontrol şemalarının çalışmasını engelleyecektir.

Başlık düzeltme YAGSL'e Takım 1466 tarafından eklendi ve 7525 Pioneers ve 6036'dan BoiledBurntBagel tarafından geliştirildi.

## Nasıl etkinleştiririm?

Başlık düzeltmeyi herhangi bir yerden [`SwerveDrive.setHeadingCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setHeadingCorrection\(boolean\)) kullanarak etkinleştirebilir veya devre dışı bırakabilirsiniz. Ölü bant (deadband), hem saniyedeki metre hem de saniyedeki radyanı temsil eden keyfi bir değerdir.

## Başlık düzeltme kodda ne yapar?

Başlık düzeltme, [`SwerveDrive.setHeadingCorrection`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#setHeadingCorrection\(boolean,double\)) ölü bandı aracılığıyla başlığı kontrol etmek için [`SwerveDrive.drive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#drive\(edu.wpi.first.math.kinematics.ChassisSpeeds,boolean,edu.wpi.first.math.geometry.Translation2d\)) içinde kullanılır. Başlık düzeltme, [`SwerveController.headingCalculate`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveController.html#headingCalculate\(double,double\)) kullanarak bir omega dönüş hızı hesaplamak için `controllerproperties.json` dosyasındaki başlık PID'sini ve mevcut sapmayı (yaw) kullanır.

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
