# ADXRS450

{% hint style="warning" %}
ADXRS450 ±300°/san sınırına sahiptir ve sınırların ötesinde dönüş verisi sağlamayı durduracaktır.\
Bu jiroskopun yarışmalarda kullanılması önerilmez.
{% endhint %}

{% hint style="warning" %}
Bu jiroskop ile HER ZAMAN başlangıçta robotunuzu sabit tutun.
{% endhint %}

## Dokümantasyon

{% embed url="https://wiki.analog.com/first/adxrs450_gyro_board_frc" %}
Resmi dokümantasyon
{% endembed %}

{% embed url="https://docs.wpilib.org/en/stable/docs/software/hardware-apis/sensors/gyros-software.html#adxrs450-gyro" %}
Nasıl başlatılacağına dair WPILib Dokümantasyonu
{% endembed %}

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p>Tek eksenli okuma.</p></figcaption></figure>

ADXRS450 eski bir tek eksenli jiroskoptur, yani çalışması için dünyaya paralel olması gerekir!

## YAGSL Kontrol Listesi

* [ ] ADXRS450'nin roboRIO'ya sıkıca takıldığından emin olun.
* [ ] roboRIO robotun üzerinde ortalanmıştır.
* [ ] roboRIO dünyaya düz paraleldir.
* [ ] Robot başlangıçta en az 10 saniye boyunca HİÇ HAREKET ETMEZ!

## İletişim

ADXRS450 doğrudan roboRIO üzerindeki SPI portuna bağlanır ve YAGSL ile yalnızca buradan bağlanabilir.

## Örnek `swervedrive.json`

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": <a data-footnote-ref href="#user-content-fn-1">"adxrs450"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-2">0</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-3">null</a>
  },
  "invertedIMU": <a data-footnote-ref href="#user-content-fn-4">false</a>,
  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

[^1]: Birincil jiroskop olarak `adxrs450` jiroskopunu seçin.

[^2]: ID, NavX için alakalı değildir, bu nedenle keyfi olarak `0` seçilmiştir.

[^3]: `canbus` NavX için alakalı değildir, bu nedenle `null` konfigürasyonda hiçbir şeyin ayarlanmamasını sağlar.

[^4]: Varsayılan olarak saat yönünün tersine okur
