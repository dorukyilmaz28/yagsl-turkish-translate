# Motorlarınızı Kontrol Edin

{% hint style="danger" %}
CAN ID'lerinizin benzersiz olduğundan emin olun! REV Güç Dağıtım Hub'ınızın CAN ID'sinin SparkMAX'in CAN ID'si ile aynı olması durumunda **SparkMAX'in motoru hareket ettirmemesine neden olacak** bilinen bir sorun var!
{% endhint %}

## Her bileşeni ID'leriyle Fiziksel Olarak Etiketleyin

Bir swerve sürüşünü (ya da herhangi bir sürüş sistemini) yapılandırırken yapılabilecek en kolay ve en kritik hatalardan biri; bir bileşen için yanlış kanal numarası, yanlış CAN ID ya da yanlış CAN hattı (örneğin cihaz CANivore üzerindeyse) tanımlamaktır. Bu durum; sürüş motoru, açı/azimuth motoru, mutlak enkoder veya jiroskop için geçerlidir.

Bazı bileşenlerin ise klasik anlamda bir ID’si yoktur. Örneğin NavX sensörleri, bağlantı yöntemine göre farklı türlerde tanımlanır (`navx_spi, navx_usb, navx_i2c`). Bu türlerin hangisinin kullanıldığının yapılandırmaya başlamadan önce bilinmesi gerekir.

Robotunuzu yapılandırmaya başlamadan önce [getting-to-know-your-robot](../configuring-yagsl/getting-to-know-your-robot/ "mention") sayfasındaki bilgileri bulmanızı şiddetle tavsiye ederim.

## Motorlar saat yönünün tersine pozitif dönmelidir

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption><p>Sol ve sağ, fiziksel sol ve sağdır.</p></figcaption></figure>

Robot devre dışıyken motorunuzu döndürdüğünüzde `swerve/modules/.../Raw Angle Encoder` (açı/dümenleme/azimut bağıl enkoderi) ve `swerve/modules/.../Raw Absolute Encoder` (mutlak enkoder) fark edeceksiniz. Bunların her ikisi de motor saat yönünün tersine döndürüldüğünde artmalıdır. Daha fazla bilgi için buraya bakın.

{% content-ref url="../configuring-yagsl/when-to-invert.md" %}
[when-to-invert.md](../configuring-yagsl/when-to-invert.md)
{% endcontent-ref %}

## Dönüşüm Faktörleri ve motorlarınız

Dönüşüm katsayıları (conversion factors), motorların yerel (native) birimlerini — genellikle dönüş (rotation) — daha anlamlı fiziksel birimlere çevirmek için kullanılır. Açı/azimuth/steering motorları için bu birim derece, sürüş motorları için ise metredir.

Dönüşüm katsayıları normalde yalnızca motor sürücüleri için geçerlidir. Ancak motor sürücüsüne bağlı bir mutlak (absolute) enkoder varsa, bu durumda dönüşüm katsayıları enkoder ölçümleri için de dikkate alınmalıdır.

## Mutlak Enkoder ofseti

{% hint style="warning" %}
Buradaki tüm örnekler sürücü paneli olarak Shuffleboard'u kullanır ancak [Advantage Scope](https://docs.advantagescope.org/) veya [Elastic](https://github.com/Gold872/elastic-dashboard) gibi başka herhangi bir alternatif de kullanılabilir.
{% endhint %}

Mutlak enkoder ofseti, swerve modülünüzün güç kesintileri arasında tekerlek yönünü korumasını sağlayan şeydir. Çalışan bir swerve sürüşü için hayati önem taşır.

1. Tüm tekerlekleri, konik dişliler (bevels) bu şekilde sola bakacak şekilde hizalayın.

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption></figcaption></figure>

2. Kodunuzu deploy edin.
3. **ROBOTUNUZU ETKİNLEŞTİRMEYİN! (DO NOT ENABLE)**
4. Sürücü panelinizi açın.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

6.

<figure><img src="../.gitbook/assets/ShuffleboardAbsoluteEncoderHighlight.png" alt=""><figcaption></figcaption></figure>

7. `swerve/modules/.../Raw Absolute Encoder` değerlerini not edin ve bunları modül JSON'larında `absoluteEncoderOffset` için kullanın.

{% hint style="warning" %}
**MAXSwerve takımlarına özel not!**

MAXSwerveModules kullanarak hizaladığınızda ve her modül için `absoluteEncoderOffset` değerini bulduğunuzda, modül konumunu düzeltmek için **`absoluteEncoderOffset` değerinden +/-`90`** yapmanız gerekebilir. `absoluteEncoderInverted` da her modül konfigürasyonunda `true` olmalıdır.

```json
{
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
```
{% endhint %}
