# Önsöz

## Swerve Sürüşleri karmaşıktır!

Swerve sürüşlerinde ters gidebilecek birçok şey olabilir. Doğru bilgilerin tümüne sahip değilseniz hata ayıklama uzun ve meşakkatli bir süreç olabilir.

## Bir swerve sürüşünün yapılandırılması zaman alır!

Swerve ile deneyim seviyenize bağlı olarak; bir swerve sürüşünü yapılandırma deneyiminiz çok farklı olacaktır. Swerve modüllerini fiziksel olarak monte etmenin zaman aldığını hesaba katmayı unutmayın.

Daha önce swerve koduyla çalıştıysanız, YAGSL konfigürasyon sürecini oldukça kolay bulabilir ve belki de yaklaşık 30 dakika + PID ayarlaması sürebilir. Daha önce hiç çalışan bir swerve sürüşüne sahip olmadıysanız, doğru şekilde yapılandırmak **haftalar** sürebilir ve birçok yardım isteği gerekebilir. Her şey çalışacaktır ancak sabır şarttır! Her şeyi belgelemeye çalışıyorum, bu yüzden aklınıza gelebilecek her türlü soru için burayı kontrol ettiğinizden emin olun!

## Ne kadar umut ederseniz, yalvarırsanız, dua ederseniz veya adaklar adasanız da, bir swerve sürüşü her zaman "Şak diye çalışmaz"

[CTRE Tuner X Swerve Generator](https://pro.docs.ctr-electronics.com/en/latest/docs/tuner/tuner-swerve/index.html) gibi bazı araçlar, COTS modüllerinden gelen eylemlere ve önceden ayarlanmış verilere dayanarak sizin için swerve sürüşü sabitleri dosyasını yapılandırmak için masaüstü istemcileri kullanır. Bunlar çok yol kat ediyor ve YAGSL'in sunduğundan tamamen farklı (ve boş zamanımda yaratmayı haklı çıkarabileceğimden çok daha fazla iş). Bir swerve sürüşünü doğru bir şekilde programlamayı düşünmek için WPILib ve Java hakkında yeterli bir anlayışa ihtiyacınız olacak. Nasıl yapılacağını bilmeniz gereken bazı örnekler arasında kontrolcüleri [`XboxController`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj/XboxController.html)'dan [`Joystick`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj/Joystick.html)'e değiştirmek yer alır.
