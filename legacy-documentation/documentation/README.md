---
hidden: true
---

# Dokümantasyon

## Özellikler ve Kaynaklar

* Özellikler ve kaynaklar tartışmalar sayfasında [burada](https://github.com/BroncBotz3481/YAGSL-Example/discussions) bulunmaktadır https://github.com/BroncBotz3481/YAGSL-Example/discussions

## Swerve sürüşü nasıl oluşturulur?

YAGSL, tamamen JSON konfigürasyon dosyalarına dayalı bir swerve sürüşü oluşturabilmeniz gerçeğiyle benzersizdir. JSON konfigürasyon dosyaları [`deploy`](https://github.com/BroncBotz3481/YAGSL-Example/src/main/deploy) dizininde bulunmalıdır. Ayrıca Konfigürasyon nesnelerini manuel olarak oluşturabilir ve Swerve Sürüşünüzü bu şekilde örneklendirebilirsiniz.

### JSON kullanarak SwerveDrive nasıl oluşturulur.

Bu örnek program, [`SwerveSubsystem`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/frc/robot/subsystems/swervedrive2/SwerveSubsystem.java) içinde [`SwerveDrive`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/java/swervelib/SwerveDrive.java)'ı oluşturur, çünkü komut tabanlı programlama kullanıyorsanız SwerveSubsystem içinde yalnızca onunla etkileşime girmelisiniz.

```java
import java.io.File;
import edu.wpi.first.wpilibj.Filesystem;
import swervelib.parser.SwerveParser;
import swervelib.SwerveDrive;
import edu.wpi.first.math.util.Units;


double maximumSpeed = Units.feetToMeters(4.5)
File swerveJsonDirectory = new File(Filesystem.getDeployDirectory(),"swerve");
SwerveDrive  swerveDrive = new SwerveParser(directory).createSwerveDrive(maximumSpeed);

```

Bu yol hızlı ve kolaydır, endişelenecek daha fazla büyük bakımı yapılamayan ve göz korkutucu sabit dosyaları yok! Bir JSON dizini oluşturmak için JSON dokümantasyonuna bakın.

## Bir swerve sürüşü oluşturma.

* [ ] NavX, ReduxLib, CTRE ve REV satıcı (vendor) bağımlılıklarını kurun.
* [ ] YAGSL'yi kurun (`https://broncbotz3481.github.io/YAGSL-Lib/yagsl/yagsl.json`)
* [ ] [Örnek JSON dizinini](https://github.com/BroncBotz3481/YAGSL/tree/main/deploy) kopyalayın veya kendinizinkini oluşturun, ardından `src/main/frc/deploy/swerve` içine taşıyın veya [buradan](https://broncbotz3481.github.io/YAGSL-Example) bir tane oluşturun
* [ ] `SwerveDrive drive = new SwerveParser(new File(Filesystem.getDeployDirectory(), "swerve")).createSwerveDrive(maximumSpeed);` aracılığıyla JSON dizininden SwerveDrive oluşturun
* [ ] [docs/index.html](https://broncbotz3481.github.io/YAGSL/) içindeki java belgelerini görüntüleyin
* [ ] Deneyin!

## Eski Konfigürasyon Dosyalarını Taşıma

1. `physicalproperties.json` dosyasından `wheelDiamter`, `gearRatio`, `encoderPulsePerRotation` alanlarını silin
2. `physicalproperties.json` dosyasına `optimalVoltage` ekleyin
3. `swervedrive.json` dosyasından `maxSpeed` ve `optimalVoltage` alanlarını silin
4. **EĞER** bir swerve modülü, swerve sürüşünün geri kalanıyla aynı sürüş motoruna veya dümenleme motoruna sahip değilse, modül konfigürasyon JSON dosyasında HEM sürüş HEM DE dümenleme motoru için bir `conversionFactor` belirtmek **ZORUNDASINIZ**. EĞER motorlardan biri swerve sürüşünün geri kalanıyla aynıysa ve o `conversionFactor`'ü kullanmak istiyorsanız, modül JSON konfigürasyonundaki `conversionFactor`'ü 0 olarak ayarlayın.
5. `new SwerveParser(directory).createSwerveDrive(maximumSpeed);` aracılığıyla bir `SwerveDrive` oluştururken maksimum hızı belirtmek ZORUNDASINIZ
6. EĞER `conversionFactor`'ü `swervedrive.json` içinde ayarlamak istemiyorsanız. Bunu yapıcıya (constructor) şu şekilde bir parametre olarak geçirebilirsiniz

```java
double DriveConversionFactor = SwerveMath.calculateMetersPerRotation(Units.inchesToMeters(WHEEL_DIAMETER), GEAR_RATIO, ENCODER_RESOLUTION);
double SteeringConversionFactor = SwerveMath.calculateDegreesPerSteeringRotation(GEAR_RATIO, ENCODER_RESOLUTION);
new SwerveParser(directory).createSwerveDrive(maximumSpeed, SteeringConversionFactor, DriveConversionFactor);
```

## Katkılar

Bu kütüphane, çok çeşitli diğer kod tabanlarına ek olarak 95'in [SwervyBot koduna](https://github.com/first95/FRC2023/tree/main/SwervyBot) dayanmaktadır. Swerve kodlarını açık kaynaklı hale getiren her takıma çok teşekkürler!
