# İlk Konfigürasyonunuzu Oluşturma

## DevilBotz 2876 Swerve Kurulum Kontrol Listesi

[DevilBotz 2876](https://www.thebluealliance.com/team/2876/2024)'nın iltifatlarıyla!

Güncellendi: 2024-02-03

## Yazdırılabilir versiyon

{% file src="../.gitbook/assets/2024-02-03 DevilBotz 2876 Swerve Bring-Up Checklist.pdf" %}

## Kaynaklar

* [YAGSL Wiki](https://yagsl.gitbook.io/yagsl/) - [https://yagsl.gitbook.io/yagsl/](https://yagsl.gitbook.io/yagsl/)
* [REV Robotics Hardware Client](https://docs.revrobotics.com/rev-hardware-client/) - [https://docs.revrobotics.com/rev-hardware-client/](https://docs.revrobotics.com/rev-hardware-client/)
  * _Spark Max Motor Kontrolcülerini ve diğer Rev cihazlarını yapılandırmak için_
* [Phoenix Tuner X](https://pro.docs.ctr-electronics.com/en/stable/docs/hardware-reference/cancoder/index.html) - [https://v6.docs.ctr-electronics.com/en/stable/docs/tuner/index.html](https://v6.docs.ctr-electronics.com/en/stable/docs/tuner/index.html)
  * _CanCoder'ları ve diğer CTR cihazlarını yapılandırmak için_

## Swerve Oryantasyon Şeması

{% hint style="warning" %}
_Not: Üstten bakıldığında, tekerleğin konik dişlili taraflarının **sola** baktığından emin olun._
{% endhint %}

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption></figcaption></figure>

### Adım 1: Modül Tipleri

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td></td><td><strong>Model, Versiyon, Vb.</strong></td></tr><tr><td><em>Motor</em></td><td></td></tr><tr><td><em>Kontrolcü</em></td><td></td></tr><tr><td><em>Mutlak Enkoder</em></td><td></td></tr><tr><td><em>IMU</em></td><td></td></tr></tbody></table>

### Adım 2: Yapıya Özgü Ayrıntılar

1. Modül merkezini **robot merkezine** göre ölçün

<table data-full-width="true"><thead><tr><th>Modül</th><th>X "Ön" (İnç)</th><th>Y "Sol" (İnç)</th></tr></thead><tbody><tr><td><em>Ön Sol (FL)</em></td><td>+</td><td>+</td></tr><tr><td><em>Ön Sağ (FR)</em></td><td>+</td><td>-</td></tr><tr><td><em>Arka Sol (BL)</em></td><td>-</td><td>+</td></tr><tr><td><em>Arka Sağ (BR)</em></td><td>-</td><td>-</td></tr></tbody></table>

2. Tekerlek çapını _inç cinsinden_ ölçün
3. [_Raporlanan_ dahili enkoder çözünürlüğünü belirleyin](#user-content-fn-1)[^1]
   * _Not: Çoğu enkoder artık raporlanan değerleri `-1` ile `1` arasında normalleştirir, bu nedenle dönüşüm faktörlerini hesaplarken Enkoder Çözünürlüğü genellikle “`1`” olmalıdır. Bilinen tek istisna TalonSRX'tir._
4. Swerve modülü üreticisinin özelliklerinden sürüş/açı dişli oranını bulun
5. (İsteğe bağlı) [sürüş/açı dönüşüm faktörlerini](#user-content-fn-2)[^2] hesaplayın
   * Sürüş Motoru Dönüşüm Faktörü (metre/dönüş) = (PI \* METRE CİNSİNDEN TEKERLEK ÇAPI) / (DİŞLİ ORANI \* ENKODER ÇÖZÜNÜRLÜĞÜ)
   * Açı Motoru Dönüşüm Faktörü (derece/dönüş) = 360 / (DİŞLİ ORANI \* ENKODER ÇÖZÜNÜRLÜĞÜ)

<table data-full-width="true"><thead><tr><th>Motor</th><th align="center">Tekerlek Çapı (metre)</th><th>Dişli Oranı</th><th align="center">Enkoder Çözünürlüğü (CPR)</th><th>Dönüşüm Faktörü</th></tr></thead><tbody><tr><td><em>Sürüş</em></td><td align="center"></td><td></td><td align="center">1</td><td></td></tr><tr><td><em>Açı</em></td><td align="center"><strong>N/A</strong></td><td></td><td align="center">1</td><td></td></tr></tbody></table>

### Adım 3: Elektriksel Özellikler

6. Her modül için CAN ID'lerini Ayarlayın/Doğrulayın

{% hint style="warning" %}
_Not: Her modül için FW'yi güncelleyin ve saklanan ayarları fabrika varsayılanlarına sıfırlayın_
{% endhint %}

<table data-full-width="true"><thead><tr><th>Modül</th><th>Motor CAN ID'leri</th><th>Motor CAN ID'leri</th><th>Enkoder CAN/Kanal ID'si</th></tr></thead><tbody><tr><td></td><td><strong>Sürüş</strong></td><td><strong>Açı</strong></td><td><strong>Mutlak Enkoder</strong></td></tr><tr><td><em>Ön Sol (FL)</em></td><td></td><td></td><td></td></tr><tr><td><em>Ön Sağ (FR)</em></td><td></td><td></td><td></td></tr><tr><td><em>Arka Sol (BL)</em></td><td></td><td></td><td></td></tr><tr><td><em>Arka Sağ (BR)</em></td><td></td><td></td><td></td></tr></tbody></table>

7. Ters Çevirmeyi (Inversion) Kontrol Edin
   1. _Sürüş_ tekerleğini **SAAT YÖNÜNÜN TERSİNE (CCW)** döndürün ("ileri" hareket ederek)
      * Yerleşik enkoder değeri **artmalıdır**. Değilse, sürüş motorunu _ters çevirin_.
   2. _Açı_ tekerleğini **SAAT YÖNÜNÜN TERSİNE (CCW)** döndürün (üstten bakıldığında)
      * Yerleşik enkoder değeri **artmalıdır**. Değilse, açı motorunu _ters çevirin_.
      * Mutlak enkoder değeri **artmalıdır**. Değilse, mutlak enkoderi _ters çevirin_.
   3. Tüm _robotu_ **SAAT YÖNÜNÜN TERSİNE (CCW)** döndürün. Jiro açısı (yaw) **artmalıdır**. Değilse, IMU'yu _ters çevirin_

{% hint style="warning" %}
_Not: Motor kontrolcülerine ve/veya mutlak enkoderlere erişmek için donanım yardımcı programlarını kullanıyorsanız, RoboRio CAN veri yolunda aktif **olmamalıdır**. RoboRio'yu devre dışı bırakmanın en güvenilir yolu, **CAN BUS sonlandırmasını etkilemeden**, RoboRio'yu besleyen Güç Dağıtım Paneli'ndeki (PDP) 10A sigortasını çekerek gücünü geçici olarak kesmek ve **ardından** robotu güç döngüsüne sokmaktır._
{% endhint %}

<table data-full-width="true"><thead><tr><th>Modül</th><th>Ters Çevrilmiş mi?</th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><strong>Sürüş</strong></td><td><strong>Açı</strong></td><td><strong>Mutlak Enkoder</strong></td><td><strong>IMU</strong></td></tr><tr><td><em>Ön Sol (FL)</em></td><td></td><td></td><td></td><td></td></tr><tr><td><em>Ön Sağ (FR)</em></td><td></td><td></td><td></td><td></td></tr><tr><td><em>Arka Sol (BL)</em></td><td></td><td></td><td></td><td></td></tr><tr><td><em>Arka Sağ (BR)</em></td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Adım 4: Mutlak Enkoder Ofsetleri

8. Robotu Açın (Devre Dışı (Disabled), böylece tekerlekler manuel olarak döndürülebilir)
9. 4 tekerleğin hepsini manuel olarak döndürün, böylece hepsi ileriye bakacak ve ileri dönüş, artan sürüş enkoder değerleri ile sonuçlanacaktır ([Oryantasyon Şeması](creating-your-first-configuration.md#swerve-orientation-diagram-1)ndaki siyah oklara bakın).
10. Her modül için mutlak enkoder değerini ölçün

<table data-full-width="true"><thead><tr><th>Modül</th><th>Açı Mutlak Ofseti (derece)</th><th></th></tr></thead><tbody><tr><td><em>Ön Sol (FL)</em></td><td></td><td></td></tr><tr><td><em>Ön Sağ (FR)</em></td><td></td><td></td></tr><tr><td><em>Arka Sol (BL)</em></td><td></td><td></td></tr><tr><td><em>Arka Sağ (BR)</em></td><td></td><td></td></tr></tbody></table>

### Adım 5: Verileri konfigürasyon web sayfasına girin

Web sayfasını açın ve verilerinizi konfigürasyon dosyalarına aktarın.\
[https://yet-another-software-suite.github.io/YAGSL/config\_generator/](https://yet-another-software-suite.github.io/YAGSL/config_generator/)

{% content-ref url="broken-reference/" %}
[broken-reference](broken-reference/)
{% endcontent-ref %}

[^1]: EĞER bir SparkMAX veya TalonFX kullanıyorsanız bu `1` olacaktır!

[^2]: Bunlar motor kontrolcüsü için dönüşleri metre/dereceye çevirir.
