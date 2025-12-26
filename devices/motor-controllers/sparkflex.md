# Spark Flex

Bu sayfa, **FIRÇASIZ BİR MOTORA (REV Vortex'ler)** bağlıyken REV Spark Flex'i ifade eder.

{% embed url="https://www.revrobotics.com/next-generation-spark-neo/" %}

{% embed url="https://www.revrobotics.com/rev-21-1652/" %}

{% embed url="https://www.revrobotics.com/rev-11-2159/" %}

## Başlarken

[`CANSparkFlex`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkflex) nesnesi oluşturmak için küçük bir örnek program aşağıdaki gibidir.

<pre class="language-java"><code class="lang-java">import com.revrobotics.CANSparkFlex;
import com.revrobotics.CANSparkLowLevel.MotorType;


new CANSparkFlex(<a data-footnote-ref href="#user-content-fn-1">10</a>, MotorType.kBrushless);
</code></pre>

## Dokümantasyon

Spark Flex, REV Hardware Client üzerinden motor kontrolcüsü PID'sini test etmenize, motoru belirli bir yüzdede çalıştırmanıza ve ürün yazılımını güncellemenize olanak tanır. SparkFlex'i YAGSL için kullanmak için REV Hardware Client kurulumu gereklidir.

{% embed url="https://docs.revrobotics.com/rev-hardware-client/gs/install" %}
REV Hardware Client Kurulum rehberi + indirme
{% endembed %}

{% embed url="https://docs.revrobotics.com/brushless/spark-flex/gs/make-it-spin" %}
REV Hardware Client kullanarak döndürün
{% endembed %}

{% hint style="warning" %}
REV Hardware Client aracılığıyla çalıştırmak için Spark Flex'in **başlangıçta** CAN veri yolundan bağlantısı kesilmelidir!
{% endhint %}

## PID Ayarlama

Spark Flex'in PID'sini ayarlamak için REV Hardware Client'ı açmanız, Spark Flex'i seçmeniz, ardından telemetri sekmesini açmanız ve sol paneldeki parametrelerle oynarken bunu konum kontrolüne ayarlamanız gerekir.

{% embed url="https://docs.revrobotics.com/rev-hardware-client/ion/telemetry" %}

## YAGSL Kontrol Listesi

* [ ] Tüm Spark Flex'leri benzersiz CAN ID'lerine ayarlayın.
* [ ] Tüm Spark Flex'leri en son ürün yazılımına güncelleyin.
* [ ] Spark Flex motoru saat yönünün tersine pozitif döndürür. (Saat yönünün tersine pozitif dönmüyorsa SparkFlex'i programatik olarak ters çevirin).
* [ ] Bir sürüş motoru için PID değerlerini ayarlayın.
* [ ] Bir dümenleme/azimut/açı motoru için PID değerlerini ayarlayın.

## İletişim

Spark Flex yalnızca CAN üzerinden iletişim kurabilir ve yakında CAN FD desteğiyle bazı heyecan verici yeni özellikler görebilir!

## Modül örnek konfigürasyonu

Aşağıdaki örnek, bir modül konfigürasyon dosyası içindir, örneğin `frontleft.json`, `frontright.json`, `backleft.json` ve `backright.json`.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": <a data-footnote-ref href="#user-content-fn-2">"sparkflex"</a>,
    "id": <a data-footnote-ref href="#user-content-fn-3">5</a>,
    "canbus": <a data-footnote-ref href="#user-content-fn-4">null</a>
  },
  "angle": {
    "type": <a data-footnote-ref href="#user-content-fn-5">"sparkflex"</a>,
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

[^1]: CAN ID'si `10` olan Spark Flex'i ifade eder

[^2]: Motor tipi olarak Spark Flex seçili.

[^3]: Bu sürüş motor kontrolcüsü Spark Flex için CAN ID 'si `5`

[^4]: Spark Flex'ler CANivore'larla uyumlu değildir bu nedenle bu `null` veya `""` olmalıdır. Bu gelecekte değişebilir!

[^5]: Motor tipi olarak Spark Flex seçili.

[^6]: Bu sürüş motor kontrolcüsü SparkFlex için CAN ID 'si `6`. (Not: Burada açı motoru kastediliyor olmalı ancak orijinal metinde drive motor controller yazılmış, çeviride de benzer şekilde bırakıldı veya düzeltilebilir. Bağlam `angle` bloğu olduğu için açı motorudur.)

[^7]: Spark Flex'ler CANivore'larla uyumlu değildir bu nedenle bu `null` veya `""` olmalıdır. Bu gelecekte değişebilir!

[^8]: Sürüş motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^9]: Dümenleme/azimut/açı motorunun saat yönünün tersine pozitif dönmesi için ters çevrilmesi gerekmez.

[^10]: Bu, Spark Flex üzerinde istenen hızı metre/saniye olarak korumak için kullanılan kP'dir.

[^11]: kI genellikle ayarlanması gerekmez.

[^12]: kD, bunu sönümlemek ve minimum aşma ile hıza daha hızlı ulaşmak için yararlı olacaktır.

[^13]: Bu, tekerleğin dönmesi için voltajın yüzadesi olarak statik ileri beslemedir (feedforward).

[^14]: Bu, Spark Flex üzerinde istenen açıyı derece olarak korumak için kullanılan kP'dir.

[^15]: kI genellikle ayarlanması gerekmez.

[^16]: kD, bunu sönümlemek ve minimum aşma ile hıza daha hızlı ulaşmak için yararlı olacaktır.

[^17]: Bu, tekerleğin dönmesi için voltajın yüzdesi olarak statik ileri beslemedir (feedforward).

[^18]: Tümü NEO olan bir MK4i L2 için dönüşüm faktörü. Bu, devir/dakika'yı metre/saniye'ye dönüştürür. Bu, [`CANSparkFlex.getEncoder().setPositionConversionFactor()`](https://codedocs.revrobotics.com/java/com/revrobotics/relativeencoder#setPositionConversionFactor\(double\)) kullanılarak motor kontrolcüsünde ayarlanır

[^19]: Tümü NEO olan bir MK4i L2 için dönüşüm faktörü. Bu, devirleri dereceye dönüştürür. Bu, [`CANSparkFlex.getEncoder().setPositionConversionFactor()`](https://codedocs.revrobotics.com/java/com/revrobotics/relativeencoder#setPositionConversionFactor\(double\)) kullanılarak motor kontrolcüsünde ayarlanır

[^20]: Sürüş motorunun çekebileceği maksimum akım `40`Amperdir. [`CANSparkFlex.setSmartCurrentLimit`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setSmartCurrentLimit\(int\)) kullanılarak ayarlanır

[^21]: Sürüş motorunun çekebileceği maksimum akım `20`Amperdir. [`CANSparkFlex.setSmartCurrentLimit`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setSmartCurrentLimit\(int\)) kullanılarak ayarlanır

[^22]: SparkMAX'ın (burada SparkFlex kastediliyor) voltaj düşüşlerini (brownouts) önlemek için kullanılan maksimum rampa oranı. Bu [`CANSparkFlex.setClosedLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setClosedLoopRampRate\(double\)) ve [`CANSparkFlex.setOpenLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setOpenLoopRampRate\(double\)) kullanılarak ayarlanır

[^23]: SparkMAX'ın (burada SparkFlex kastediliyor) voltaj düşüşlerini (brownouts) önlemek için kullanılan maksimum rampa oranı. Bu [`CANSparkMAX.setClosedLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setClosedLoopRampRate\(double\)) ve [`CANSparkMax.setOpenLoopRampRate`](https://codedocs.revrobotics.com/java/com/revrobotics/cansparkbase#setOpenLoopRampRate\(double\)) kullanılarak ayarlanır
