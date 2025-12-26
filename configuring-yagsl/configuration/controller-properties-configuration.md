# Kontrolcü Özellikleri Konfigürasyonu

## Swerve Kontrolcüsü (`controllerproperties.json`)

Swerve Kontrolcüsü, swerve sürüşünün otonom ve sürüş modlarında nasıl çalışacağına ilişkin konfigürasyon seçeneklerini saklar; bu modlar, bir joystick'e dayalı olarak robotun başlığını (heading) ayarlar. JSON dosyaları, [`SwerveControllerConfiguration`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/SwerveControllerConfiguration.html) oluşturan [`ControllerPropertiesJson`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/json/ControllerPropertiesJson.html) ile 1:1 eşlenir. Buradaki değerler otonom için **SON DERECE** önemlidir çünkü Otonom fonksiyonların çalışması için robot başlığı PID'sinin doğru şekilde ayarlanması gerekir.

## Alanlar

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>angleJoystickRadiusDeadband</code></td><td>Double</td><td>E</td><td>Robotun başlık ayarlamasına izin vermek için açı kontrol joystick'inin minimum yarıçapı.</td></tr><tr><td><code>heading</code></td><td><a href="pidf-properties-configuration/pidf.md">PID</a></td><td>E</td><td>Robot başlığını kontrol etmek için kullanılan PID.</td></tr></tbody></table>

## Örnek Konfigürasyon

<pre class="language-json"><code class="lang-json">{
  <a data-footnote-ref href="#user-content-fn-1">"angleJoystickRadiusDeadband": 0.5</a>,
  "heading": {
    "p": 0.4,
    "i": 0,
    "d": 0.01
  }
}
</code></pre>

[^1]: 2 eksene dayalı olarak dönülecek açıyı bulurken bir ölü bölge (deadband) ayarlamak için [`SwerveController.getTargetSpeeds`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveController.html#getTargetSpeeds\(double,double,double,double,double,double\)) ile kullanılır.
