# Fiziksel Özellikler Konfigürasyonu

## Swerve Modülü Fiziksel Özellikleri (`modules/physicalproperties.json`)

Bu JSON, tüm Swerve Modülleriyle paylaşılan fiziksel özellikleri yapılandırır. [`SwerveModulePhysicalCharacteristics`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModulePhysicalCharacteristics.html) oluşturan [`PhysicalPropertiesJson`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/json/PhysicalPropertiesJson.html) ile 1:1 eşlenir.

{% hint style="info" %}
Bir COTS swerve modülü kullanıyorsanız robotunuz için dönüşüm faktörlerini ayarlamak üzere [standard-conversion-factors.md](../standard-conversion-factors.md "mention") sayfasını kullanın!
{% endhint %}

## Alanlar

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th width="115">Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>conversionFactors</code></td><td><a href="physical-properties-configuration.md#conversion-factor-composition">Dönüşüm Faktörü Bileşimi</a></td><td>E</td><td>Dönüşüm faktörü bileşimi. Faktör başlangıçta hesaplanır.</td></tr><tr><td><code>optimalVoltage</code></td><td>Voltaj (Voltage)</td><td>E</td><td>Telafi edilecek ve ileri besleme (feedforward) hesaplamalarını temel alacak optimal voltaj.</td></tr><tr><td><code>currentLimit</code></td><td><a href="physical-properties-configuration.md#motorconfig">MotorConfig</a><br>Daha fazla bilgi <a href="../../fundamentals/swerve-modules.md#current-limiting">burada</a>.</td><td>H</td><td>Motorlara uygulanacak AMPER cinsinden akım sınırı. SparkMAX'ler için stator limiti, TalonFX'ler için besleme (supply) limiti.</td></tr><tr><td><code>rampRate</code></td><td><a href="physical-properties-configuration.md#motorconfig">MotorConfig</a></td><td>H</td><td>Motorun 0'dan tam gaza geçmesi için gereken minimum saniye sayısı.</td></tr><tr><td><code>friction</code></td><td><a href="physical-properties-configuration.md#motorconfig">MotorConfig</a></td><td>H</td><td>Tekerleği veya modülü hareket ettirmek için gereken minimum voltaj. Sürüş motorları için varsayılan <code>0.2</code>, açı motorları için <code>0.3</code>'tür.</td></tr><tr><td><code>robotMass</code></td><td>Lb (Pounds)</td><td>H</td><td>Varsayılan <code>50</code>kgs. (Not: Birimler karışık görünüyor, orijinal metne sadık kalınmıştır)</td></tr><tr><td><code>steerRotationalInertia</code></td><td>KilogramMetersSquare</td><td>H</td><td><code>KilogramMetersSquare</code> cinsinden dönme eylemsizliği. Varsayılan <code>0.03</code>.</td></tr><tr><td><code>wheelGripCoefficientOfFriction</code></td><td>Halı Üzerinde Sürtünme Katsayısı</td><td>H</td><td>Halı üzerindeki kavrama bandı sürtünme katsayısı. Pratik maksimum ivmeyi hesaplamak için kullanılır.</td></tr></tbody></table>

#### MotorConfig

| İsim    | Birimler | Gerekli | Açıklama        |
| ------- | ------ | -------- | ------------------ |
| `drive` | Sayı | E        | Sürüş motoru değeri. |
| `angle` | Sayı | E        | Açı motoru değeri. |

#### Dönüşüm Faktörü Bileşimi

<table><thead><tr><th>İsim</th><th>Birimler</th><th width="62">Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>drive</code></td><td><a href="physical-properties-configuration.md#drive-conversion-factor-composition">Sürüş Bileşimi</a></td><td>E</td><td>Sürüş dönüşüm faktörü bileşimi</td></tr><tr><td><code>angle</code></td><td><a href="physical-properties-configuration.md#angle-conversion-factor-composition">Açı Bileşimi</a></td><td>E</td><td>Açı dönüşüm faktörü bileşimi</td></tr></tbody></table>

#### Sürüş Dönüşüm Faktörü Bileşimi

<table><thead><tr><th width="149">İsim</th><th width="117">Birimler</th><th width="106">Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>diameter</code></td><td>İnç</td><td>E</td><td>Tekerleğin çapı.</td></tr><tr><td><code>gearRatio</code></td><td>Sayı</td><td>E</td><td>Sürüş motorunun tekerleğe dişli oranı.</td></tr><tr><td><code>factor</code></td><td>Sayı</td><td>H</td><td>Önceden hesaplanmış dönüşüm faktörü.</td></tr></tbody></table>

#### Açı Dönüşüm Faktörü Bileşimi

<table><thead><tr><th width="156">İsim</th><th width="123">Birimler</th><th width="87">Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>gearRatio</code></td><td>Sayı</td><td>E</td><td>Açı/dümenleme/azimut motorunun tekerleğe dişli oranı.</td></tr><tr><td><code>factor</code></td><td>Sayı</td><td>H</td><td>Önceden hesaplanmış dönüşüm faktörü.</td></tr></tbody></table>

## Örnek Konfigürasyon Dosyası

<pre class="language-json"><code class="lang-json">{
  <a data-footnote-ref href="#user-content-fn-1">"conversionFactors"</a>: {
	"angle": {"gearRatio": 28.125},
	"drive": {"diameter": 4, "gearRatio": 6.75}
  },
  "currentLimit": {
    "drive": 40,
    "angle": 20
  },
  "rampRate": {
    "drive": 0.25,
    "angle": 0.25
  },
  "wheelGripCoefficientOfFriction": 1.19,
  "optimalVoltage": 12
}
</code></pre>

[^1]: COTS swerve modülleri için [standard-conversion-factors.md](../standard-conversion-factors.md "mention") içinde bulunabilir
