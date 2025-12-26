# Kaymayı (Drift) Ayarlayarak Giderme

Mevcut pozunuzu hesaplamaya çalışırken, poz tahmincisi (pose estimator) bir dereceye kadar mükemmel bir iş çıkarır (bunu ayarlayabilirsiniz ancak çoğu takım yapmaz).

Ayarlamanız gereken ilk şey [sürüş ve açı PID'leridir.](how-to-tune-pidf.md)

Odometriye yardımcı olması için görüntüleme (vision) kullanıyorsanız takımlar `SwerveDrivePoseEstimator` `visionStdDev` değerini ayarlamalıdır. Görüntülemeyi ayarlamak çoğunlukla mesafeye bağlı bir ölçekle standart sapma üzerinde tahmin ve kontroldür. Bazı takımlar, X mesafesindeki tüm tahmini pozları filtreleyerek daha iyi stabilite elde ederler.

Bundan sonra, sistem gecikmesini telafi etmek için ayrıklaştırmayı (discretization) ayarlayabilirsiniz. Ayrıklaştırmayı ayarlama hakkında daha fazla bilgi [buradadır.](../overview/our-features/chassis-speed-discretization.md)

Bundan sonra, [jiroskop sistem gecikmesini telafi etmek için açısal hız katsayınızı](../overview/our-features/angular-velocity-compensation.md) ayarlayabilirsiniz (canivore üzerinde bir pigeon'ınız olduğunda o kadar gerekli değildir).

Bunların hepsi birbirinin üzerine inşa edilen bireysel ayarlama adımlarıdır.

{% hint style="warning" %}
Alt adımlardan biriyle oynarsanız, tüm üst adımlar senkronizasyon dışı kalır ve jiroskopunuz gibi bir parçayı değiştirmeniz gerekirse yine de hepsini yeniden yapmanız gerekebilir.
{% endhint %}

Kaymayı ayarlayarak giderme konusundaki ağır matematiksel açıklama burada mevcuttur.

{% embed url="https://github.com/calcmogul/controls-engineering-in-frc" %}
