# SparkMAX

Bu sayfa, **FIRÇASIZ BİR MOTORA (REV NEO'lar)** bağlıyken REV SparkMAX'i ifade eder, REV SparkMAX'in fırçalı modda kullanımını tartışmak için daha sonra başka dokümantasyon eklenecektir.

{% embed url="https://www.revrobotics.com/rev-11-2158/" %}
REV SparkMAX ürün bağlantısı
{% endembed %}

## Başlarken

[`CANSparkMax`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkmax) nesnesi oluşturmak için küçük bir örnek program aşağıdaki gibidir.

<pre class="language-java"><code class="lang-java">import com.revrobotics.CANSparkMax;
import com.revrobotics.CANSparkLowLevel.MotorType;


new CANSparkMax(<a data-footnote-ref href="#user-content-fn-1">10</a>, MotorType.kBrushless);
</code></pre>

## Dokümantasyon

SparkMAX, REV Hardware Client üzerinden motor kontrolcüsü PID'sini test etmenize, motoru belirli bir yüzdede çalıştırmanıza ve ürün yazılımını güncellemenize olanak tanır. SparkMAX'i YAGSL için kullanmak için REV Hardware Client kurulumu gereklidir.

{% embed url="https://docs.revrobotics.com/rev-hardware-client/gs/install" %}
REV Hardware Client Kurulum rehberi + indirme
{% endembed %}

{% embed url="https://docs.revrobotics.com/rev-hardware-client/ion/spark-max" %}
REV Hardware Client içinde SparkMAX rehberi
{% endembed %}

{% hint style="warning" %}
REV Hardware Client aracılığıyla çalıştırmak için SparkMAX'in **başlangıçta** CAN veri yolundan bağlantısı kesilmelidir!
{% endhint %}

## PID Ayarlama

SparkMAX'in PID'sini ayarlamak için REV Hardware Client'ı açmanız, SparkMAX'i seçmeniz, ardından telemetri sekmesini açmanız ve sol paneldeki parametrelerle oynarken bunu konum kontrolüne ayarlamanız gerekir.

{% embed url="https://docs.revrobotics.com/rev-hardware-client/ion/telemetry" %}

## YAGSL Kontrol Listesi

* [ ] Tüm SparkMAX'leri benzersiz CAN ID'lerine ayarlayın.
* [ ] Tüm SparkMAX'leri en son ürün yazılımına güncelleyin.
* [ ] SparkMAX motoru saat yönünün tersine pozitif döndürür. (Saat yönünün tersine pozitif dönmüyorsa SparkMAX'i programatik olarak ters çevirin).
* [ ] Bir sürüş motoru için PID değerlerini ayarlayın.
* [ ] Bir dümenleme/azimut/açı motoru için PID değerlerini ayarlayın.

## İletişim

SparkMAX PWM üzerinden iletişim kurabilir ancak bu mod YAGSL tarafından desteklenmez çünkü hem sürüş hem de dümenleme/azimut/açı motorları için sensörler gereklidir.

## Modül örnek konfigürasyonu

Aşağıdaki örnek, bir modül konfigürasyon dosyası içindir, örneğin `frontleft.json`, `frontright.json`, `backleft.json` ve `backright.json`.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": <a data-footnote-ref href="#user-content-fn-2">"sparkmax"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-3">5</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-4">null</a>
  },
  "angle": {
    "type": <a data-footnote-ref href="#user-content-fn-5">"sparkmax"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-6">6</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-7">null</a>
  },
  "encoder": {
    "type": "cancoder",
    "id": 11,
    "canbus": null
  },
  "inverted": {
    "drive": <a data-footnote-ref href="#user-content-fn-8">false</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-9">false</a>
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
    "p": <a data-footnote-ref href="#user-content-fn-10">0.0020645</a>,
    "i": <a data-footnote-ref href="#user-content-fn-11">0</a>,
    "d": <a data-footnote-ref href="#user-content-fn-12">0</a>,
    "f": <a data-footnote-ref href="#user-content-fn-13">0</a>,
    "iz": 0
  },
  "angle": {
    "p": <a data-footnote-ref href="#user-content-fn-14">0.01</a>,
    "i": <a data-footnote-ref href="#user-content-fn-15">0</a>,
    "d": <a data-footnote-ref href="#user-content-fn-16">0</a>,
    "f": <a data-footnote-ref href="#user-content-fn-17">0</a>,
    "iz": 0
  }
}
</code></pre>

