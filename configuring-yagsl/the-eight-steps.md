# Sekiz adım

## Bir şeyler yanlış ama sürülüyor gibi?

Ters çevirme durumu değişiklikleri işe yaramadığında ve bildiğiniz başka hiçbir şey sorunlarınızı çözmediğinde, bu tür kurulumların hata ayıklaması (debugging) acı verici ve yorucu olabilir. İşte bu hata ayıklamayı başarmak için ne yazık ki gerekli olan sekiz adım.

Şefkatle _"Robot başlığına dayalı Öteleme Ekseni değişimi"_ (robotunuzun dönüşüne bağlı olarak alan odaklı X ve Y ekseni değişimi) olarak bilinen bu adımlar, bunu bir yerlerde çözecektir.

## Robot kodunuzu hazırlayın.

Bu testlerin hızlı ve etkili bir şekilde yürütülmesi için lütfen sürüş kodunuz olarak aşağıdakini veya bir varyasyonunu kullanın. Bunu bir joystick'e uyarlamanız veya alınan eksen verilerini tersine çevirmeniz gerekebilir, ancak bu, sorunlarınızı daha hızlı gidermenize yardımcı olacaktır.

{% code title="RobotContainer.java" %}
```java
...
    SwerveSubsystem drivebase;
    CommandXboxController driverXbox;
...
    // Applies deadbands and inverts controls because joysticks
    // are back-right positive while robot
    // controls are front-left positive
    // left stick controls translation
    // right stick controls the desired angle NOT angular rotation
    Command driveFieldOrientedDirectAngle = drivebase.driveCommand(
        () -> MathUtil.applyDeadband(driverXbox.getLeftY(), OperatorConstants.LEFT_Y_DEADBAND),
        () -> MathUtil.applyDeadband(driverXbox.getLeftX(), OperatorConstants.LEFT_X_DEADBAND),
        () -> driverXbox.getRightX(),
        () -> driverXbox.getRightY());
        
    drivebase.setDefaultCommand(driveFieldOrientedDirectAngle);
....
```
{% endcode %}

<pre class="language-java" data-title="SwerveSubsystem.java"><code class="lang-java">...
public class SwerveSubsytem extends SubsystemBase
{
...
  SwerveDrive swerveDrive;
  /**
   * Command to drive the robot using translative values and heading as a setpoint.
   *
   * @param translationX Translation in the X direction. Cubed for smoother controls.
   * @param translationY Translation in the Y direction. Cubed for smoother controls.
   * @param headingX     Heading X to calculate angle of the joystick.
   * @param headingY     Heading Y to calculate angle of the joystick.
   * @return Drive command.
   */
  public Command driveCommand(DoubleSupplier translationX, DoubleSupplier translationY, DoubleSupplier headingX,
                              DoubleSupplier headingY)
  {
    // swerveDrive.setHeadingCorrection(true); // Normally you would want heading correction for this kind of control.
    return run(() -> {

      Translation2d scaledInputs = SwerveMath.scaleTranslation(new Translation2d(translationX.getAsDouble(),
                                                                                 translationY.getAsDouble()), 0.8);

      // Make the robot move
<strong>      driveFieldOriented(swerveDrive.swerveController.getTargetSpeeds(scaledInputs.getX(), scaledInputs.getY(),
</strong><strong>                                                                      headingX.getAsDouble(),
</strong><strong>                                                                      headingY.getAsDouble(),
</strong><strong>                                                                      swerveDrive.getOdometryHeading().getRadians(),
</strong><strong>                                                                      swerveDrive.getMaximumVelocity()));
</strong>    });
  }
  
