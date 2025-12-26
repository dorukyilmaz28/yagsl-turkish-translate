# TalonFX

## Başlarken

TalonFX, Kraken X60 ve Falcon 500'leri kontrol etmek için kullanılan motor kontrolcüsüdür.

{% embed url="https://wcproducts.com/products/kraken" %}

{% hint style="warning" %}
Falcon 500 v2 kullanıyorsanız (bunlar fiilen üretimden kalkmıştır), burada açıklanan loctite düzeltmesini uyguladığınızdan emin olun!\
[https://content.vexrobotics.com/vexpro/Falcon/217-6515-753-Falcon500-V2-Upgrade.pdf](https://content.vexrobotics.com/vexpro/Falcon/217-6515-753-Falcon500-V2-Upgrade.pdf)
{% endhint %}

REV NEO'lardan daha güçlü ve verimli olabildikleri için genellikle sürüş motorları olarak kullanılırlar.

```java
import com.ctre.phoenix6.hardware.TalonFX;
import com.ctre.phoenix6.controls.DutyCycleOut;

TalonFX motor = new TalonFX(10);
motor.setControl(new DutyCycleOut(1.0)); // 100% full speed positive.
```

## Dokümantasyon

Bu cihaz CTRE Tuner X ile yükseltilebilir.

{% embed url="https://v6.docs.ctr-electronics.com/en/latest/docs/tuner/index.html" %}
Tuner X kurulumu ve dokümantasyonu
{% endembed %}

{% embed url="https://pro.docs.ctr-electronics.com/en/stable/docs/hardware-reference/talonfx/index.html" %}
Resmi Dokümantasyon kaynağı
{% endembed %}

Herhangi bir zamanda hata ayıklamanıza yardımcı olması için LED durum koduna çok dikkat edin. Talon FX için Tuner X'te değiştirilen tüm ayarların YAGSL başlatıldığında üzerine yazıldığını unutmayın.

## YAGSL Kontrol Listesi

* [ ] Tüm TalonFX'leri benzersiz CAN ID'lerine ayarlayın.
* [ ] Tüm TalonFX'leri en son ürün yazılımına güncelleyin.
* [ ] TalonFX motoru saat yönünün tersine pozitif döndürür. (Saat yönünün tersine pozitif dönmüyorsa TalonFX'i programatik olarak ters çevirin).
* [ ] Bir sürüş motoru için PID değerlerini ayarlayın.
* [ ] Bir dümenleme/azimut/açı motoru için PID değerlerini ayarlayın.

## Modül örnek konfigürasyonu

Aşağıdaki örnek, bir modül konfigürasyon dosyası içindir, örneğin `frontleft.json`, `frontright.json`, `backleft.json` ve `backright.json`.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": <a data-footnote-ref href="#user-content-fn-1">"talonfx"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-2">5</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-3">null</a>
  },
  "angle": {
    "type": <a data-footnote-ref href="#user-content-fn-4">"talonfx"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-5">6</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-6">null</a>
  },
  "encoder": {
    "type": "cancoder",
    "id": 11,
    "canbus": null
  },
  "inverted": {
    "drive": <a data-footnote-ref href="#user-content-fn-7">false</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-8">false</a>
  },
  "absoluteEncoderOffset": -18.281,
  "location": {
    "front": -12,
    "left": -12
  }
}
</code></pre>

## Örnek `pidfproperties.json`

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "p": <a data-footnote-ref href="#user-content-fn-9">0.0020645</a>,
    "i": <a data-footnote-ref href="#user-content-fn-10">0</a>,
    "d": <a data-footnote-ref href="#user-content-fn-11">0</a>,
    "f": <a data-footnote-ref href="#user-content-fn-12">0</a>,
    "iz": 0
  },
  "angle": {
    "p": <a data-footnote-ref href="#user-content-fn-13">0.01</a>,
    "i": <a data-footnote-ref href="#user-content-fn-14">0</a>,
    "d": <a data-footnote-ref href="#user-content-fn-15">0</a>,
    "f": <a data-footnote-ref href="#user-content-fn-16">0</a>,
    "iz": 0
  }
}
</code></pre>

## Örnek `physicalproperties.json`

<pre class="language-json"><code class="lang-json">{
  "conversionFactor": {
    "drive": <a data-footnote-ref href="#user-content-fn-17">0.047286787200699704</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-18">16.8</a>
  },
  "currentLimit": {
    "drive": <a data-footnote-ref href="#user-content-fn-19">40</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-20">20</a>
  },
  "rampRate": {
    "drive": <a data-footnote-ref href="#user-content-fn-21">0.25</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-22">0.25</a>
  },
  "wheelGripCoefficientOfFriction": 1.19,
  "optimalVoltage": 12
}
</code></pre>

[^1]: TalonFX seçili

[^2]: Bu sürüş motor kontrolcüsü TalonFX için CAN ID 'si `5`

[^3]: TalonFX'ler CANivore'larla uyumludur ve kullanılırsa CAN veri yolu kullanımını azaltabilir; TalonFX CANivore'un CAN döngüsündeyse bunu CANivore'un adına ayarlayın.

[^4]: TalonFX seçili

[^5]: Bu sürüş motor kontrolcüsü TalonFX için CAN ID 'si `6`

[^6]: TalonFX'ler CANivore'larla uyumludur ve kullanılırsa CAN veri yolu kullanımını azaltabilir; TalonFX CANivore'un CAN döngüsündeyse bunu CANivore'un adına ayarlayın.

[^7]: Sürüş motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^8]: Dümenleme/azimut/açı motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^9]: Bu, TalonFX üzerinde istenen hızı metre/saniye olarak korumak için kullanılan kP'dir.

[^10]: kI genellikle ayarlanması gerekmez.

[^11]: kD, bunu sönümlemek ve minimum aşma ile hıza daha hızlı ulaşmak için yararlı olacaktır.

[^12]: Bu, tekerleğin dönmesi için voltajın yüzdesi olarak statik ileri beslemedir (feedforward).

[^13]: Bu, TalonFX üzerinde istenen açıyı derece olarak korumak için kullanılan kP'dir.

[^14]: kI genellikle ayarlanması gerekmez.

[^15]: kD, bunu sönümlemek ve minimum aşma ile hıza daha hızlı ulaşmak için yararlı olacaktır.

[^16]: Bu, tekerleğin dönmesi için voltajın yüzdesi olarak statik ileri beslemedir (feedforward).

[^17]: Tümü Kraken olan bir MK4i L2 için devir/dakika'dan metre/saniye'ye geçiş için dönüşüm faktörü.

[^18]: Tümü Kraken olan bir MK4i L2 için devirlerden dereceye geçiş için dönüşüm faktörü.

[^19]: Sürüş motorunun çekebileceği maksimum akım `40`Amperdir.

[^20]: Sürüş motorunun çekebileceği maksimum akım `20`Amperdir.

[^21]: TalonFX'in voltaj düşüşlerini (brownouts) önlemek için kullanılan maksimum rampa oranı.

[^22]: TalonFX'in voltaj düşüşlerini (brownouts) önlemek için kullanılan maksimum rampa oranı.
