# Swerve Sürüş Konfigürasyonu

## Swerve Sürüşü (`swervedrive.json`)

Swerve Sürüşü JSON konfigürasyon dosyası, genel Swerve Sürüşü ile ilgili her şeyi konfigüre eder. [`SwerveDrive`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html) nesnesini oluşturmak için kullanılan bir [`SwerveDriveConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveDriveConfiguration.html) oluşturan [`SwerveDriveJson`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/json/SwerveDriveJson.html) ile 1:1 eşlenir.

## JSON Alanları

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>imu</code></td><td><a href="../../devices/gyroscope.md#gyroscope-configuration">Jiroskop</a></td><td>E</td><td>Robotun başlığını (heading) belirlemek için kullanılan robot IMU.</td></tr><tr><td><code>invertedIMU</code></td><td>Boolean</td><td>E</td><td>IMU'nun ters çevirme durumu.</td></tr><tr><td><code>modules</code></td><td>String dizisi</td><td>E</td><td>Ön soldan başlayarak saat yönünde sırayla Modül JSON'ları.</td></tr></tbody></table>

## Örnek Konfigürasyon

<pre class="language-json"><code class="lang-json">{
  "imu": {
    <a data-footnote-ref href="#user-content-fn-1">"type": "pigeon2"</a>,
    <a data-footnote-ref href="#user-content-fn-2">"id": 13</a>,
    <a data-footnote-ref href="#user-content-fn-3">"canbus"</a>: <a data-footnote-ref href="#user-content-fn-4">"canivore"</a>
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

[^1]: Daha fazla bilgi için bkz. [gyroscope.md](../../devices/gyroscope.md "mention")

[^2]: IMU/gyro roboRIO'ya bağlı olduğunda, SPI veya MXP portu üzerinden bağlı değilse, bu üzerinde bulunduğu kanal numarası olmalıdır. \
    \
    Cihaz bir CAN cihazıysa bu, cihazın CAN ID'si olacaktır.

[^3]: Bu örnekte CANivore `"canivore"` olarak adlandırılmıştır ve `pigeon2`, roboRIO'nun CAN döngüsü (cihaz bunun üzerinde bulunsaydı `null` veya `"rio"` olurdu) yerine CANivore'a bağlanmıştır.

[^4]: IMU/jiroskop bir CANivore üzerinde değilse bu `null` veya `"rio"` olmalıdır.
