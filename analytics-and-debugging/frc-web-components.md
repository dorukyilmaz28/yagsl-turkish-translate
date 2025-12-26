# FRC Web Components

FRC Web Components, Swerve Sürüşünü görselleştirmenin ve size yardımcı olması için YAGSL geliştiricilerine yararlı geri bildirimler vermenin kolay bir yoludur.

## İndirme

Bunu indirmek ve kurmak için lütfen doğru dosyayı seçin ve bu sayfadan çalıştırın.<br>

{% embed url="https://github.com/frc-web-components/app/releases/latest" %}

## FRC Web Components Konfigürasyonu

<figure><img src="../.gitbook/assets/yagsl_fwc.gif" alt=""><figcaption></figcaption></figure>

1. Dizüstü bilgisayarı robota bağlayın
2. "FRC Web Components"ı açın
3. "Settings"e (Ayarlar) tıklayın

<figure><img src="../.gitbook/assets/fwc_config6.png" alt=""><figcaption><p>Ayarlar vurgulanmış halde FRC Web Components</p></figcaption></figure>

4. Takım numaranıza göre roboRIO IP adresini girin. `10.TE.AM.2`

{% embed url="https://docs.wpilib.org/en/stable/docs/networking/networking-introduction/ip-configurations.html#te-am-ip-notation" %}

<figure><img src="../.gitbook/assets/fwc_conrfig5.png" alt=""><figcaption><p>FRC Web Components için Dashboard ayarları.</p></figcaption></figure>

5. Widget menüsünü açın.

<figure><img src="../.gitbook/assets/fwc_config4.png" alt=""><figcaption><p>Buraya basın.</p></figcaption></figure>

6. `Swerve Drivebase`i seçin ve `Append`e (Ekle) tıklayın

<figure><img src="../.gitbook/assets/fwc_config3.png" alt=""><figcaption></figcaption></figure>

7. Widget'ın üzerine tıklayın.
8. "Connect to data source..."a (Veri kaynağına bağlan...) tıklayın

<figure><img src="../.gitbook/assets/fwc_config2.png" alt=""><figcaption></figcaption></figure>

9. Buradaki seçime basarak `SmartDashboard/swerve`ye bağlanın.

<figure><img src="../.gitbook/assets/FWC_config1.png" alt=""><figcaption></figcaption></figure>

10. "Close"a (Kapat) basın

## Genel Bakış

<figure><img src="../.gitbook/assets/FRC_web_component_snapshot.png" alt=""><figcaption><p>Yanlış bir konfigürasyonla hareket halindeki Swerve Drivebase.</p></figcaption></figure>

{% hint style="warning" %}
**MAVİ** çizgiler swerve modülünün ölçülen hızı ve konumudur.

**KIRMIZI** çizgiler gönderilen modülün hızı ve konumudur!
{% endhint %}
