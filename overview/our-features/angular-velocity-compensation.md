# Açısal Hız Telafisi

YAGSL, açısal hız telafisi için Jack-in-the-bot tarafından geliştirilen bir yöntemi kullanır. Bu özellik etkinleştirildiğinde, robot dönerken oluşan kayma (skew) azaltılmaya çalışılır.

Bu özellik, `SwerveDrive.setAngularVelocityCompensation(true, true, 0.1)` metodu ile etkinleştirilir.

Parametrelerin anlamı:

* Birinci parametre: Teleop modunda etkin olup olmadığı
* İkinci parametre: Otonom modda etkin olup olmadığı
* Üçüncü parametre: Kullanılacak telafi katsayısı (coefficient)

***

#### Ayarlama (Tuning)

Özelliği ilk kez etkinleştirdiğinizde, eğer robotun kayması belirgin şekilde artıyorsa, katsayının işaretini tersine çevirmeyi deneyin.

Ayarlama işlemi şu şekilde yapılmalıdır:

* Robotu düz bir hatta hareket ettirirken aynı anda döndürün
* Açısal hız kontrolü için sağ joystick kullanılması önerilir
* Kayma görsel olarak azalacak şekilde katsayıyı değiştirin
* Farklı doğrusal ve açısal hız büyüklüklerinde ayarın tutarlı çalıştığından emin olun

Teleop sürüşte kaymayı azaltıyorsa, otonom sürüş performansını da iyileştirebilir.

***

Bu özellik, **PR** [**#231**](https://github.com/BroncBotz3481/YAGSL-Example/pull/231) kapsamında [**yapplejack**](https://github.com/yapplejack) tarafından eklenmiştir.&#x20;
