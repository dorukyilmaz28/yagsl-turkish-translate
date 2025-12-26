# PIDF

## PIDF Konfigürasyonu

PIDF konfigürasyonları, modül hızı ve konumu ve robot başlığı gibi robot için PID veya PIDF konfigürasyonları ile ilgili bilgileri saklayan [`PIDFConfig`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/parser/PIDFConfig.html) ile 1:1 eşlenir. Her PIDF konfigürasyonunda her parametre kullanılmaz. Örneğin `heading` yalnızca PID'yi dikkate alır.

## Alanlar

Herhangi bir yerdeki `0`, temel olarak PIDF'in o kısmını devre dışı bırakır.

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>p</code></td><td>kP Kazancı</td><td>E</td><td>PID için Oransal (Proportional) Kazanç.</td></tr><tr><td><code>i</code></td><td>kI Kazancı</td><td>E</td><td>PID için İntegral (Integral) Kazanç.</td></tr><tr><td><code>d</code></td><td>kD Kazancı</td><td>E</td><td>PID için Türev (Derivative) Kazancı.</td></tr><tr><td><code>f</code></td><td>Sayı</td><td>H</td><td>PID için İleri Besleme (Feedforward).</td></tr><tr><td><code>iz</code></td><td>Sayı</td><td>H</td><td>PID entegratörü için integral bölgesi (zone).</td></tr><tr><td><code>output</code></td><td><a href="pidf.md#range">Aralık</a></td><td>H</td><td>PID için çıktı aralığı.</td></tr></tbody></table>

#### Aralık

<table data-full-width="true"><thead><tr><th>İsim</th><th>Birimler</th><th>Gerekli</th><th>Açıklama</th></tr></thead><tbody><tr><td><code>min</code></td><td>Sayı</td><td>H</td><td>PID aralığındaki minimum değer. Varsayılan <code>-1</code>.</td></tr><tr><td><code>max</code></td><td>Sayı</td><td>H</td><td>PID aralığındaki maksimum değer. Varsayılan <code>1</code>.</td></tr></tbody></table>
