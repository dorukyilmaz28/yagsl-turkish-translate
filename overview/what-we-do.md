---
description: Swerve sürüşünüzü çalıştırıyoruz!
---

# Ne yapıyoruz

## YAGSL programımda nasıl konumlanır?

YAGSL esasen, [WPILib](https://docs.wpilib.org/en/stable/docs/software/hardware-apis/motors/wpi-drive-classes.html)'den bildiğimiz [`DifferentialDrive`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj/drive/DifferentialDrive.html) gibi davranmayı amaçlayan ancak Swerve Sürüşleri için olan tek bir sınıfa [`SwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html) indirgenir.

<figure><img src="../.gitbook/assets/yagsl.png" alt="created by DeltaDizzy"><figcaption><p>Bir Sürüş Alt Sistemini ve <code>SwerveDrive</code>'ın buna nasıl oturduğunu gösteren diyagram. (DeltaDizzy tarafından oluşturuldu)</p></figcaption></figure>

## Bu rehberin amaçları

* İsterseniz kendiniz programlayabilmeniz veya YAGSL'i değiştirebilmeniz için `SwerveDrive` ve `SwerveModule`'ün temellerini öğretmek.
* Örnek üzerinden bir YAGSL projesi kurmanızda size rehberlik etmek.
* Bu rehberle programınız şunları yapabilecek kapasitede olacaktır:
  * Otonom (PathPlanner + entegre komutlar ile)
  * Swerve Sürüşü teleop kodu.
