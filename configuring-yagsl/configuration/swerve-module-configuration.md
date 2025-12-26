# Swerve Modül Konfigürasyonu

## Swerve Modül Konfigürasyonu (`module/x.json`)

Swerve modül konfigürasyonu, her swerve modülünün benzersiz özelliklerini yapılandırır. [`SwerveModuleConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveModuleConfiguration.html) oluşturmak için kullanılan [`ModuleJson`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/json/ModuleJson.html) ile 1:1 eşlenir. Bu konfigürasyon dosyası doğrudan swerve kinematiği ile etkileşime girer.

{% hint style="warning" %}
**EĞER** açı motorlarınız kontrolden çıkarak dönüyorsa `inverted` içinde onları ters çevirmeniz gerekebilir
{% endhint %}

{% hint style="warning" %}
**EĞER** sürüş motorlarınız kontrolsüz bir şekilde dönüyorsa, ID'ler aracılığıyla sürüş motorunuzu açı motoru olarak ayarlamış olabilirsiniz. Bunları kontrol ettiğinizden emin olun!
{% endhint %}

## Alanlar

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>drive</code></td><td><a href="../../devices/motor-controllers/#motor-controller-configuration">Motor Kontrolcüsü</a></td><td>E</td><td>Sürüş motoru cihaz konfigürasyonu.</td></tr><tr><td><code>angle</code></td><td><a href="../../devices/motor-controllers/#motor-controller-configuration">Motor Kontrolcüsü</a></td><td>E</td><td>Açı motoru cihaz konfigürasyonu.</td></tr><tr><td><code>encoder</code></td><td><a href="../../devices/absolute-encoders.md#absolute-encoder-configuration">Mutlak Enkoder</a></td><td>E</td><td>Mutlak enkoder cihaz konfigürasyonu.</td></tr><tr><td><code>inverted</code></td><td><a href="swerve-module-configuration.md#motorconfig">MotorKonfigürasyonu</a></td><td>E</td><td>Boolean olarak her motorun ters çevirme durumu.</td></tr><tr><td><code>absoluteEncoderOffset</code></td><td>Derece</td><td>E</td><td>Mutlak enkoderin 0'dan ofseti derece cinsinden. Negatif bir sayı olması gerekebilir.</td></tr><tr><td><code>absoluteEncoderInverted</code></td><td>Bool</td><td>H</td><td>Mutlak Enkoderin ters çevirme durumu.</td></tr><tr><td><code>location</code></td><td><a href="swerve-module-configuration.md#location">Konum</a></td><td>E</td><td>Robotun merkezinden swerve modülünün inç cinsinden konumu. +x robotun önüne doğru, +y robotun soluna doğrudur.</td></tr><tr><td><code>conversionFactors</code></td><td><a href="physical-properties-configuration.md#conversion-factor-composition">Dönüşüm Faktörü Bileşimi </a><br><a href="physical-properties-configuration.md#fields"><code>physicalproperties.json</code></a> içindeki değeri, varsa ve <code>0</code>'a eşit değilse geçersiz kılar.</td><td>H</td><td><em>GEÇERSİZ KILMA (OVERRIDE)</em> Yerleşik PID için motor kontrolcüsüne uygulanan dönüşüm faktörleri, <a href="https://github.com/BroncBotz3481/YAGSL/wiki/Swerve-Drive"><code>swervedrive.json</code></a> içindeki bu ayarı geçersiz kılmak için kullanılır</td></tr><tr><td><code>useCosineCompensator</code></td><td>Bool</td><td>H</td><td>İstenen açılarla tam olarak hizalanmayan modüllerin hızını, açılar arasındaki farkın kosinüsü ile ölçekleyen kosinüs telafisini devre dışı bırakır.</td></tr></tbody></table>

#### MotorKonfigürasyonu

| İsim    | Birimler | Gerekli | Açıklama        |
| ------- | ----- | -------- | ------------------ |
| `drive` | Değer | E        | Sürüş motoru değeri. |
| `angle` | Değer | E        | Açı motoru değeri. |

#### Konum

| İsim    | Birimler | Gerekli | Açıklama                                              |
| ------- | ----- | -------- | -------------------------------------------------------- |
| `front` | Değer | E        | Robot merkezinden modüle ileri yönde inç. |
| `left`  | Değer | E        | Robot merkezinden modüle sol yönde inç.    |

## Örnek Konfigürasyon

<pre class="language-json"><code class="lang-json">{
  "drive": {
    <a data-footnote-ref href="#user-content-fn-1">"type": "sparkmax"</a>,
    "id": 2,
    "canbus": null
  },
  "angle": {
    <a data-footnote-ref href="#user-content-fn-2">"type": "sparkmax"</a>,
    "id": 1,
    "canbus": null
  },
  "encoder": {
    <a data-footnote-ref href="#user-content-fn-3">"type": "cancoder"</a>,
    "id": 10,
    "canbus": null
  },
  "inverted": {
    "drive": false,
    "angle": false
  },
  "absoluteEncoderInverted": false,
  "absoluteEncoderOffset": -50.977,
  "location": {
    "front": 12,
    "left": -12
  }
}
</code></pre>

[^1]: Daha fazlası için bkz. [motor-controllers](../../devices/motor-controllers/ "mention")

[^2]: Daha fazlası için bkz. [motor-controllers](../../devices/motor-controllers/ "mention")

[^3]: Daha fazlası için bkz. [absolute-encoders.md](../../devices/absolute-encoders.md "mention")
