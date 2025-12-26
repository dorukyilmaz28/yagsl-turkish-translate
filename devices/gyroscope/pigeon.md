# Pigeon

Bu, CTRE Pigeon'un üretimi durdurulan ve yalnızca Phoenix 5 aracılığıyla desteklenen ilk yinelemesini ifade eder.

## Phoenix Tuner

Bu cihazla iletişim kurmak ve güncellemek için Phoenix tuner'ı kurmanız gerekir.

{% embed url="https://store.ctr-electronics.com/software/" %}
Phoenix Tuner, "Phoenix Framework for HERO C#" altında mevcuttur
{% endembed %}

## Dokümantasyon

Pigeon yalnızca Phoenix 5'te mevcuttur, bu nedenle dokümantasyon aşağıdadır. Kısmen bu cihaz nedeniyle YAGSL'ye Phoenix 5 kütüphanelerini dahil etmelisiniz.

{% embed url="https://v5.docs.ctr-electronics.com/en/stable/ch11_BringUpPigeon.html" %}
Pigeon programlama ve yapılandırma rehberi
{% endembed %}

## YAGSL Kontrol Listesi

* [ ] Benzersiz bir CAN ID ayarlayın.
* [ ] Mevcut en son ürün yazılımına güncelleyin.

## İletişim

CAN ID'yi ayarladıktan sonra, JSON konfigürasyonunun `id` kısmını `pigeon` için CAN ID'ye ayarlarsınız. Bu cihaz CANivore'larla uyumlu değildir, bu nedenle `canbus` seçeneği geçerli değildir ve `""` veya `"rio"` veya `null` olmalıdır.

## Örnek `swervedrive.json`

<pre class="language-json"><code class="lang-json">{
  "imu": {
    "type": "<a data-footnote-ref href="#user-content-fn-1">pigeon</a>",
    "id": <a data-footnote-ref href="#user-content-fn-2">13</a>,
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

[^1]: Pigeon cihazı

[^2]: CAN ID 13

[^3]: Uygulanamaz bu nedenle `null` seçilen tercihtir.
