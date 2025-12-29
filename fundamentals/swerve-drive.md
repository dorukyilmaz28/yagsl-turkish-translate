---
description: Swerve Sürüşü nasıl çalışır?
---

# Swerve Sürüşü

<figure><img src="../.gitbook/assets/sim_sample.png" alt=""><figcaption><p>YAGSL'den Swerve Sürüşü simülasyonu</p></figcaption></figure>

## Bir Swerve Drive Oluştururken İpuçları

* Jiroskopu robotun ortasına yerleştirin, bu küçük bir sapmayı (drift) önlemeye ve daha doğru odometri sağlamaya yardımcı olacaktır.
* Mıknatısların (eğer kullanıyorsanız) doğru şekilde yapıştırıldığından emin olun!
* Zaman ayırın, yarışmalar sırasında 1 modülü inşaa ederken batıracağınızı veya başka bir şekilde yedeğe ihtiyacınız olacağını varsayın.
* Bir Swerve Sürüşünü programlamak zordur ve YAGSL bunu kolaylaştırmaya çalışsa da, ne yaptığınızı tam olarak anlamak için bilmeniz gereken birçok şey vardır!
* İş için doğru araçları kullanın! Bir Swerve Sürüşünde hata ayıklamak sadece metinle yeterince zordur, [AdvantageScope](https://github.com/Mechanical-Advantage/AdvantageScope/blob/main/docs/NAVIGATION.md) veya [FRC Web Components](https://github.com/frc-web-components/app/releases) gibi size yardımcı olacak mükemmel görselleştirme araçlarına sahip diğer Dashboard'ları deneyin!

## Temeller

Swerve Drive sistemleri, her bir tekerleği belirli bir açıya (azimuth) döndürerek ve tekerleği o yönde sürerek hareket eder. Bu sistemlerin en ayırt edici özelliği, dönme hareketinin doğrusal hareketten bağımsız olmasıdır. Bu sayede robot, herhangi bir yöne hareket ederken aynı anda farklı bir yöne bakabilir. Robot yerinde dönebilir ya da hareket hâlindeyken dönmeye devam edebilir. Robotun bu dönme hareketi ve yönelimi **“heading”** olarak adlandırılır.

## Swerve Drive Nedir?

Bir Swerve Drive sistemi genellikle 4 adet swerve modülünden ve bir jiroskoptan oluşur (jiroskopun robotun merkezine yerleştirilmesi önerilir). Her bir swerve modülü temel olarak bir sürüş motoru, bir açı/azimuth motoru ve bir mutlak (absolute) enkoder içerir.

Kullanılan motorlar, mutlak enkoderler ve jiroskoplar farklı üreticilerden olabilir ve birlikte çalışabilir; ancak başarı düzeyleri değişkenlik gösterebilir. Genel bir kural olarak, mümkünse tek bir donanım ekosistemine bağlı kalmak (örneğin tamamen REV veya tamamen CTRE) daha sorunsuz bir yapı ve daha zengin özellik seti sunar. Bununla birlikte, bu sistemler birbirinin aynısı değildir.

Farklı donanımların birlikte kullanıldığı tüm diğer senaryolarda ise YAGSL en uygun çözümdür. YAGSL, sensörleri ve motor sürücülerini işlevsel olarak eşdeğer hâle getirmeyi hedefleyen bir soyutlama yaklaşımıyla tasarlanmıştır.

#### Özet

Bir swerve drive şunlardan oluşur:

* [ ] Jiroskop
* [ ] Swerve Modülü
  * [ ] Açı/Azimut Motoru (+ kontrolcü)
  * [ ] Sürüş Motoru
  * [ ] Mutlak Enkoder

#### Başlıca Sorunlara Neden Olan Şeyler

* [ ] Kötü Ağırlık Merkezi
* [ ] Ortalanmamış jiroskop
* [ ] Kare olmayan sürüş sistemi

Bu tam bir liste değildir ve zamanla büyüyecektir.

## Swerve Drive kodda nasıl çalışır?

Swerve Drive, her modülü gitmek istediğiniz yöne ve bakmak istediğiniz başlığa göre belirlenen belirli bir açıya hareket ettirir. FRC için bu değerleri robotun kinematiğini hesaplayarak elle alabiliriz veya [`ChassisSpeeds`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/ChassisSpeeds.html) nesnesi verildiğinde her tekerleğin dönüşünün ve hızının ne olması gerektiğini belirlemek için modül konumlarını kullanan ve bir [`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html) dizisi döndüren [`SwerveDriveKinematics`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveDriveKinematics.html) kullanabiliriz. [`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html) daha sonra her Swerve Modülünün istenen başlığa bakarak istenen yönde gitmesi için karşılık gelen açıyı/azimutu ve hızı ayarlamak için kullanılabilir.

### `SwerveDriveKinematics`

<pre class="language-java" data-title="SwerveDrive.java" data-line-numbers data-full-width="false"><code class="lang-java">// Import relevant classes.
import edu.wpi.first.math.kinematics.SwerveDriveKinematics;
import edu.wpi.first.math.geometry.Translation2d;
import edu.wpi.first.math.util.Units;

// Example SwerveDrive class
public class SwerveDrive {

    // Attributes
<strong>    SwerveDriveKinematics kinematics;
</strong>    
    // Constructor
    public SwerveDrive() {
        // Create SwerveDriveKinematics object
        // 12.5in from center of robot to center of wheel.
        // 12.5in is converted to meters to work with object.
        // Translation2d(x,y) == Translation2d(front, left)
<strong>        kinematics = new SwerveDriveKinematics(
</strong><strong>            new Translation2d(Units.inchesToMeters(12.5), Units.inchesToMeters(12.5)), // Ön Sol
</strong><strong>            new Translation2d(Units.inchesToMeters(12.5), Units.inchesToMeters(-12.5)), // Ön Sağ
</strong><strong>            new Translation2d(Units.inchesToMeters(-12.5), Units.inchesToMeters(12.5)), // Arka Sol
</strong><strong>            new Translation2d(Units.inchesToMeters(-12.5), Units.inchesToMeters(-12.5))  // Arka Sağ
</strong><strong>        );
</strong>    }
}
</code></pre>

{% hint style="info" %}
Sıra, modül açısı/azimutlarının ve hızlarının çıktı sırasının ne olacağını tanımlar!
{% endhint %}

### `SwerveModuleState`

[`SwerveDriveKinematics`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveDriveKinematics.html), verilen sırada her modülün [`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html)'ini oluşturmak için kullanılır, aşağıdaki örnek bunu `drive()` fonksiyonunda verilen bir `ChassisSpeeds` nesnesi ile nasıl yapabileceğinizi gösterir.

[`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html), bir Swerve Modülünün özelliklerini yansıtan 2 özelliğe sahiptir: `angle` (açı) ve `speedMetersPerSecond` (saniyedeki metre hızı). Bunları aldıktan sonraki amaç, doğru swerve modülünü ([`SwerveDriveKinematics`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveDriveKinematics.html) nesnesinin oluşturulması sırasındaki sıraya göre) [`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html) içinde verilen açı ve hıza ayarlamaktır!

<pre class="language-java" data-title="SwerveDrive.java" data-line-numbers data-full-width="false"><code class="lang-java">// Import relevant classes.
import edu.wpi.first.math.kinematics.SwerveDriveKinematics;
import edu.wpi.first.math.geometry.Translation2d;
import edu.wpi.first.math.util.Units;
import edu.wpi.first.math.kinematics.SwerveModuleState;

// Example SwerveDrive class
public class SwerveDrive 
{

    // Attributes
    SwerveDriveKinematics kinematics;
    
    // Constructor
    public SwerveDrive() 
    {
        // Create SwerveDriveKinematics object
        // 12.5in from center of robot to center of wheel.
        // 12.5in is converted to meters to work with object.
        // Translation2d(x,y) == Translation2d(front, left)
        kinematics = new SwerveDriveKinematics(
            new Translation2d(Units.inchesToMeters(12.5), Units.inchesToMeters(12.5)), // Ön Sol
            new Translation2d(Units.inchesToMeters(12.5), Units.inchesToMeters(-12.5)), // Ön Sağ
            new Translation2d(Units.inchesToMeters(-12.5), Units.inchesToMeters(12.5)), // Arka Sol
            new Translation2d(Units.inchesToMeters(-12.5), Units.inchesToMeters(-12.5))  // Arka Sağ
        );
    }
    
    // Simple drive function
    public void drive()
    {
<strong>        // X=14in, Y=4in giden ve saniyede 30 derece dönen test ChassisSpeeds oluşturun.
</strong><strong>        ChassisSpeeds testSpeeds = new ChassisSpeeds(Units.inchesToMeters(14), Units.inchesToMeters(4), Units.degreesToRadians(30));
</strong>        
        // İstenen hızlar verildiğinde her modül için SwerveModuleStates'i alın.
<strong>        SwerveModuleState[] swerveModuleStates = kinematics.toSwerveModuleStates(testSpeeds);
</strong><strong>        // Çıktı sırası Ön-Sol, Ön-Sağ, Arka-Sol, Arka-Sağ şeklindedir
</strong>    }
}
</code></pre>

{% hint style="danger" %}
Swerve Drive kodu, modül konumlarını ve açılarını takip etmek için [`SwerveDriveOdometry`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveDriveOdometry.html) veya [`SwerveDrivePoseEstimator`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/estimator/SwerveDrivePoseEstimator.html) olmadan çalışmaz!
{% endhint %}

### `SwerveDriveOdometry`

Ne yazık ki hayat o kadar kolay değil. Robotumuzun mevcut konumunu, özellikle topluca **odometri** olarak bilinen **başlık**, **hız** ve **modül konumlarını** sürekli takip etmek zorundayız. Kullanılabilir [`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html) oluşturmanın tek doğru yolu budur.

<pre class="language-java" data-title="SwerveDrive.java" data-line-numbers data-full-width="false"><code class="lang-java">// Import relevant classes.
import edu.wpi.first.math.kinematics.SwerveDriveKinematics;
import edu.wpi.first.math.geometry.Translation2d;
import edu.wpi.first.math.util.Units;
import edu.wpi.first.math.kinematics.SwerveModuleState;
import edu.wpi.first.math.kinematics.SwerveModulePosition;
import edu.wpi.first.math.kinematics.SwerveDriveOdometry;
import edu.wpi.first.math.geometry.Pose2d;
import edu.wpi.first.wpilibj2.command.SubsystemBase;



// Example SwerveDrive class
public class SwerveDrive extends SubsystemBase
{

    // Attributes
    SwerveDriveKinematics kinematics;
<strong>    SwerveDriveOdometry   odometry;
</strong><strong>    Gyroscope             gyro; // Psuedo-class representing a gyroscope.
</strong><strong>    SwerveModule[]        swerveModules; // Psuedo-class representing swerve modules.
</strong>    
    // Constructor
    public SwerveDrive() 
    {
    
<strong>        <a data-footnote-ref href="#user-content-fn-1">swerveModules = new SwerveModule[4];</a> // Psuedo-code; Create swerve modules here.
</strong>        
        // Create SwerveDriveKinematics object
        // 12.5in from center of robot to center of wheel.
        // 12.5in is converted to meters to work with object.
        // Translation2d(x,y) == Translation2d(front, left)
        kinematics = new SwerveDriveKinematics(
            new Translation2d(Units.inchesToMeters(12.5), Units.inchesToMeters(12.5)), // Ön Sol
            new Translation2d(Units.inchesToMeters(12.5), Units.inchesToMeters(-12.5)), // Ön Sağ
            new Translation2d(Units.inchesToMeters(-12.5), Units.inchesToMeters(12.5)), // Arka Sol
            new Translation2d(Units.inchesToMeters(-12.5), Units.inchesToMeters(-12.5))  // Arka Sağ
        );
        
<strong>        gyro = new Gyroscope(); // Psuedo-constructor for generating gyroscope.
</strong>
<strong>        // Create the SwerveDriveOdometry given the current angle, the robot is at x=0, r=0, and heading=0
</strong><strong>        odometry = new SwerveDriveOdometry(
</strong><strong>            kinematics,
</strong><strong>            gyro.getAngle(), // returns current gyro reading as a Rotation2d
</strong><strong>            new SwerveModulePosition[]{new SwerveModulePosition(), new SwerveModulePosition(), new SwerveModulePosition(), new SwerveModulePosition},
</strong><strong>            // Front-Left, Front-Right, Back-Left, Back-Right
</strong><strong>            new Pose2d(0,0,new Rotation2d()) // x=0, y=0, heading=0
</strong>        );
            
    }
    
    // Simple drive function
    public void drive()
    {
        // Create test ChassisSpeeds going X = 14in, Y=4in, and spins at 30deg per second.
        ChassisSpeeds testSpeeds = new ChassisSpeeds(Units.inchesToMeters(14), Units.inchesToMeters(4), Units.degreesToRadians(30));
        
        // Get the SwerveModuleStates for each module given the desired speeds.
        SwerveModuleState[] swerveModuleStates = kinematics.toSwerveModuleStates(testSpeeds);
        // Output order is Front-Left, Front-Right, Back-Left, Back-Right
        
<strong>        swerveModules[0].setState(swerveModuleStates[0]);
</strong><strong>        swerveModules[1].setState(swerveModuleStates[1]);
</strong><strong>        swerveModules[2].setState(swerveModuleStates[2]);
</strong><strong>        swerveModules[3].setState(swerveModuleStates[3]);
</strong>    }
    
    // Fetch the current swerve module positions.
    public SwerveModulePosition[] getCurrentSwerveModulePositions()
    {
<strong>        return new SwerveModulePosition[]{
</strong><strong>            new SwerveModulePosition(swerveModules[0].getDistance(), swerveModules[0].getAngle()), // Front-Left
</strong><strong>            new SwerveModulePosition(swerveModules[1].getDistance(), swerveModules[1].getAngle()), // Front-Right
</strong><strong>            new SwerveModulePosition(swerveModules[2].getDistance(), swerveModules[2].getAngle()), // Back-Left
</strong><strong>            new SwerveModulePosition(swerveModules[3].getDistance(), swerveModules[3].getAngle())  // Back-Right
</strong><strong>        };
</strong>    }
    
    @Override
    public void periodic()
    {
<strong>        // Update the odometry every run.
</strong><strong>        <a data-footnote-ref href="#user-content-fn-2">odometry.update(gyro.getAngle(),  getCurrentSwerveModulePositions());</a>
</strong>    }
    
}
</code></pre>

{% hint style="info" %}
`SwerveDriveOdometry`, `SwerveDrivePoseEstimator` ile değiştirilebilir.
{% endhint %}

Swerve Sürüşü odometrisi, altsistemlerdeki `periodic` fonksiyonuna benzer şekilde her tekil çalıştırmada güncellenmelidir.

## Sonuç

Swerve Sürüşlerinin bu sayfada ele alınandan çok daha fazla karmaşıklığı vardır ancak bu, bir Swerve Sürüşünün nasıl programlanacağına dair temel bir anlayış için yeterlidir. Okuyucuyu, bazı püf noktalarını daha iyi anlamak için bulabildikleri kadar çok örneğe bakmaya veya YAGSL kullanmaya devam etmeye şiddetle teşvik ederim, İyi Şanslar!

[^1]: Bu olduğu gibi çalışmayacaktır ve bir `SwerveModule` sınıfını temsil eder.

[^2]: Bu isteğe bağlı değildir ve robotunuzun mevcut konumunu takip etmek ve doğru `SwerveModuleState`'ler üretmeye devam etmek için gereklidir.
