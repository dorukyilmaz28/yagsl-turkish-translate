---
description: Swerve Modülü Nedir?
---

# Swerve Modülleri

Diğer takımların kodlarında `SwerveModule`'ü temsil eden bir sürü farklı sınıf görebilir ve neden standart bir sınıf olmadığını merak edebilirsiniz. Bunun çok iyi bir nedeni var, her motor, mutlak enkoder, dişli oranı ve kurulum farklı olabilir! Bazı takımlar Swerve Sürüşlerinde daha fazla sorunu önlemeye çalışırlar çünkü hata ayıklamak için daha fazla zamanları olmuştur. YAGSL, tüm yaygın sorunları dikkate almayı ve bunları JSON konfigürasyon dosyalarında ele almayı amaçlamaktadır.

{% hint style="warning" %}
Manyetik bir enkoder kullanıyorsanız, mıknatısın kaymaması için doğru şekilde yapıştırıldığından emin olun.
{% endhint %}

## Bir Swerve Modülünde ne var?

* [ ] Sürüş Dişlileri (oran bilinmelidir)
* [ ] Dümenleme (Steering) Dişlileri (oran bilinmelidir)
* [ ] Sürüş Motoru (+ kontrolcü)
* [ ] Açı/Azimut/Dümenleme Motoru (+ kontrolcü)
* [ ] Mutlak Enkoder

## Gözden Geçirme

Bu yersiz görünebilir ancak swerve sürüşlerinde hata ayıklarken çok çabuk işe yarar!

Akıllı Motor Kontrolcüler tipik olarak aşağıdaki özelliklere sahiptir

* [ ] Her iki yönde dönebilme.
* [ ] motorda her iki yönde okuyan sensörlere sahip olma.
* [ ] Sıkıştığında veya hareket edemediğinde yanarak çok yüksek amper kullanımı.
* [ ] Çalışırken mevcut voltaj seviyesini düşürme.
* [ ] Sürtünmeye karşı dönmek için minimum miktarda voltaja ihtiyaç duyma.
* [ ] Şafta bağlı yağlanmış dişliler.
* [ ] Anında çok fazla güç kullanmaktan kaçınmak için yapılandırılabilir bir oranda hıza çıkma (Ramp up).
* [ ] Bağlı bir sensör girişine (tipik olarak bir enkoder) dayalı olarak çıktıyı kontrol edebilen entegre PID döngülerine sahip olma.
* [ ] Bir CAN veriyoluna bağlı olma, varsayılan olarak `rio`'dur ancak bir [CANivore](https://store.ctr-electronics.com/canivore/) bağlıysa motor kontrolcüsü desteklediği sürece [CANivore](https://store.ctr-electronics.com/canivore/) adı da olabilir.
* [ ] Tekerleği dişlilerle orantılı olarak birden fazla mil dönüşünde döndürme.

Bir Swerve Modülünü düzgün bir şekilde yapılandırmak için tüm bunların doğru ayarlanması gerekir. Bunlardan biri doğru ayarlanmazsa, kolayca tanımlayamayacağınız davranışlarla karşılaşabilirsiniz.

#### Özet

1. Motorlar birçok şekilde bozulabilir ve yalnızca tek bir şekilde çalışması beklenir, hata ayıklarken buraya başvurun.
2. Swerve Modülleri, **sürüş dişlileri**, **dümenleme dişlileri**, **sürüş motoru**, **dümenleme motoru** ve bir **mutlak enkoder** içerir.

## Kontrol Listesi

