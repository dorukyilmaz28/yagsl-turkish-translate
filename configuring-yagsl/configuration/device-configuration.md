# Cihaz Konfigürasyonu

## Cihaz Konfigürasyonu

Bir swerve sürüşündeki tüm cihazlar temel bir alan kümesine indirgenir. Cihaz konfigürasyonu, [`DeviceJson`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/json/DeviceJson.html) ile 1:1 eşleme ile ayrıştırma sırasında bu cihazları saklamak ve oluşturmak için kullanılır.

## Alanlar

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>type</code></td><td><a href="../../devices/absolute-encoders.md#possible-absolute-encoder-types">Enkoder <code>type</code></a><br><a href="../../devices/gyroscope.md#possible-gyroscope-types">IMU <code>type</code></a><br><a href="../../devices/motor-controllers/#possible-motor-controller-types">Motor <code>type</code></a></td><td>Y</td><td>Swerve tipinin oluşturulması için kullanılan cihaz tipi.</td></tr><tr><td><code>id</code></td><td>Integer</td><td>Y</td><td>CANBus üzerindeki cihaz ID'si veya belirli cihazlar için roboRIO üzerindeki pin ID'si.</td></tr><tr><td><code>canbus</code></td><td>String</td><td>N</td><td>Cihazın örneklendirileceği canbus. Yalnızca alternatif CAN veriyolları ile uyumlu cihazlarda çalışır.<br><br><code>type</code> <code>sparkmax_brushed</code> olduğunda bu, sürüş motorları için gerekli olan motora bağlı enkoderi tanımlar, açı motorları da ekli bir mutlak enkoder yoksa bunları kullanmalıdır. Bu durumda geçerli değerler <code>greyhill_63r256</code>, <code>srx_mag_encoder</code>, <code>throughbore</code>, <code>throughbore_dataport</code>, <code>greyhill_63r256_dataport</code>, <code>srx_mag_encoder_dataport</code>.<br>EKLİ ENKODER BİR MUTLAK ENKODER İSE BUNU AYARLAMAYIN</td></tr></tbody></table>

## Yararlı ipuçları

1. IMU'nuz umduğunuz kadar doğru değilse optimize edin, NavX'lerin bunun için [burada](https://pdocs.kauailabs.com/navx-mxp/guidance/best-practices/) güzel bir rehberi var
2. Kodu okuyun! Bir şeyi anlayamazsanız kodun tamamı belgelenmiştir ve okunması kolaydır.
