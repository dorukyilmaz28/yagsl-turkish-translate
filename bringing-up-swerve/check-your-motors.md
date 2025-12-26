# Motorlarınızı Kontrol Edin

{% hint style="danger" %}
CAN ID'lerinizin benzersiz olduğundan emin olun! REV Güç Dağıtım Hub'ınızın CAN ID'sinin SparkMAX'in CAN ID'si ile aynı olması durumunda **SparkMAX'in motoru hareket ettirmemesine neden olacak** bilinen bir sorun var!
{% endhint %}

## Her bileşeni ID'leriyle Fiziksel Olarak Etiketleyin

Bir swerve sürüşü (veya başka herhangi bir sürüş sistemi) yapılandırmasını mahvetmenin, sürüş motoru, açı motoru, mutlak enkoder veya jiroskop olsun, bir bileşen için yanlış kanal numarasını, CAN ID'sini ve hatta CAN veri yolunu (cihazınız bir CANivore üzerindeyse) koymaktan daha kolay bir yolu yoktur. Bazı bileşenlerin NavX'ler gibi ID'leri yoktur ve bunun yerine bağlantı yöntemini tanımlayan birkaç farklı `tür`e (`navx_spi`, `navx_usb`, `navx_i2c`) sahiptirler, bunların önceden bilinmesi gerekir.

Robotunuzu yapılandırmaya başlamadan önce [robotunuzu tanıma](../configuring-yagsl/getting-to-know-your-robot/ "mention") sayfasındaki bilgileri bulmanızı şiddetle tavsiye ederim.

## Motorlar saat yönünün tersine pozitif dönmelidir

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption><p>Sol ve sağ, fiziksel sol ve sağdır.</p></figcaption></figure>

Robot devre dışıyken motorunuzu döndürdüğünüzde `swerve/modules/.../Raw Angle Encoder` (açı/dümenleme/azimut bağıl enkoderi) ve `swerve/modules/.../Raw Absolute Encoder` (mutlak enkoder) fark edeceksiniz. Bunların her ikisi de motor saat yönünün tersine döndürüldüğünde artmalıdır. Daha fazla bilgi için buraya bakın.

{% content-ref url="../configuring-yagsl/when-to-invert.md" %}
[when-to-invert.md](../configuring-yagsl/when-to-invert.md)
{% endcontent-ref %}

## Dönüşüm Faktörleri ve motorlarınız

Dönüşüm faktörleri, motorunuzun yerel birimlerden (genellikle _**dönüşler**_) dümenleme/azimut/açı motorları için dereceye ve sürüş motorları için metreye dönüştürmek üzere uygulanır. Dönüşüm faktörleri, motor kontrolcünüze bağlı bir mutlak enkoder olması durumu haricinde, yalnızca motor kontrolcüleri için geçerlidir.

## Mutlak Enkoder ofseti

{% hint style="warning" %}
Buradaki tüm örnekler sürücü paneli olarak Shuffleboard'u kullanır ancak [Advantage Scope](https://docs.advantagescope.org/) veya [Elastic](https://github.com/Gold872/elastic-dashboard) gibi başka herhangi bir alternatif de kullanılabilir.
{% endhint %}

Mutlak enkoder ofseti, swerve modülünüzün güç kesintileri arasında tekerlek yönünü korumasını sağlayan şeydir. Çalışan bir swerve sürüşü için hayati önem taşır.

1. Tüm tekerlekleri, konik dişliler (bevels) bu şekilde sola bakacak şekilde hizalayın.

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption></figcaption></figure>

2. Kodunuzu dağıtın (deploy).
3. **ROBOTUNUZU ETKİNLEŞTİRMEYİN! (DO NOT ENABLE)**
4. Sürücü panelinizi açın.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

6.

<figure><img src="../.gitbook/assets/ShuffleboardAbsoluteEncoderHighlight.png" alt=""><figcaption></figcaption></figure>

7. `swerve/modules/.../Raw Absolute Encoder` değerlerini not edin ve bunları modül JSON'larında `absoluteEncoderOffset` için kullanın.

{% hint style="warning" %}
**MAXSwerve takımlarına özel not!**

MAXSwerveModules kullanarak hizaladığınızda ve her modül için `absoluteEncoderOffset` değerini bulduğunuzda, modül konumunu düzeltmek için **`absoluteEncoderOffset` değerinden +/-`90`** yapmanız gerekebilir. `absoluteEncoderInverted` da her modül konfigürasyonunda `true` olmalıdır.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": "sparkmax",
    "id": 12,
    "canbus": null
  },
  "angle": {
    "type": "sparkmax",
    "id": 11,
    "canbus": null
  },
  "encoder": {
    "type": "attached",
    "id": 0,
    "canbus": null
  },
  "inverted": {
    "drive": false,
    "angle": false
  },
  "absoluteEncoderInverted": true,
  "absoluteEncoderOffset": -90,
  "location": {
    "front": 12,
    "left": -12
  }
}
</code></pre>
{% endhint %}
