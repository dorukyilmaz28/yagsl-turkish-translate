# Modül Otomatik Senkronizasyonu

YAGSL, swerve modülü yarım saniye boyunca hareketsiz kaldığında, açı/steering/azimuth motoruna ait dahili enkoder ile mutlak (absolute) enkoderi otomatik olarak senkronize eder.\
Bu senkronizasyon, dahili enkoder ile mutlak enkoder arasındaki fark belirlenen deadband değerinden büyükse gerçekleştirilir.

Bu özellik, `SwerveDrive.setModuleEncoderAutoSynchronize(bool, double)` metodu ile yapılandırılabilir.\
İlk parametre otomatik senkronizasyonun açık veya kapalı olduğunu, ikinci parametre ise derece cinsinden deadband değerini belirler.
