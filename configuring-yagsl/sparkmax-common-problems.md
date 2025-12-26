---
description: Bunlar genellikle MAXSwerve robotlarında ortaya çıkar..
---

# SparkMax ve SparkFlex Yaygın Sorunlar

## NEO'lar SparkMAX Katilleridir!

Bir NEO çok uzun süre durdurulduğu (stalled) için yeterince ısındığında, sensör kablosuna pozitif kısa devre yapar, bu da düşük akım kanalından ÇOK yüksek bir akımın geçmesine ve SparkMax PCB'sinin erimesine neden olur. Bu, SparkMAX'ınızı ve katil NEO'nuza takılı olan her SparkMAX'ı ÖLDÜRECEKTİR.

Bu, açık bir SparkMAX'a takarsanız dizüstü bilgisayarınızı da öldürebilir çünkü kısa devre USB portuna kadar UZANABİLİR.

{% embed url="https://docs.google.com/presentation/d/1uM_uPD5HjzGwYUOmzZOmmgb1-KANiTTKI3o9aIJlPcc/edit?slide=id.p#slide=id.p" %}

## SparkMAX Mutlak Enkoder Kartları

[SparkMAX Mutlak Enkoder kartı](https://www.revrobotics.com/rev-11-3326/), yedeklilik sağlamak ve kartın gevşemesini önlemek için SparkMAX'a kablo bağıyla bağlanmalı ve sıcak silikonlanmalıdır.

### Mutlak enkoder kartına Throughbore Bağlantısı

[SparkMax Mutlak Enkoder kartı](https://www.revrobotics.com/rev-11-3326/) ile [REV Throughbore](https://www.revrobotics.com/rev-11-1271/) arasındaki konnektör, **HER İKİ** bağlantı noktasından sıcak silikonla yapıştırılmalıdır çünkü bunlar kolayca çıkabilir!

Kablo ayrıca tam ayarında gerdirilmelidir, eğer aşırı gerilirse kablo konnektöre tam girmeyebilir ve veriler eksik, bozuk veya kullanılamaz olabilir.

## Throughbore'lar mutlak enkoder ofsetine ayarlanmıyor

{% hint style="danger" %}
Bağlı mutlak enkoderlerle `factor` değerinizi `360` yapmanız artık gerekli değildir, ancak bunu yapmak aşağıda açıklanmıştır.
{% endhint %}

Bir Mutlak Enkoder kartı aracılığıyla SparkMax'a bağlı Mutlak Enkoderler kullandığınızda, normalde bir DutyCycleEncoder olarak tanımlanır.

`physicalproperties.json` içindeki `factor` değerini `360` olarak ayarlayarak bunu birincil geri bildirim cihazı olarak kullanabilirsiniz **ANCAK** bunu yaptığınızda JSON'da verilen mutlak enkoder ofseti UYGULANMAZ. Bu nedenle, enkoder ofsetini SparkMAX DutyCycleEncoder Ofset Flash Konfigürasyonuna AYARLAYACAK olan [`SwerveDrive.useExternalFeedbackSensor()`](https://broncbotz.org/YAGSL-Lib/docs/swervelib/SwerveDrive.html#useExternalFeedbackSensor\(\)) kullanmalısınız.

SparkMax DutyCycleEncoder Ofsetini sıfırlamak için, Spark DutyCycleEncoder Ofsetini 0'a ayarlayacak olan [`SwerveDrive.useInternalFeedbackSensor()`](https://broncbotz.org/YAGSL-Lib/docs/swervelib/SwerveDrive.html#useInternalFeedbackSensor\(\)) kullanmalısınız.

## Status Frame Hatası

Genellikle bir status frame hatası varsa, bu REV Throughbore bağlantınızın bir şekilde eksik olduğu veya motorunuzdan gelen sensör kablosunun gevşek veya kopuk olduğu anlamına gelir!

Bunu görürseniz **O SPARKMAX'A GİDEN TÜM SENSÖR KABLOLARINI KONTROL ETTİĞİNİZDEN EMİN OLUN!**
