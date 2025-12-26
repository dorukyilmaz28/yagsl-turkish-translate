---
description: >-
  YAGSL odometriyi sizin için halleder ve istediğiniz veriyi ekleyebilmeniz için genişletir!
---

# Görüntü Odometrisi (Vision Odometry)

## Vision Odometry Nedir?

Görüntü odometrisi (vision odometry) verisi normalde [`SwerveDrivePoseEstimator.addVisionMeasurement`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/estimator/PoseEstimator.html#addVisionMeasurement\(edu.wpi.first.math.geometry.Pose2d,double,edu.wpi.first.math.Matrix\)) kullanılarak eklenir ve YAGSL [`SwerveDrivePoseEstimator`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/estimator/SwerveDrivePoseEstimator.html)'ı sizin için hallettiğinden, kendi tahmincisinizi (estimator) oluşturmak yerine [`SwerveDrive.addVisionMeasurement`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#addVisionMeasurement\(edu.wpi.first.math.geometry.Pose2d,double\)) ile görüntü ölçümlerini işlemek için [`SwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html) içindeki işlevleri genişletiyoruz.

## Vision Odometry'i Nasıl Kullanırım?

YAGSL-Example'da sahte görüntü ölçümleri kullanırken sahte bir kullanım senaryosu gösterdiğimiz bir örnek kullanım vardır. Poz tahmincisi olarak etkili bir şekilde [`SwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html) sınıfını kullanırsınız.

<pre class="language-java"><code class="lang-java">/**
 * Add a fake vision reading for testing purposes.
 */
public void addFakeVisionReading()
{
<strong>  swerveDrive.addVisionMeasurement(new Pose2d(3, 3, Rotation2d.fromDegrees(65)), Timer.getFPGATimestamp());
</strong>}
</code></pre>