* [ ] Dümenleme/Azimut/Açı motoru [mutlak enkoder değeriyle artıyor](#user-content-fn-1)[^1].
* [ ] Dümenleme/Azimut/Açı motoru saat yönünün tersine pozitif artıyor.
* [ ] Sürüş motorları robotu "ileri" iterek artıyor
* [ ] Mutlak Enkoderler Swerve Modülüne güvenli bir şekilde oturtulmuş.
* [ ] Dönüşüm Faktörü doğru hesaplanmış.
* [ ] Tekerleğin aynı yöne baktığı mutlak enkoder ofseti yapılandırılmış.

{% hint style="warning" %}
Mutlak enkoder ofsetini almak için tekerlekler, konik dişliler (bevels) aynı yöne bakacak şekilde hizalanmalıdır.
{% endhint %}

## Genel Bakış

Swerve Modülleri çok hızlı bir şekilde çok karmaşık hale gelebilir. Bu örneği basit tutacağım ve gelecekte genişletebilirim. Yukarıdaki adımların tümünü içermeyecektir ancak yapıcıda (constructor) bunun için yer olacaktır. Bu öğreticinin amaçları doğrultusunda, daha ayrıntılı olabildiği için REVLib'den [`CANSparkMax`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkmax) kullanacağım.

## Temeller

REVLib kullanarak koddaki modülü temsil eden bir swerve modülü sınıfı oluşturuyoruz.

```java
import com.revrobotics.CANSparkMax;
import com.ctre.phoenix6.hardware.CANcoder;


public class SwerveModule {

    private CANSparkMax driveMotor;
    private CANSparkMax steerMotor;
    private CANcoder    absoluteEncoder;
    
    public SwerveModule(int driveMotorCANID, int steerMotorCANID, int cancoderCANID)
    {
        driveMotor = new CANSparkMax(driveMotorCANID);
        steerMotor = new CANSparkMax(steerMotorCANID);
        absoluteEncoder = new CANcoder(cancoderCANID);
        
        // Reset everything to factory default
        driveMotor.restoreFactoryDefaults();
        steerMotor.restoreFactoryDefaults();
        absoluteEncoder.getConfigurator().apply(new CANcoderConfiguration());
        
        // Continue configuration here..
        
    }

}
```

Sınıf basitçe sürüş ve dümenleme motorlarını ve mutlak enkoderi uygular. Bu çok temel yapıcıdır. Her şey donanım istemcileri aracılığıyla yapılandırılmışsa motorları ve mutlak enkoderleri fabrika varsayılanına döndürmeniz gerekmez, ancak bu önerilmez.

## Konfigürasyon

Bir swerve modülünü yapılandırmak SON DERECE ÖNEMLİDİR!! Çok fazla sabır gerektirir ve muhtemelen ilk denemede asla çalıştıramayacaksınız. Burada gerekli adımları inceleyeceğim.

### Mutlak Enkoder Ofsetleri

Mekanik ekibiniz aşırı hassasiyetle çalışmıyorsa ve mıknatısı swerve modülü tekerleği zaten düzken her bir modül için mükemmel bir şekilde ortalamıyorsa, mutlak enkoderin tekerlek yönünü doğru okuması için her modül için bir ofset ayarlamanız gerekecektir.

Bunu bir donanım istemcisi kullanarak yapabilirsiniz ve yapmalısınız, ancak istemiyorsanız mutlak enkoderin mevcut değerinin ne olduğunu yazdırmak için aşağıdaki gibi basit bir program yazabilirsiniz.

{% hint style="warning" %}
Mutlak Enkoder ofsetleri modülün nereye işaret etmesi gerektiğini belirler. Modüller önyüklemede (boot) veya düz gitmesi komut edildikten sonra düz ileriye işaret etmediğinde, Mutlak Enkoder Ofsetlerinizde **KESİNLİKLE** bir sorun vardır.

Bazen ofset sadece biraz kapalıysa, bir modül sürüklenebilir ve bu da **cezalarla sonuçlanabilir**.
{% endhint %}

```java
// Copyright (c) FIRST and other WPILib contributors.
// Open Source Software; you can modify and/or share it under the terms of
// the WPILib BSD license file in the root directory of this project.

package frc.robot;

import com.ctre.phoenix6.hardware.CANcoder;
import com.ctre.phoenix6.StatusSignal;
import com.ctre.phoenix6.signals.AbsoluteSensorRangeValue;
import com.ctre.phoenix6.signals.SensorDirectionValue;
import com.ctre.phoenix6.configs.CANcoderConfiguration;
import com.ctre.phoenix6.configs.CANcoderConfigurator;
import com.ctre.phoenix6.configs.MagnetSensorConfigs;
import edu.wpi.first.math.util.Units;


/**
 * The VM is configured to automatically run this class, and to call the functions corresponding to each mode, as
 * described in the TimedRobot documentation. If you change the name of this class or the package after creating this
 * project, you must also update the build.gradle file in the project.
 */
public class Robot extends TimedRobot
{

  private static Robot   instance;
  private CANcoder    absoluteEncoder;

  public Robot()
  {
    instance = this;
  }

  public static Robot getInstance()
  {
    return instance;
  }

  /**
   * This function is run when the robot is first started up and should be used for any initialization code.
   */
  @Override
  public void robotInit()
  {
   absoluteEncoder = new CANcoder(/* Change this to the CAN ID of the CANcoder */ 0);
   CANcoderConfigurator cfg = encoder.getConfigurator();
   cfg.apply(new CANcoderConfiguration());
   MagnetSensorConfigs  magnetSensorConfiguration = new MagnetSensorConfigs();
   cfg.refresh(magnetSensorConfiguration);
   cfg.apply(magnetSensorConfiguration
                  .withAbsoluteSensorRange(AbsoluteSensorRangeValue.Unsigned_0To1)
                  .withSensorDirection(SensorDirectionValue.CounterClockwise_Positive));
                  
  }

  /**
   * This function is called every 20 ms, no matter the mode. Use this for items like diagnostics that you want ran
   * during disabled, autonomous, teleoperated and test.
   *
   * <p>This runs after the mode specific periodic functions, but before LiveWindow and
   * SmartDashboard integrated updating.
   */
  @Override
  public void robotPeriodic()
  {
   StatusSignal<Double> angle = encoder.getAbsolutePosition().waitForUpdate(0.1);

   System.out.println("Absolute Encoder Angle (degrees): " + Units.rotationsToDegrees(angle.getValue()));
  }
}

```

### Ters Çevirme (Inversion)

Swerve modülünüze bağlı olarak, beklendiği gibi çalışması için motorlarınızın ters çevrilmesi gerekebilir.

{% hint style="warning" %}
Motor kontrolcünüzün ters çevirme durumu dümenleme/açı/azimutunuz için yanlış olduğunda, Swerve Modülü herhangi bir giriş verildiğinde ve bazen hareketsizken bile kontrolden çıkıp **DÖNECEKTİR**.
{% endhint %}

```java
import com.revrobotics.CANSparkMax;
import com.ctre.phoenix6.hardware.CANcoder;
import com.ctre.phoenix6.StatusSignal;
import com.ctre.phoenix6.signals.AbsoluteSensorRangeValue;
import com.ctre.phoenix6.signals.SensorDirectionValue;
import com.ctre.phoenix6.configs.CANcoderConfiguration;
import com.ctre.phoenix6.configs.CANcoderConfigurator;
import com.ctre.phoenix6.configs.MagnetSensorConfigs;
import edu.wpi.first.math.util.Units;


public class SwerveModule {

    private CANSparkMax driveMotor;
    private CANSparkMax steerMotor;
    private CANcoder    absoluteEncoder;
    
    public SwerveModule(int driveMotorCANID, int steerMotorCANID, int cancoderCANID)
    {
        driveMotor = new CANSparkMax(driveMotorCANID);
        steerMotor = new CANSparkMax(steerMotorCANID);
        absoluteEncoder = new CANcoder(cancoderCANID);
        
        // Reset everything to factory default
        driveMotor.restoreFactoryDefaults();
        steerMotor.restoreFactoryDefaults();
        absoluteEncoder.getConfigurator().apply(new CANcoderConfiguration());
        
        // Continue configuration here..
        
        // CANcoder Configuration
        CANcoderConfigurator cfg = encoder.getConfigurator();
        cfg.apply(new CANcoderConfiguration());
        MagnetSensorConfigs  magnetSensorConfiguration = new MagnetSensorConfigs();
        cfg.refresh(magnetSensorConfiguration);
        cfg.apply(magnetSensorConfiguration
                  .withAbsoluteSensorRange(AbsoluteSensorRangeValue.Unsigned_0To1)
                  .withSensorDirection(SensorDirectionValue.CounterClockwise_Positive));

        // Steering Motor Configuration
        steerMotor.setInverted(false);
        
        // Drive Motor Configuration
        driveMotor.setInverted(false);
    }

}
```

### Dönüşüm Faktörü

Matematik zamanı! Boyut analizini hatırlıyor musunuz?

{% embed url="https://youtu.be/hIAdCTNi1S8" %}
Birim dönüşümleri için Boyut Analizinin Kahn Academy Açıklaması
{% endembed %}

Swerve Modüllerine, hızı (Saniyedeki Metre) ve Açıyı (basitlik için derece olarak vereceğiz) ayarlamak için bir [`SwerveModuleState`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/kinematics/SwerveModuleState.html) nesnesi verilir. Bu da yerel birimleri (bizim durumumuzda dönüşler ve dakikadaki dönüşler) hız ve açı birimlerine dönüştürmemiz gerektiği anlamına gelir. Ayrıca motorun tam bir tekerlek dönüşü elde etmek için çalıştığı dişli oranını da biliyoruz.

Dümenleme dönüşüm faktörü, rotorun (veya sparkmax veri portuna bağlıysa mutlak enkoderin) _**dönüşlerini**_ alır ve bunları _**derecelere**_ dönüştürür.

Bu örnek için dişli oranının `12.8:1` [(SDS MK4 Dümenleme Oranı)](https://www.swervedrivespecialties.com/collections/kits/products/mk4-swerve-module) olduğunu varsayacağız, yani rotor bir mekanizma dönüşünü tamamlamak için `12.8` kez döner.

$$
SteeringConverionFactor = \frac{1_{degree}}{1_{rot}} = \frac{1_{rot}}{12.8_{rot}} * \frac{1_{rot}}{360_{deg}}
$$

Sürüş dönüşüm faktörü, motor enkoderi tarafından verilen _**dönüşler/dakika**_'yı alacak ve bunları _**metre/saniye**_'ye dönüştürecektir.

Aşağıdaki örnek için dişli oranı `6.75:1` [(SDS MK4 L2 Sürüş Oranı)](https://www.swervedrivespecialties.com/collections/kits/products/mk4-swerve-module) kullanacağız, yani tekerleğin bir dönüşü tamamlaması için rotor `6.75` kez döner.

$$
DriveConversionFactor = \frac{\frac{1_{meter}}{1_{sec}}}{\frac{1_{rot}}{1_{min}}} = \frac{1_{rot}}{1_{min}} * \frac{1_{rot}}{6.75_{rot}} * \frac{60_{sec}}{1_{min}} * \frac{\pi*d_{meters}}{1_{rot}}
$$

{% hint style="warning" %}
YAGSL için sürüş dönüşüm faktörü, aşağıdaki örnekteki gibi RPM'den MPS'ye değil, dönüşleri metrelere dönüştürür.
{% endhint %}

Bütün bunlar, matematiğin önemli olduğunu ve dönüşüm faktörlerinizin sihirli sayılar olmadığını göstermenin uzun yoludur!!

{% hint style="warning" %}
Dönüşüm faktörü son derece önemlidir ve eğer yanlışsa motor kontrolden çıkıp **DÖNEBİLİR** veya odometriniz her zaman biraz kapalı olacak ve etrafta sürerken daha abartılı hareketlerle sonuçlanacaktır.
{% endhint %}

### PID Kontrolü

PID, Oransal-İntegral-Türev (Percent-Integral-Derivative) anlamına gelir. Swerve Sürüşleri en güncel geri bildirim sensörlerini kullanmaya çalışmalıdır, bu nedenle SparkMAX'in dahili PID özelliğini kullanacağız.

WPILib'in burada PID'leri öğrenmek için harika bir rehberi var. Taret konumu örneği, dümenleme motorlarını nasıl kontrol edeceğimizdir.

{% embed url="https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/introduction-to-pid.html" %}

REV'in bu konudaki belgeleri mevcuttur ve SparkMAX kontrolcüsünde (çoğunlukla) nasıl çalıştığını gösterir.

{% embed url="https://docs.revrobotics.com/sparkmax/operating-modes/closed-loop-control" %}

Bir Swerve Modülünü kontrol etmek için oluşturmanız gereken 2 PID vardır, biri sürüş motoru için, diğeri dümenleme motorları için.

#### Sürüş Motoru PID'si

WPILib belgelerindeki örneğe dayanarak, bunu sadece burada belgelenen bir volan (fly-wheel) gibiymiş gibi ayarlamanız gerekir.

{% embed url="https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-flywheel.html" %}

Bir sürüş tekerleği için, PID'nin robotun ağırlığı üzerindeyken tekerleği hareket ettirecek minimum voltajın üzerine çıkmak zorunda kalmamasını sağlamak için her zaman kullanmak isteyebileceğiniz bir ileri besleme (feedforward) olabilir.

#### Dümenleme Motoru PID'si

Dümenleme Motoru PID'si, geri bildirim sensörüne dayalı olarak tekerleğin açısını derece cinsinden kontrol eder. Ancak bunu etkili bir şekilde yapmak için birkaç püf noktası gereklidir.

1. PID Sarma (Wrapping), tekerleğin her zaman hedef açıya giden en kısa yolu seçmesini sağlar.
2. Dişlilerinizi sık sık yağlayın!!!
3. Doğru dönüşüm faktörünü hesaplayın.
4. Donanım istemcisi veya Tuner X kullanarak hızlı ve doğru bir şekilde ayarlayın.

WPILib, tam olarak aynı prensip olan bir taret konumu kontrolcüsü hakkında bazı belgelere sahiptir.

{% embed url="https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-turret.html" %}

### Akım Sınırlama

Çok fazla güç çekmekten ve voltaj düşüşünden (browning out) kaçınmak için motorlarınızın akımlarını sınırlamalısınız, tipik olarak bunlar dümenleme motorları için 20A ve sürüş motorları için 40A aralığındadır.

{% hint style="warning" %}
SparkMAX'ler yalnızca stator sınırlarını uygulayabilir.
{% endhint %}

{% embed url="https://v6.docs.ctr-electronics.com/en/stable/docs/hardware-reference/talonfx/improving-performance-with-current-limits.html" %}

## Örnek Kod

```java
import com.revrobotics.CANSparkMax;
import com.ctre.phoenix6.hardware.CANcoder;
import com.ctre.phoenix6.StatusSignal;
import com.ctre.phoenix6.signals.AbsoluteSensorRangeValue;
import com.ctre.phoenix6.signals.SensorDirectionValue;
import com.ctre.phoenix6.configs.CANcoderConfiguration;
import com.ctre.phoenix6.configs.CANcoderConfigurator;
import com.ctre.phoenix6.configs.MagnetSensorConfigs;
import edu.wpi.first.math.util.Units;
import com.revrobotics.RelativeEncoder;
import com.revrobotics.SparkMaxPIDController;


public class SwerveModule {

    private CANSparkMax driveMotor;
    private CANSparkMax steerMotor;
    private CANcoder    absoluteEncoder;
    private SparkMaxPIDController drivingPIDController;
    private SparkMaxPIDController turningPIDController;
    private RelativeEncoder driveEncoder;
    private RelativeEncoder steerEncoder;
    
    public SwerveModule(int driveMotorCANID, int steerMotorCANID, int cancoderCANID)
    {
        driveMotor = new CANSparkMax(driveMotorCANID);
        steerMotor = new CANSparkMax(steerMotorCANID);
        absoluteEncoder = new CANcoder(cancoderCANID);
        
        // Get the PID Controllers
        drivingPIDController = driveMotor.getPIDController();
        turningPIDController = steerMotor.getPIDController();
        
        // Get the encoders
        driveEncoder = driveMotor.getEncoder():
        steerEncoder = steerMotor.getEncoder();
        
        // Reset everything to factory default
        driveMotor.restoreFactoryDefaults();
        steerMotor.restoreFactoryDefaults();
        absoluteEncoder.getConfigurator().apply(new CANcoderConfiguration());
        
        // Continue configuration here..
        
        // CANcoder Configuration
        CANcoderConfigurator cfg = encoder.getConfigurator();
        cfg.apply(new CANcoderConfiguration());
        MagnetSensorConfigs  magnetSensorConfiguration = new MagnetSensorConfigs();
        cfg.refresh(magnetSensorConfiguration);
        cfg.apply(magnetSensorConfiguration
                  .withAbsoluteSensorRange(AbsoluteSensorRangeValue.Unsigned_0To1)
                  .withSensorDirection(SensorDirectionValue.CounterClockwise_Positive));

        // Steering Motor Configuration
        steerMotor.setInverted(false);
        turningPIDController.setFeedbackDevice(steerEncoder);
        // Apply position and velocity conversion factors for the turning encoder. We
        // want these in radians and radians per second to use with WPILib's swerve
        // APIs.
        steerEncoder.setPositionConversionFactor(ModuleConstants.kTurningEncoderPositionFactor);
        steerEncoder.setVelocityConversionFactor(ModuleConstants.kTurningEncoderVelocityFactor);
        // Enable PID wrap around for the turning motor. This will allow the PID
        // controller to go through 0 to get to the setpoint i.e. going from 350 degrees
        // to 10 degrees will go through 0 rather than the other direction which is a
        // longer route.
        turningPIDController.setPositionPIDWrappingEnabled(true);
        turningPIDController.setPositionPIDWrappingMinInput(0);
        turningPIDController.setPositionPIDWrappingMaxInput(90);
        // Set the PID gains for the turning motor. Note these are example gains, and you
        // may need to tune them for your own robot!
        turningPIDController.setP(ModuleConstants.kTurningP);
        turningPIDController.setI(ModuleConstants.kTurningI);
        turningPIDController.setD(ModuleConstants.kTurningD);
        turningPIDController.setFF(ModuleConstants.kTurningFF);
        
        // Drive Motor Configuration
        driveMotor.setInverted(false);
        drivingPIDController.setFeedbackDevice(driveEncoder);
        // Apply position and velocity conversion factors for the driving encoder. The
        // native units for position and velocity are rotations and RPM, respectively,
        // but we want meters and meters per second to use with WPILib's swerve APIs.        
        driveEncoder.setPositionConversionFactor(ModuleConstants.kDrivingEncoderPositionFactor);        
        driveEncoder.setVelocityConversionFactor(ModuleConstants.kDrivingEncoderVelocityFactor);
        // Set the PID gains for the driving motor. Note these are example gains, and you
        // may need to tune them for your own robot!
        drivingPIDController.setP(ModuleConstants.kDrivingP);
        drivingPIDController.setI(ModuleConstants.kDrivingI);
        drivingPIDController.setD(ModuleConstants.kDrivingD);
        drivingPIDController.setFF(ModuleConstants.kDrivingFF);
        
        // Save the SPARK MAX configurations. If a SPARK MAX browns out during
        // operation, it will maintain the above configurations.
        driveMotor.burnFlash();
        steerMotor.burnFlash();
          
        driveEncoder.setPosition(0);
        steerEncoder.setPosition(encoder.getAbsolutePosition().refresh().getValue() * 360);
    }
    
    
    /**
    Get the distance in meters.
    */
    public double getDistance()
    {
        return driveEncoder.getPosition();
    }
    
    /**
    Get the angle.
    */
    public Rotation2d getAngle()
    {
          return Rotation2d.fromDegrees(steerEncoder.getPosition());
    }
    
    /**
    Set the swerve module state.
    @param state The swerve module state to set.
    */
    public void setState(SwerveModuleState state)
    {
          turningPIDController.setReference(state.angle.getDegrees(), ControlType.kPosition);
          drivingPIDController.setReference(state.speedMetersPerSecond, ControlType.kVelocity);
    }

}
```

[^1]: Bu, koddaki motor kontrolcüsünün ters çevrilmesiyle düzeltilebilir.
