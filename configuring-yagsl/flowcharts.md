# Akış Şemaları

## Swerve Sürüş Şeması

<figure><img src="../.gitbook/assets/devilbots_cropped_swerve_orientation.png" alt=""><figcaption></figcaption></figure>

## Dikkat edilmesi gerekenler



{% hint style="danger" %}
Pigeon 1 ve NavX 1 gibi eski jiroskoplar, açık kaldıkları süre uzadıkça kayma (drift) yaşarlar. Programınızın başlangıcında jiroskopunuzu yeniden başlatmayı veya sıfırlamayı düşünün.
{% endhint %}

## Swerve Modülleri

### Swerve modülleri "kontrolden çıkmış" şekilde dönüyor

<figure><img src="../.gitbook/assets/flowchart2.png" alt=""><figcaption></figcaption></figure>

## Swerve Modülü doğru dönmüyor.

Bunun için daha sonra bir akış şeması ekleyeceğim ama temel olarak şöyledir.

1. CAN ID'leri, motor tipleri ve mutlak enkoder tipleri doğru mu?
2. Modül konumları doğru mu?
3. Mutlak manyetik enkoder kullanıyor musunuz?
   1. Mıknatısınızda loctite kullandınız mı?
   2. Mıknatıs üzerinde iyi bir (normalde yeşil LED) okumanız var mı?
4. Mutlak enkoder ofsetini, tekerleklerin konik dişlileri sola ve tekerlekler önden arkaya düz bakarken mi ayarladınız?
5. Ters çevirme durumları için [when-to-invert.md](when-to-invert.md "mention")'yi kontrol ettiniz mi?
6. PID'nizi ayarladınız mı?

## Swerve Sürüşü "kontrolden çıkıyor"

<figure><img src="../.gitbook/assets/flowchart4.png" alt=""><figcaption></figcaption></figure>