  /**
   * Drive the robot given a chassis field oriented velocity.
   *
   * @param velocity Velocity according to the field.
   */
  public void driveFieldOriented(ChassisSpeeds velocity)
  {
    swerveDrive.driveFieldOriented(velocity);
  }
...
</code></pre>

Bu kod parçası doğrudan YAGSL-Example projesinden alınmıştır, eğer o projeyi kullanıyorsanız sadece `SwerveSubsystem` için varsayılan komut olarak `driveFieldOrientedDirectAngle` kullandığınızdan ve gerekli joystick ters çevirmelerini düzelttiğinizden emin olmanız gerekir.

## Sekiz adım.

{% hint style="danger" %}
**Adımlar tehlikelidir!**

Bunlardan 6 tanesi robotunuzun kontrolden çıkmasına neden olacaktır.

Bunlardan 1 tanesi doğru olacaktır.

Bunlardan 1 tanesi doğru gibi görünecek ancak robot başlığına (heading) dayalı olarak öteleme ekseni değişikliğine sahip olacaktır.
{% endhint %}

{% hint style="warning" %}
Çalışan bir swerve sürüşü elde etmek için bu adımların hepsini tamamlamanız beklenmez, sorununuz bir yerlerde ortadan kalkmalıdır.
{% endhint %}

1. `swervedrive.json` içindeki `invertIMU` değerini `false` **VE** modül JSON'larındaki `drive` `invert` değerini `false` yaparak başlayın.
2. SONRA `invertIMU` değerini `true` yapın.
3. SONRA modül JSON'larındaki tüm sürüş motorlarını `true`'ya ayarlayarak ters çevirin.
4. SONRA `invertIMU` değerini `false` yapın.
5. SONRA [modülleri ters yüz edin (flip)](#user-content-fn-1)[^1].\\

    <figure><img src="../.gitbook/assets/image-48.png" alt=""><figcaption><p>Modüllerin doğru şekilde ters yüz edilmesinin tasviri.</p></figcaption></figure>
6. SONRA tüm sürüş motorlarını `false` yaparak ters çevirmeyi kaldırın.
7. SONRA `invertIMU` değerini `true` yapın.
8. SONRA sürüş motorlarınızın ters çevirme durumlarını (inversion states) `true` yapın.

{% hint style="danger" %}
EĞER bunlardan hiçbiri işe yaramazsa, büyük olasılıkla yanlış bir donanım yapılandırmanız vardır, bir şeyler beklendiği gibi çalışmıyordur veya bir şeyler yanlış kablolanmıştır.
{% endhint %}

## Davranışı doğrulama

Bazen 8 adım gerçekten bitmiş olsa da bitmiş gibi görünmez. Burada botun aslında doğru ayarlandığı ancak robotun istenen ön tarafının aslında robotun arkası olduğu bir örnek verilmiştir.



<details>

<summary>Modül konfigürasyonları nasıl değiştirilir</summary>

Örnekler için daha az kafa karıştırıcı olması adına sayılarla etiketliyoruz, ancak modül dosyalarını değiştirirken sayıları ilgili ilk modül konfigürasyon adlarına atarız. Yukarıdaki örnek için aşağıdaki gibidir:

1. `frontleft.json`
2. `frontright.json`
3. `backleft.json`
4. `backright.json`

**`frontleft.json` ile `backright.json`'ı değiştirmek**

<pre class="language-json" data-title="frontleft.json"><code class="lang-json">{
<strong>  "drive": {
</strong><strong>    "type": "sparkmax",
</strong><strong>    "id": 4,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "angle": {
</strong><strong>    "type": "sparkmax",
</strong><strong>    "id": 3,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "encoder": {
</strong><strong>    "type": "cancoder",
</strong><strong>    "id": 9,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "inverted": {
</strong><strong>    "drive": false,
</strong><strong>    "angle": false
</strong><strong>  },
</strong><strong>  "absoluteEncoderOffset": -114.609,
</strong>  "location": {
    "front": 12,
    "left": 12
  }
}
</code></pre>

<pre class="language-json" data-title="backright.json"><code class="lang-json"><strong>{
</strong><strong>  "drive": {
</strong><strong>    "type": "sparkmax",
</strong><strong>    "id": 5,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "angle": {
</strong><strong>    "type": "sparkmax",
</strong><strong>    "id": 6,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "encoder": {
</strong><strong>    "type": "cancoder",
</strong><strong>    "id": 11,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "inverted": {
</strong><strong>    "drive": false,
</strong><strong>    "angle": false
</strong><strong>  },
</strong><strong>  "absoluteEncoderOffset": -18.281,
</strong>  "location": {
    "front": -12,
    "left": -12
  }
}
</code></pre>

Vurgulanan satırları değiştirin ve modül konfigürasyonlarını doğru şekilde değiştirmiş olursunuz.

#### Kolay yol

1. Konum olumsuzlamalarını (negations) istenen modül tarafına değiştirin.
2. Dosyaları birbirinin üzerine yazmadan yeniden adlandırın.

</details>

[^1]: Sürüş VE açı motor kontrolcüleri VE mutlak enkoderler için cihaz konfigürasyonunu aşağıdaki şekilde değiştirin.\
    \
    (Front Left -> Back Right)  \
    (Front Right -> Back Left)  \
    (Back Left -> Front Right)  \
    (Back Right -> Front Left) &#x20;
