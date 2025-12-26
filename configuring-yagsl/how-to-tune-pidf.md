# PIDF Nasıl Ayarlanır

{% hint style="warning" %}
Swerve dümenleme/açı/azimut motorları, en üst ve en alt noktada (örneğin "ön" ve "arka") PID sarmalaması (wrapping) etkinleştirilmiştir, PID'nizi ayarlarken sol veya sağ öteleme (translation) ile test etmek isteyebilirsiniz.
{% endhint %}

## Temel fikir

YAGSL, swerve modülü klasörü içindeki [`pidfproperties.json`](configuration/pidf-properties-configuration/) dosyasında PIDF değerlerine sahiptir.

Bu daha önce şu şekilde en basit forma indirgenmiştir.

* P: olmak istediğin yerde değilsen, oraya git.
* I: uzun zamandır olmak istediğin yerde değilsen, oraya daha hızlı git
* D: olmak istediğin yere yaklaşıyorsan, yavaşla.
  * 78 tarafından bulunan [Bu CD Gönderisi](https://www.chiefdelphi.com/t/finally-i-understand-pid/450811) tarafından bulunan [Video](https://www.youtube.com/watch?v=qKy98Cbcltw)

<figure><img src="../.gitbook/assets/pid_explainer.png" alt=""><figcaption></figcaption></figure>

## PIDF Ayarlama

Bunu açıklamanın bir başka iyi yolu [CTRE'den](https://pro.docs.ctr-electronics.com/en/latest/docs/api-reference/device-specific/talonfx/closed-loop-requests.html)

Manuel ayarlama tipik olarak şu süreci izler:

1. $$P$$, $$I$$ ve $$D$$ değerlerini sıfıra ayarlayın.
2. Çıktı ayar noktası etrafında **titreşmeye** (ossilasyon) **başlayana** kadar $$P$$'yi artırın.
3. Tepkide **seğirmeye** (jittering) neden **olmadan** $$D$$'yi mümkün olduğunca artırın.

## WPI Rehberi

WPILib, PID dahil olmak üzere harika belgelere sahip, bu yüzden kontrol etmenizi şiddetle tavsiye ederim!

{% embed url="https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/introduction-to-pid.html" %}
PID Temelleri
{% endembed %}

{% embed url="https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-flywheel.html" %}
Sürüş motorları gibi Hız Ayarlama!
{% endembed %}

{% embed url="https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-turret.html" %}
Dümenleme/açı/azimut motorları gibi pozisyon ayarlama!
{% endembed %}

## Başlangıç Noktaları

PIDF değerleri her robot için değişecektir, bu nedenle ayarlama ve test gereklidir. İşte karşılık geldikleri motor kontrolcüsü türleri ile belgelediğim bazı başlangıç noktaları.

{% tabs %}
{% tab title="Sürüş Motoru" %}
#### SparkMax

Her modül için `drive` motor `type` (tipi) `sparkmax` olduğunda, başlangıç noktası bu olabilir.

<pre class="language-json"><code class="lang-json">{
<strong>  "drive": {
</strong><strong>    "p": 0.0020645,
</strong><strong>    "i": 0,
</strong><strong>    "d": 0,
</strong><strong>    "f": 0,
</strong><strong>    "iz": 0
</strong><strong>  },
</strong>  "angle": {
    "p": 0.01,
    "i": 0,
    "d": 0,
    "f": 0,
    "iz": 0
  }
}
</code></pre>

#### TalonFX

Her modül için sürüş motoru `type`'ı `talonfx` veya benzeri (`kraken`/`falcon`) olduğunda, başlangıç noktası bu olabilir.

<pre class="language-json"><code class="lang-json">{
<strong>  "drive": {
</strong><strong>    "p": 1,
</strong><strong>    "i": 0,
</strong><strong>    "d": 0,
</strong><strong>    "f": 0,
</strong><strong>    "iz": 0
</strong><strong>  },
</strong>  "angle": {
    "p": 50,
    "i": 0,
    "d": 0.32,
    "f": 0,
    "iz": 0
  }
}
</code></pre>
{% endtab %}

{% tab title="Açı Motoru" %}
#### SparkMax

Her modül için `angle` motor `type`'ı `sparkmax` olduğunda, başlangıç noktası bu olabilir.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "p": 0.0020645,
    "i": 0,
    "d": 0,
    "f": 0,
    "iz": 0
  },
<strong>  "angle": {
</strong><strong>    "p": 0.01,
</strong><strong>    "i": 0,
</strong><strong>    "d": 0,
</strong><strong>    "f": 0,
</strong><strong>    "iz": 0
</strong><strong>  }
</strong>}
</code></pre>

#### TalonFX

Her modül için `angle` motor `type`'ı `talonfx` veya benzeri (`kraken`/`falcon`) olduğunda, başlangıç noktası bu olabilir.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "p": 1,
    "i": 0,
    "d": 0,
    "f": 0,
    "iz": 0
  },
<strong>  "angle": {
</strong><strong>    "p": 50,
</strong><strong>    "i": 0,
</strong><strong>    "d": 0.32,
</strong><strong>    "f": 0,
</strong><strong>    "iz": 0
</strong><strong>  }
</strong>}
</code></pre>
{% endtab %}
{% endtabs %}
