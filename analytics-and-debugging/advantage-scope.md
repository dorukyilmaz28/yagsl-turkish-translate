---
description: >-
  Advantage Scope, takım 6328 Mechanical Advantage'ın izniyle, hata ayıklama
  için size geri bildirim vermek üzere Swerve Sürüşünü görselleştirebilen bir
  veri görselleştirme aracıdır.
---

# Advantage Scope

## Açma

2024 Sezonundan beri, [Advantage Scope](https://github.com/Mechanical-Advantage/AdvantageScope) WPILib kurulumuna dahil edilmiştir. Harici bir indirme gerekmez, ancak her WPILib güncellemesinde, WPILib araçlarının en son sürümünü almak için [WPILib yükleyicisini](https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html) yeniden indirmelisiniz.

## Advantage Scope Konfigürasyonu

1. Dizüstü bilgisayarı robota bağlayın
2. `AdvantageScope (WPILib)`i açın veya VS Code'da komut paletini açıp `WPILib: Start Tool` yazın ve `AdvantageScope`a tıklayın
3. `Help` (Yardım) ardından `Show Preferences` (Tercihleri Göster)e tıklayın

<figure><img src="../.gitbook/assets/AdvantageScope-Preferences.png" alt=""><figcaption><p>Advantage Scope'un yardım menüsü</p></figcaption></figure>

4. Takım numaranıza göre roboRIO IP adresini girin. `10.TE.AM.2`

<figure><img src="../.gitbook/assets/AdvantageScope-Preferences-IP.png" alt=""><figcaption><p>roboRIO Adres alanı vurgulanmış</p></figcaption></figure>

5. Robota (veya simülatöre) bağlanın

<figure><img src="../.gitbook/assets/AdvantageScope-Connect.png" alt=""><figcaption><p>Robot menüsüne bağlan</p></figcaption></figure>

6. Pencerenin sağ tarafındaki `+` işaretine tıklayarak yeni bir sekme ekleyin

<figure><img src="../.gitbook/assets/AdvantageScope-Add.png" alt=""><figcaption><p>Yeni sekme ekle</p></figcaption></figure>

7. Yeni bir :crab: Swerve sekmesi ekleyin

<figure><img src="../.gitbook/assets/AdvantageScope-Swerve.png" alt=""><figcaption><p>Swerve sekmesi</p></figcaption></figure>

8.  Modül durumlarını ve rotasyonunu Smart Dashboard'dan Alanlara bağlayın.

    1. `SmartDashboard/swerve` menüsü altında `advantagescope/` içindeki her şeyi `Sources` (Kaynaklar) alanına sürükleyin.
    2. `SmartDashboard/swerve/advantagescope/desiredStates`i ekleyebilmeniz için önce robotunuzu etkinleştirmeniz gerekebilir

    <figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
9.  Data sütununu Swerve Sürüşünüzün özelliklerine göre ayarlayın.

    1. `Data` sütunu altında `Max Speed` alanını `SmartDashboard/swerve/maxSpeed` girişinin değerine değiştirin.

    <figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
10. (İsteğe bağlı) Display sütununu, Size (Sol-Sağ) ve Size (Ön-Arka) değerlerini `SmartDashboard/swerve/sizeLeftRight` ve `SmartDashboard/swerve/sizeFrontBack` altındakilerle eşleşecek şekilde değiştirerek robotunuzun şasi boyutlarını doğru bir şekilde gösterecek şekilde ayarlayın.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Genel Bakış

<figure><img src="../.gitbook/assets/FRC_web_component_snapshot.png" alt=""><figcaption><p>Yanlış bir konfigürasyonla hareket halindeki Swerve Drivebase.<br>(Bunu Advantage Scope'un gerçek bir resmiyle değiştirmek gerekiyor)</p></figcaption></figure>

{% hint style="info" %}
**KIRMIZI** çizgiler swerve modülünün ölçülen hızı ve konumudur.

**MAVİ** çizgiler gönderilen modülün hızı ve konumudur!
{% endhint %}
