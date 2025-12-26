# Standart Dönüşüm Faktörleri

Bu sayfa, birkaç tipik modül için standart bir dönüşüm faktörleri seti sunar.

## Bunları nasıl buldum?

```java
    // Açı dönüşüm faktörü 360 / (DİŞLİ ORANI)
    //  Bu durumda dişli oranı tekerlek dönüşü başına 12.8 motor devridir.
    //  Motor devri başına enkoder çözünürlüğü motor devri başına 1'dir.
    double angleConversionFactor = SwerveMath.calculateDegreesPerSteeringRotation(12.8);
    // Motor dönüşüm faktörü (PI * METRE CİNSİNDEN TEKERLEK ÇAPI) / (DİŞLİ ORANI).
    //  Bu durumda tekerlek çapı 4 inçtir, bu metre/saniye elde etmek için metreye dönüştürülmelidir.
    //  Dişli oranı tekerlek dönüşü başına 6.75 motor devridir.
    //  Motor devri başına enkoder çözünürlüğü motor devri başına 1'dir.
    double driveConversionFactor = SwerveMath.calculateMetersPerRotation(Units.inchesToMeters(4), 6.75);
    System.out.println("\"conversionFactors\": {");
    System.out.println("\t\"angle\": {\"factor\": " + angleConversionFactor + "},");
    System.out.println("\t\"drive\": {\"factor\": " + driveConversionFactor + "}");
    System.out.println("}");
```

## MAX Swerve

{% tabs %}
{% tab title="12T" %}
```json
"conversionFactors": {
    "angle": {"gearRatio": 46.42},
    "drive": {"gearRatio": 5.50, "diameter": 3}
}
```
{% endtab %}

{% tab title="13T" %}
```json
"conversionFactors": {
    "angle": {"gearRatio": 46.42},
    "drive": {"gearRatio": 5.08, "diameter": 3}
}
```
{% endtab %}

{% tab title="14T" %}
```json
"conversionFactors": {
    "angle": {"gearRatio": 46.42},
    "drive": {"gearRatio": 4.71, "diameter": 3}
}
```
{% endtab %}
{% endtabs %}

## Swerve Drive Specialties (SDS)

{% tabs %}
{% tab title="MK4i L1 " %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 21.4285714286},
	"drive": {"gearRatio": 8.14, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4i L2" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 21.4285714286},
	"drive": {"gearRatio": 6.75, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4i L3" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 21.4285714286},
	"drive": {"gearRatio": 6.12, "diameter": 4}
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="MK4 L1" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 12.8},
	"drive": {"gearRatio": 8.14, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4 L2" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 12.8},
	"drive": {"gearRatio": 6.75, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4 L3" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 12.8},
	"drive": {"gearRatio": 6.12, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4 L4" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 12.8},
	"drive": {"gearRatio": 5.14, "diameter": 4}
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="MK4n L1" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 18.75},
	"drive": {"gearRatio": 7.13, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4n L2" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 18.75},
	"drive": {"gearRatio": 5.9, "diameter": 4}
}
```
{% endtab %}

{% tab title="MK4n L3" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 18.75},
	"drive": {"gearRatio": 5.36, "diameter": 4}
}
```
{% endtab %}
{% endtabs %}

## Thrifty Swerve

{% tabs %}
{% tab title="18T" %}
<figure><img src="../.gitbook/assets/thriftswerve.PNG" alt=""><figcaption><p>Thrifty Swerve Dişli Oranı Tablosu</p></figcaption></figure>

Aşağıdaki örnek NEO'lar tarafından kontrol edilen 3 inçlik tekerlekli 18T Çıkış Dişlisi ve 12T pinyon dişlisi içindir. Lütfen konfigürasyonunuz için yukarıdaki tabloya bakın.

Dümenleme motoru dişli oranı **25:1**

```json
"conversionFactors": {
	"angle": {"gearRatio": 25},
	"drive": {"gearRatio": 15, "diameter": 3}
}
```
{% endtab %}

{% tab title="16T" %}


<figure><img src="../.gitbook/assets/thriftswerve.PNG" alt=""><figcaption><p>Thrifty Swerve Dişli Oranı Tablosu</p></figcaption></figure>

Aşağıdaki örnek NEO'lar tarafından kontrol edilen 3 inçlik tekerlekli 16T Çıkış Dişlisi ve 12T pinyon dişlisi içindir. Lütfen konfigürasyonunuz için yukarıdaki tabloya bakın.

Dümenleme motoru dişli oranı **25:1**

```json
"conversionFactors": {
	"angle": {"gearRatio": 25},
	"drive": {"gearRatio": 16.9, "diameter": 3}
}
```
{% endtab %}
{% endtabs %}



## Plummer Industries

{% tabs %}
{% tab title="Corner Mid Ratio" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 28},
	"drive": {"gearRatio": 4, "diameter": 2.5}
}
```
{% endtab %}

{% tab title="Corner High Ratio" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 28},
	"drive": {"gearRatio": 3.25, "diameter": 2.5}
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Corner Mid Ratio - Linear" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 28},
	"drive": {"gearRatio": 4, "diameter": 2.5}
}
```
{% endtab %}

{% tab title="Corner High Ratio - Linear" %}
```json
"conversionFactors": {
	"angle": {"gearRatio": 28},
	"drive": {"gearRatio": 3.25, "diameter": 2.5}
}
```
{% endtab %}
{% endtabs %}
