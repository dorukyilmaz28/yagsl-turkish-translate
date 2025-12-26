---
description: NavX 2'yi kalibre etme
---

# NavX

NavX2, Studica'nın (resmi olarak KauiLabs tarafından) NavX serisinin en son yinelemesidir ve nasıl kalibre edileceği ve jiroskopunuzdan en iyi şekilde nasıl yararlanılacağı konusunda mükemmel okumalar ve dokümantasyon sunar.

{% embed url="https://www.studica.ca/en/navx-2-mxp-robotics-navigation-sensor" %}

## Başlarken

Artık bir NavX'iniz var, tebrikler! Şimdi yapılandırma ve kalibre etme zamanı, bu adımları izlemezseniz mümkün olduğu kadar iyi çalışmayacaktır.

NavX için java sınıfı `import com.kauailabs.navx.frc.AHRS;` adresinden içe aktarılan `AHRS`dir.

## NavX Omni-Mount

NavX, sapmayı (yaw) herhangi bir konuma yeniden yapılandırabilir! İşte nasıl yapılacağına dair rehberleri.

{% embed url="https://pdocs.kauailabs.com/navx-mxp/installation/omnimount/" %}

## NavXUI Kurulumu

Java 1.7 veya üstü gereklidir

{% embed url="https://pdocs.kauailabs.com/navx-mxp/software/navx-mxp-ui/" %}

{% embed url="https://www.kauailabs.com/public_files/navx-mxp/navx-mxp.zip" %}
Kurulum ZIP'i
{% endembed %}

Robotta optimum doğruluğu sağlamak amacıyla gelişmiş kalibrasyon için kullanışlıdır.

## Kalibrasyon

Kalibrasyon için tam dokümantasyon buradadır. Orijinal kalibrasyon Hawaii'deki fabrikada yapılır, bu nedenle en az bir kez yapmanız şiddetle tavsiye edilir!

{% embed url="https://pdocs.kauailabs.com/navx-mxp/guidance/gyroaccelcalibration/" %}

Burada kısa bir özet sunacağız.

Jiroskoplar ortam sıcaklığına duyarlıdır, bu nedenle bunları teslim aldığınızda **VE** etkinliklerde yeniden kalibre etmeniz zorunludur. NavX talimatları aşağıdaki gibidir.

1. NavX'i dünya yüzeyine paralel sabit bir platforma yerleştirin (bir su terazisi kullanın!).
2. **CAL** düğmesine en az 10 saniye basılı tutun.
3. **CAL** düğmesini bıraktığınızda **CAL** ledinin kısaca yanıp söndüğünden emin olun.
4. **RESET** düğmesine basın.
5. 15 saniyeye kadar bekleyin.
6. Bir sonraki Anında (On-the-fly) Cayro kalibrasyonu tamamlanana kadar sapma (yaw) doğruluğu azalabilir. (bu, ilk otonomunuzun doğru hareket etmeyebileceği anlamına gelir!)

## YAGSL Kontrol Listesi

* [ ] Mevcut en son ürün yazılımına (firmware) güncelleyin.
* [ ] NavX'i dünyaya paralel olarak hizalayın.
* [ ] NavX'i kalibre edin.
* [ ] Kullanmak istediğiniz bağlantı/iletişim yöntemini seçin.

## Bağlantı Yöntemleri

### SPI (`navx`, `navx_spi`)

YAGSL, roboRIO MXP üzerinden NavX SPI iletişimini destekler. Bu, NavX cihazlarıyla iletişim kurmak için önerilen yöntemdir.

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-1">"navx_spi"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-2">0</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-3">null</a>
  },
  "invertedIMU": true,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-4">"navx"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-5">0</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-6">null</a>
  },
  "invertedIMU": true,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

### Seri (`navx_mxp_serial`, `navx_usb`)

Seri iletişim, SPI iletişiminden daha yavaştır ve parazite daha açık olabilir, ancak bu [NavX2 micro](https://www.andymark.com/products/navx2-micro-navigation-sensor) (`navx_usb`) ile iletişim kurmanın kutudan çıkan tek yoludur, bu nedenle bir tane kullanıyorsanız bu seçilmelidir. SPI MXP iletişiminin şu anda çalışmadığı durumlarda MXP seri iletişimi kullanılabilir.

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-7">"navx_mxp_serial"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-8">0</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-9">null</a>
  },
  "invertedIMU": true,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-10">"navx_usb"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-11">0</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-12">null</a>
  },
  "invertedIMU": true,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

### I2C (`navx_i2c`)

MXP üzerinde I2C iletişimi desteklenir ancak bunun rastgele roboRIO üzerinde kalıcı kilitlenmelere neden olduğu bilinmektedir, bu sorun kapsamlı bir şekilde araştırılmış ve bilinen bir neden bulunamamıştır. Bu seçeneği kullanmaktan ne pahasına olursa olsun kaçınılması teşvik edilir!!

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-13">"navx_i2c"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-14">0</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-15">null</a>
  },
  "invertedIMU": true,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

## NavX Micro

<figure><img src="../../.gitbook/assets/navx2_micro.png" alt=""><figcaption><p>Andymark'tan NavX micro</p></figcaption></figure>

NavX micro kullanıyorsanız, USB üzerinden seri iletişim kurduğunuzu belirtmek için lütfen `navx_usb` türünü seçin, aksi takdirde jiroskop YAGSL ile çalışmayacaktır!

[^1]: MXP üzerinde SPI üzerinden NavX seçili.

[^2]: Uygulanamaz, herhangi bir şey olabilir `0` keyfi olarak seçilmiştir.

[^3]: Uygulanamaz, bu nedenle `null` seçilmiştir.

[^4]: Arka planda `navx_spi` olarak varsayılan ayarlanır.

[^5]: ID, NavX için alakalı değildir, bu nedenle keyfi olarak `0` seçilmiştir.

[^6]: `canbus` NavX için alakalı değildir, bu nedenle `null` konfigürasyonda hiçbir şeyin ayarlanmamasını sağlar.

[^7]: MXP seri portları üzerinden NavX seri iletişimi.

[^8]: ID, NavX için alakalı değildir, bu nedenle keyfi olarak `0` seçilmiştir.

[^9]: `canbus` NavX için alakalı değildir, bu nedenle `null` konfigürasyonda hiçbir şeyin ayarlanmamasını sağlar.

[^10]: USB portu üzerinden NavX seri iletişimi, bu NavX2 micro ile iletişim kurmanın en kolay yoludur.

[^11]: ID, NavX için alakalı değildir, bu nedenle keyfi olarak `0` seçilmiştir.

[^12]: `canbus` NavX için alakalı değildir, bu nedenle `null` konfigürasyonda hiçbir şeyin ayarlanmamasını sağlar.

[^13]: MXP'nin I2C portu üzerinden bağlanan NavX. Bu tehlikelidir ve bunun yerine diğerlerinden biri seçilmelidir!

[^14]: ID, NavX için alakalı değildir, bu nedenle keyfi olarak `0` seçilmiştir.

[^15]: `canbus` NavX için alakalı değildir, bu nedenle `null` konfigürasyonda hiçbir şeyin ayarlanmamasını sağlar.
