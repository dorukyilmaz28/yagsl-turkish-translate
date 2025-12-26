# PIDF Özellikleri Konfigürasyonu

## Swerve Modül PID Konfigürasyonu (`modules/pidfpropreties.json`)

Bu dosya, her swerve modülü için sürüş ve motor modüllerinin integral bölgesi (integral zone) ve maksimum çıktısı ile PIDF değerlerini yapılandırır. [`PIDFPropertiesJson`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/json/PIDFPropertiesJson.html) ile 1:1 eşlenir ve [`SwerveDriveConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveDriveConfiguration.html) nesnesi başlatılırken kullanılır.

{% hint style="warning" %}
TalonFX/Kraken/Falcon açı motorları yüksek bir PID (yaklaşık \~`50` kP ve \~`0.32` kD) gerektirir.&#x20;
{% endhint %}

## Alanlar

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>drive</code></td><td><a href="pidf.md">Integral Zone ve Çıktı Limiti ile PIDF</a></td><td>E</td><td>Sürüş motorunda PIDF için kullanılacak konfigürasyon.</td></tr><tr><td><code>angle</code></td><td><a href="pidf.md">Integral Zone ve Çıktı Limiti ile PIDF</a></td><td>E</td><td>Açı motorunda PIDF için kullanılacak konfigürasyon.</td></tr></tbody></table>

## Örnek Konfigürasyon Dosyası

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "p": 0.0020645,
    "i": 0,
    "d": 0,
    "f": 0,
    "iz": 0
  },
  "angle": {
    <a data-footnote-ref href="#user-content-fn-1">"p": 0.01</a>,
    "i": 0,
    <a data-footnote-ref href="#user-content-fn-2">"d": 0</a>,
    "f": 0,
    "iz": 0
  }
}
</code></pre>

[how-to-tune-pidf.md](../../how-to-tune-pidf.md "mention")

[^1]: Krakenler ve Falconlar gibi TalonFX motor kontrolcüleri için bu yaklaşık `50` olmalıdır. Daha fazla bilgi için bkz. [how-to-tune-pidf.md](../../how-to-tune-pidf.md "mention")

[^2]: TalonFX motor kontrolcüleri için bu yaklaşık `0.32` olmalıdır. Daha fazla bilgi için bkz. [how-to-tune-pidf.md](../../how-to-tune-pidf.md "mention")
