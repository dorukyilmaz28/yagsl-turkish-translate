# Ne zaman ters çevirmeli?

Swerve Modülleri ve Swerve Sürüşleri, düzgün çalışması için bazı ters çevirmeler (inversions) gerektirir. Amaç her şeyin saat yönünün tersine pozitif artmasını sağlamaktır!

{% hint style="warning" %}
Dişlileriniz yerdeyken gıcırdıyorsa ancak bloklar üzerindeyken gıcırdamıyorsa ve tekerlekleriniz doğru yönlere bakıp dönüyorsa, ters çevirmek yerine PID ayarı yapmanız gerekebilir!
{% endhint %}

{% hint style="warning" %}
EĞER yanlış ters çevrilmişseniz modülleriniz veya robotunuz "kontrolden çıkmış şekilde" dönebilir
{% endhint %}

## Swerve Motorları

Motorunuzu saat yönünün tersine döndürdüğünüzde NetworkTables `swerve/modules/.../Raw Absolute Encoder` ve `swerve/modules/.../Raw Angle Encoder` değerlerinin ikisi de artmalıdır.

* ![](../.gitbook/assets/ShuffleboardAbsoluteEncoderHighlight.png)
* `swerve/modules/.../Raw Absolute Encoder` değerlerini not edin ve bunları modül JSON'larında `absoluteEncoderOffset` için kullanın.

## Modülünüzü saat yönünün tersine döndürün

{% hint style="danger" %}
Modüllerinizi yukarıdan aşağıya bakışta **SAAT YÖNÜNÜN TERSİNE (COUNTERclockwise)** döndürün.
{% endhint %}

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption><p>Mor renk, konik dişlilerinizin (bevels) bakması gereken yönü gösterir (fotoğraf Takım 2876 tarafından)</p></figcaption></figure>

Swerve sürüşü yan yatmış veya başka bir şekilde kaldırılmış olmalıdır. Swerve modülü konik dişlileriniz gösterildiği gibi sola bakmalıdır. Swerve modüllerini döndürmek için gösterildiği gibi saat yönünün tersine döndürülmeleri gerekir.

### EĞER `swerve/modules/.../Raw Angle Encoder` azalıyorsa...

Azalan her modül için açı motorunuzu ters çevirin!

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": "sparkmax",
    "id": 2,
    "canbus": null
  },
  "angle": {
    "type": "sparkmax",
    "id": 1,
    "canbus": null
  },
  "encoder": {
    "type": "cancoder",
    "id": 10,
    "canbus": null
  },
  "inverted": {
    "drive": false,
<strong>    "angle": true
</strong>  },
  "absoluteEncoderInverted": false,
  "absoluteEncoderOffset": -50.977,
  "location": {
    "front": 12,
    "left": -12
  }
}
</code></pre>

### EĞER `swerve/modules/.../Raw Absolute Encoder` azalıyorsa...

Mutlak enkoderi, burada gösterildiği gibi `absoluteEncoderInverted` ile modül JSON'unda ters çevirin.

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": "sparkmax",
    "id": 2,
    "canbus": null
  },
  "angle": {
    "type": "sparkmax",
    "id": 1,
    "canbus": null
  },
  "encoder": {
    "type": "cancoder",
    "id": 10,
    "canbus": null
  },
  "inverted": {
    "drive": false,
    "angle": false
  },
<strong>  "absoluteEncoderInverted": true,
</strong>  "absoluteEncoderOffset": -50.977,
  "location": {
    "front": 12,
    "left": -12
  }
}
</code></pre>

## Tekerleğinizi saat yönünün tersine döndürün

{% hint style="warning" %}
Bazen, robotu döndürdüğünüzde robot alana yönelik modda sürerken ön/arka tarafını değiştiriyorsa bunları tersine çevirmeniz gerekebilir.
{% endhint %}

{% hint style="danger" %}
#### Odometri uyuşmazlığı

Robotunuz odometride geriye ve gerçek hayatta ileriye doğru giderken, yerinde dönüşün Saat Yönünün Tersi-Pozitif hareketi oluşturduğunu koruyorsa, bu yamayı uygulamanız gerekebilir.

Bu davranışı düzeltmek için her modül dosyasındaki her `absoluteEncoderOffset` değerine `180` eklemelisiniz.
{% endhint %}

### EĞER `swerve/modules/.../Raw Drive Encoder` azalıyorsa...

Azalan her modül için sürüş motorunuzu ters çevirin!

<pre class="language-json"><code class="lang-json">{
  "drive": {
    "type": "sparkmax",
    "id": 2,
    "canbus": null
  },
  "angle": {
    "type": "sparkmax",
    "id": 1,
    "canbus": null
  },
  "encoder": {
    "type": "cancoder",
    "id": 10,
    "canbus": null
  },
  "inverted": {
<strong>    "drive": true,
</strong>    "angle": false
  },
  "absoluteEncoderInverted": false,
  "absoluteEncoderOffset": -50.977,
  "location": {
    "front": 12,
    "left": -12
  }
}
</code></pre>

## Robotunuzu saat yönünün tersine döndürün

{% hint style="danger" %}
Robotunuzun saat yönünün tersine dönmesinin, tekerleklere güç verildiğinde böyle görünmesi gerektiğini unutmayın! Eğer görünmüyorsa her modül dosyası için ID'lerinizi değiştirmeniz **GEREKECEKTİR**.
{% endhint %}

<figure><img src="../.gitbook/assets/id_change1.png" alt=""><figcaption><p>Swerve modül dosyalarında yeniden konumlandırılan ID'ler</p></figcaption></figure>

Sürücü panelinizdeki `Raw IMU Yaw` alanının arttığını fark etmelisiniz. Artmıyorsa, IMU'nuzu bu şekilde ters çevirmeniz gerekir.

<pre class="language-json"><code class="lang-json">{
  "imu": {
    <a data-footnote-ref href="#user-content-fn-1">"type": "pigeon2"</a>,
    "id": 13,
    "canbus": "canivore"
  },
<strong>  "invertedIMU": true,
</strong>  "modules": [
    "frontleft.json",
    "frontright.json",
    "backleft.json",
    "backright.json"
  ]
}
</code></pre>

[^1]: Daha fazla bilgi için bkz. [gyroscope.md](../devices/gyroscope.md "mention")