## Örnek `physicalproperties.json`

<pre class="language-json"><code class="lang-json">{
  "conversionFactor": {
    "drive": <a data-footnote-ref href="#user-content-fn-18">0.047286787200699704</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-19">16.8</a>
  },
  "currentLimit": {
    "drive": <a data-footnote-ref href="#user-content-fn-20">40</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-21">20</a>
  },
  "rampRate": {
    "drive": <a data-footnote-ref href="#user-content-fn-22">0.25</a>,
    "angle": <a data-footnote-ref href="#user-content-fn-23">0.25</a>
  },
  "wheelGripCoefficientOfFriction": 1.19,
  "optimalVoltage": 12
}
</code></pre>

[^1]: CAN ID'si `10` olan SparkMAX'i ifade eder

[^2]: Motor tipi olarak SparkMAX seçili.

[^3]: Bu sürüş motor kontrolcüsü SparkMAX için CAN ID 'si `5`

[^4]: SparkMAX'ler CANivore'larla uyumlu değildir bu nedenle bu `null` veya `""` olmalıdır.

[^5]: Motor tipi olarak SparkMAX seçili.

[^6]: Bu sürüş motor kontrolcüsü SparkMAX için CAN ID 'si `6`

[^7]: SparkMAX'ler CANivore'larla uyumlu değildir bu nedenle bu `null` veya `""` olmalıdır.

[^8]: Sürüş motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^9]: Dümenleme/azimut/açı motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^10]: Bu, SparkMAX üzerinde istenen hızı metre/saniye olarak korumak için kullanılan kP'dir.

[^11]: kI genellikle ayarlanması gerekmez.

[^12]: kD, bunu sönümlemek ve minimum aşma ile hıza daha hızlı ulaşmak için yararlı olacaktır.

[^13]: Bu, tekerleğin dönmesi için voltajın yüzdesi olarak statik ileri beslemedir (feedforward).

[^14]: Bu, SparkMAX üzerinde istenen açıyı derece olarak korumak için kullanılan kP'dir.

[^15]: kI genellikle ayarlanması gerekmez.

[^16]: kD, bunu sönümlemek ve minimum aşma ile hıza daha hızlı ulaşmak için yararlı olacaktır.

[^17]: Bu, tekerleğin dönmesi için voltajın yüzdesi olarak statik ileri beslemedir (feedforward).

[^18]: Tümü NEO olan bir MK4i L2 için dönüşüm faktörü. Bu, devir/dakika'yı metre/saniye'ye dönüştürür. Bu [`CANSparkMax.getEncoder().setPositionConversionFactor()`](https://codedocs.revrobotics.com/java/com/revrobotics/relativeencoder#setPositionConversionFactor\(double\)) kullanılarak motor kontrolcüsünde ayarlanır

[^19]: Tümü NEO olan bir MK4i L2 için dönüşüm faktörü. Bu, devirleri dereceye dönüştürür. Bu [`CANSparkMax.getEncoder().setPositionConversionFactor()`](https://codedocs.revrobotics.com/java/com/revrobotics/relativeencoder#setPositionConversionFactor\(double\)) kullanılarak motor kontrolcüsünde ayarlanır

[^20]: Sürüş motorunun çekebileceği maksimum akım `40`Amperdir. [`CANSparkMax.setSmartCurrentLimit`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setSmartCurrentLimit\(int\)) kullanılarak ayarlanır

[^21]: Sürüş motorunun çekebileceği maksimum akım `20`Amperdir. [`CANSparkMax.setSmartCurrentLimit`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setSmartCurrentLimit\(int\)) kullanılarak ayarlanır

[^22]: SparkMAX'ın voltaj düşüşlerini (brownouts) önlemek için kullanılan maksimum rampa oranı. Bu [`CANSparkMAX.setClosedLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setClosedLoopRampRate\(double\)) ve [`CANSparkMax.setOpenLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setOpenLoopRampRate\(double\)) kullanılarak ayarlanır

[^23]: SparkMAX'ın voltaj düşüşlerini (brownouts) önlemek için kullanılan maksimum rampa oranı. Bu [`CANSparkMAX.setClosedLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setClosedLoopRampRate\(double\)) ve [`CANSparkMax.setOpenLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setOpenLoopRampRate\(double\)) kullanılarak ayarlanır
