# Konfigürasyon

## Ayarlama (Tuning) Web Sayfası

YAGSL, sıfırdan konfigürasyon dosyaları oluşturmanıza yardımcı olmak için burada kısmen eksiksiz bir yapılandırma aracı bulundurur.

{% embed url="https://broncbotz3481.github.io/YAGSL-Example/" %}

Bu web sayfasından tüm dosyaları indirebilmeli ve [`new SwerveParser(new File(Filesystem.getDeployDirectory(),"swerve")`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveParser.html#%3Cinit%3E\(java.io.File\))[`.createSwerveDrive(Units.feetToMeters(4.5));`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveParser.html#createSwerveDrive\(double\)) için kullanmak üzere `deploy` dizininize yerleştirebilmelisiniz.

Ayrıca burada bilinen çalışan konfigürasyonlar için bir depo (repository) tutuyoruz!

{% embed url="https://github.com/BroncBotz3481/YAGSL-Configs" %}

## Hangi modülün ne olduğunu bildiğinizden emin olun!

Değilse modülleriniz böyle olabilir!.

<figure><img src="../../.gitbook/assets/id_change3.png" alt=""><figcaption><p>Modüller ters çevrilmiş, SAAT YÖNÜNÜN TERSİNE (CCW) dönüyor+</p></figcaption></figure>

Bu, jiroskopun robot üzerine tam olarak nerede durduğuna veya konfigürasyon dosyalarında yanlış modül konumlarındaki cihaz konfigürasyonlarına sahip olmanızdan dolayı modül konumlarını yanlış girdiğinizde gerçekleşir. **Eğer bu başınıza gelirse, modüllerinizi YANLIŞ yapılandırmışsınız DEMEKTİR.**

<details>

<summary>Modül konfigürasyonları nasıl değiştirilir</summary>

Örneklerde daha az kafa karışıklığı olması için numaralarla etiketliyoruz, ancak modül dosyalarını değiştirirken numaraları ilgili başlangıç modül konfigürasyon adlarına atarız. Yukarıdaki örnek için aşağıdaki gibidir

1. `frontleft.json`
2. `frontright.json`
3. `backleft.json`
4. `backright.json`

**`frontleft.json` ile `backleft.json`'ı değiştirme**

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

<pre class="language-json" data-title="backleft.json"><code class="lang-json"><strong>{
</strong><strong>  "drive": {
</strong><strong>    "type": "sparkmax",
</strong><strong>    "id": 7,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "angle": {
</strong><strong>    "type": "sparkmax",
</strong><strong>    "id": 8,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "encoder": {
</strong><strong>    "type": "cancoder",
</strong><strong>    "id": 12,
</strong><strong>    "canbus": null
</strong><strong>  },
</strong><strong>  "inverted": {
</strong><strong>    "drive": false,
</strong><strong>    "angle": false
</strong><strong>  },
</strong><strong>  "absoluteEncoderOffset": 6.504,
</strong>  "location": {
    "front": -12,
    "left": 12
  }
}
</code></pre>

Vurgulanan satırları değiştirin ve modül konfigürasyonlarını doğru şekilde değiştirmiş olursunuz.

**Kolay yol**

1. Konum negatifliklerini (negations) istenen modül tarafına değiştirin.
2. Dosyaları birbirinin üzerine yazmadan yeniden adlandırın.

</details>

#### Örnek konfigürasyon meydan okuması

<details>

<summary>Meydan Okuma</summary>

İşte size bir meydan okuma, bu yanlış konfigürasyonu nasıl çözebilirsiniz?

<img src="../../.gitbook/assets/id_spin1.png" alt="While rotating right" data-size="original"><img src="../../.gitbook/assets/challenge_reorder2.png" alt="Translating right" data-size="original">

</details>

<details>

<summary>Çözüm</summary>

<img src="../../.gitbook/assets/challenge_reorder1.png" alt="" data-size="original">

Adımlar:

1. 4 ve 2'yi ters çevirin.
2. 1 ve 4'ü değiştirin.

</details>

Bu, çabalarınızda size yardımcı olabilir!

{% file src="../../.gitbook/assets/SwerveDiagram.docx" %}

## Swerve modüllerinizi doğru şekilde yönlendirin!

`absoluteEncoderOffset` değerini doğru bir şekilde elde etmek için swerve modülleriniz değerleri okurken bu şekilde bakıyor olmalıdır.

<figure><img src="../../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption></figcaption></figure>

## Konfigürasyon Dizini

### JSON Dosyaları

JSON, "JavaScript Object Notation" anlamına gelir, konfigürasyon ve dize veri temsili için popüler bir formattır. [Buradan](https://www.w3schools.com/js/js_json_intro.asp) daha fazla bilgi edinebilirsiniz

### Swerve dizini neye benzemelidir?

Bir swerve sürüşü oluşturmak için swerve dizini böyle görünmelidir. Swerve modüllerinizi [`swervedrive.json`](swerve-drive-configuration.md)'da `"modules": [ "frontleft.json", "frontright.json", "backleft.json", "backright.json"]` olarak tanımladığınız varsayılırsa.

```
└── swerve
    ├── controllerproperties.json
    ├── modules
    │   ├── backleft.json
    │   ├── backright.json
    │   ├── frontleft.json
    │   ├── frontright.json
    │   ├── physicalproperties.json
    │   └── pidfproperties.json
    └── swervedrive.json
```

Swerve sürüşünü oluşturmak için `modules` klasörü, [`controllerproperties.json`](controller-properties-configuration.md), [`physicalproperties.json`](physical-properties-configuration.md), [`pidfproperties.json`](pidf-properties-configuration/) ve [`swervedrive.json`](swerve-drive-configuration.md) dosyaları gereklidir. Her birinin, swerve sürüşünün bir özelliğine (bazıları fiziksel, bazıları soyut) karşılık gelen belirli alanları vardır.

## Eski Konfigürasyon Dosyalarını Taşıma

1. `physicalproperties.json` dosyasından `wheelDiamter`, `gearRatio`, `encoderPulsePerRotation` alanlarını silin
2. `physicalproperties.json` dosyasına `optimalVoltage` ekleyin
3. `swervedrive.json` dosyasından `maxSpeed` ve `optimalVoltage` alanlarını silin
4. **EĞER** bir swerve modülü, swerve sürüşünün geri kalanıyla aynı sürüş motoruna veya dümenleme motoruna sahip değilse, modül konfigürasyonu JSON dosyasında HEM sürüş hem de dümenleme motoru için bir `conversionFactor` (dönüşüm faktörü) belirtmelisiniz. EĞER motorlardan biri swerve sürüşünün geri kalanıyla aynıysa ve o `conversionFactor`'ü kullanmak istiyorsanız, modül JSON konfigürasyonunda `conversionFactor`'ü 0 olarak ayarlayın.
5. `new SwerveParser(directory).createSwerveDrive(maximumSpeed);` aracılığıyla bir `SwerveDrive` oluştururken maksimum hızı belirtmelisiniz.
6. EĞER `swervedrive.json`'da `conversionFactor` ayarlamak istemiyorsanız. Bunu kurucuya (constructor) bir parametre olarak şu şekilde geçirebilirsiniz

```java
double DriveConversionFactor = SwerveMath.calculateMetersPerRotation(Units.inchesToMeters(WHEEL_DIAMETER), GEAR_RATIO, ENCODER_RESOLUTION);
double SteeringConversionFactor = SwerveMath.calculateDegreesPerSteeringRotation(GEAR_RATIO, ENCODER_RESOLUTION);
new SwerveParser(directory).createSwerveDrive(maximumSpeed, SteeringConversionFactor, DriveConversionFactor);
```
