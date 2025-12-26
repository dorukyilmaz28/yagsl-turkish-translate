# Pigeon 2.0

Pigeon 2.0, CTRE tarafından geliştirilen Pigeon IMU'nun bir sonraki yinelemesidir. Bu cihaz CANivore ile uyumludur.

{% embed url="https://store.ctr-electronics.com/pigeon-2/" %}

## Tuner X

Bu cihaz CTRE Tuner X ile yükseltilebilir.

{% embed url="https://v6.docs.ctr-electronics.com/en/latest/docs/tuner/index.html" %}

## Dokümantasyon

{% embed url="https://pro.docs.ctr-electronics.com/en/latest/docs/hardware-reference/pigeon2/index.html" %}

{% embed url="https://v6.docs.ctr-electronics.com/en/latest/docs/tuner/pigeon-cal.html" %}

Herhangi bir zamanda hata ayıklamanıza yardımcı olması için LED durum koduna çok dikkat edin. Pigeon 2.0 için Tuner X'te değiştirilen tüm ayarların YAGSL başlatıldığında üzerine yazıldığını unutmayın.

## YAGSL Kontrol Listesi

* [ ] Sapma (Yaw), Saat Yönünün Tersi Pozitif olarak artar.
* [ ] Pigeon 2.0 mümkün olduğunca ortalanmıştır.
* [ ] Pigeon 2.0 en son ürün yazılımına güncellenmiştir.
* [ ] Pigeon 2.0 benzersiz bir CAN ID'sine güncellenmiştir.
* [ ] Robota yerleştirildiğinde Pigeon 2.0'ı kalibre edin.

## İletişim

Bu cihaz roboRIO ile CAN veriyolu üzerinden iletişim kurar ve [CANivore](https://store.ctr-electronics.com/canivore/) ile eşleştirilebilir, böylece roboRIO'nun CAN veriyolu üzerinde bant genişliği kaplamaz. Bunu yapmak için [CANivore](https://pro.docs.ctr-electronics.com/en/latest/docs/canivore/canivore-setup.html) için bir isim belirlemeniz ve bunu YAGSL'de `canbus` adı olarak kullanmanız gerekir.

{% embed url="https://pro.docs.ctr-electronics.com/en/latest/docs/canivore/canivore-setup.html" %}

## Örnek `swervedrive.json`

Aşağıdaki, Pigeon 2.0'ı kuran bir `swervedrive.json` örneğidir. Pigeon 2.0'ın CANivore ile uyumlu olduğunu, bu nedenle `canbus` parametresinin aslında çalıştığını unutmayın!

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-1">"pigeon2"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-2">13</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-3">"canivore"</a>
  },
  "invertedIMU": <a data-footnote-ref href="#user-content-fn-4">true</a>,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>



[^1]: Pigeon 2.0 IMU seçildi

[^2]: Pigeon'un CAN ID'si 13'tür.

[^3]: Pigeon 2.0, "`canivore`" adında roboRIO'ya bağlı bir CANivore üzerindedir.

[^4]: Pigeon ters çevrilmiştir.
