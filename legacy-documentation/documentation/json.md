# JSON

## JSON Dosyaları

JSON, "JavaScript Object Notation" (JavaScript Nesne Gösterimi) anlamına gelir, popüler bir konfigürasyon ve dize veri formatıdır. Daha fazlasını [buradan](https://www.w3schools.com/js/js\_json\_intro.asp) öğrenin

## Swerve dizini neye benzemelidir?

Bir swerve sürüşü oluşturmak için swerve dizini buna benzemelidir. [`swervedrive.json`](https://github.com/BroncBotz3481/YAGSL-Example/tree/main/src/main/deploy/swerve/swervedrive.json) içinde swerve modüllerinizi `"modules": [ "frontleft.json", "frontright.json", "backleft.json", "backright.json"]` olarak tanımladığınızı varsayarsak.

```
└── swerve
    ├── controllerproperties.json
    ├── modules
    │   ├── backleft.json
    │   ├── backright.json
    │   ├── frontleft.json
    │   ├── frontright.json
    │   ├── physicalproperties.json
    │   └── pidfproperties.json
    └── swervedrive.json
```

`modules` klasörü, `controllerproperties.json`, `physicalproperties.json`, `pidfproperties.json` ve `swervedrive.json` dosyaları swerve sürüşünü oluşturmak için gereklidir. Her birinin, swerve sürüşünün bazı fiziksel ve bazı soyut özelliklerine karşılık gelen belirli alanları vardır.

#### Konfigürasyon seçeneklerini görmek için aşağıdaki her bir JSON'a tıklayın

* `swervedrive.json`
* `controllerproperties.json`
* `pidfpropreties.json`
* `physicalproperties.json`
* `backleft.json`, `backright.json`, `frontleft.json`, `frontright.json`
