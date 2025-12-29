# Önsöz

## Swerve Drive karmaşıktır!

Swerve Drive'da ters gidebilecek birçok şey olabilir. Doğru bilgilerin tümüne sahip değilseniz hata ayıklama uzun ve meşakkatli bir süreç olabilir.

## Bir swerve drive'ın yapılandırılması zaman alır!

Swerve konusundaki deneyim seviyenize bağlı olarak, bir swerve sürüşünü yapılandırma süreci oldukça farklılık gösterebilir. Ayrıca, swerve modüllerinin fiziksel olarak monte edilmesinin de zaman aldığını mutlaka hesaba katmak gerekir.

Daha önce swerve sürüş kodlarıyla çalıştıysanız, YAGSL yapılandırma sürecini nispeten kolay bulabilirsiniz; çoğu durumda yaklaşık 30 dakika ve ardından PID ayarlaması yeterli olabilir. Ancak daha önce hiç çalışan bir swerve sürüşünüz olmadıysa, sistemi doğru şekilde yapılandırmak haftalar sürebilir ve bu süreçte çok sayıda yardım talebine ihtiyaç duyulabilir.

Sonuçta her şey çalışacaktır; ancak sabırlı olmak şarttır. Bu rehberde mümkün olduğunca her detay belgelenmiştir, bu nedenle aklınıza takılan sorular için önce burayı incelemeniz önerilir.

## Ne kadar umut ederseniz, yalvarırsanız, dua ederseniz veya adaklar adasanız da, bir swerve drive her zaman "Şak diye çalışmaz"

[CTRE Tuner X Swerve Generator](https://pro.docs.ctr-electronics.com/en/latest/docs/tuner/tuner-swerve/index.html) gibi bazı araçlar, COTS modüllerden alınan hazır veriler ve kullanıcı etkileşimleri sayesinde swerve drive'a ait sabitler (constants) dosyasını masaüstü istemcileri üzerinden otomatik olarak yapılandırır. Bu araçlar oldukça faydalıdır; ancak YAGSL’in sunduğu yaklaşımdan tamamen farklıdır ve benim boş zamanımda geliştirmemi haklı çıkaramayacağım kadar fazla emek gerektirir.

Bir swerve sürüşü doğru şekilde programlayabilmek için WPILib ve Java konusunda sağlam bir temel bilgiye sahip olmanız gerekir. Örneğin, kullanılan kontrolcüleri [`XboxController`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj/XboxController.html)’dan [`Joystick`](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj/Joystick.html)'e değiştirebilmek gibi temel düzenlemeleri rahatça yapabiliyor olmanız beklenir.
