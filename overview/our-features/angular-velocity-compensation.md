# Açısal Hız Telafisi

YAGSL, açısal hız telafisi için Jack-in-the-bot tarafından öncülük edilen bir yöntem kullanır. Bunu etkinleştirmek için `SwerveDrive.setAngularVelocityCompensation(true, true, 0.1);` kullanırsınız; burada ilk parametre teleop'ta etkin durumu, ikincisi otonomda etkin durumu ve üçüncüsü kullanılacak katsayıdır.

İlk kez etkinleştirildiğinde sapma (skew) önemli ölçüde daha kötüyse değeri tersine çevirmeyi (negatif yapmayı) deneyin.

1. Dönerken düz bir çizgide hareket ederek ayarlayın.
   * Test en iyi sağ çubuktaki açısal hız kontrolleriyle yapılır.
2. Sapmadan görsel olarak memnun olana kadar değeri değiştirin.
3. Ayarınızın farklı öteleme ve dönme büyüklükleriyle çalıştığından emin olun.
4. Bu, teleop'ta sapmayı azaltırsa, otonomu iyileştirebilir.

**PR** [**#231**](https://github.com/BroncBotz3481/YAGSL-Example/pull/231) **içinde** [**yapplejack**](https://github.com/yapplejack) tarafından oluşturuldu.
