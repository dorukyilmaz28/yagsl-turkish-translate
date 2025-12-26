# Bağımlılık Kurulumu

## WPILib

{% embed url="https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html" %}

## REV Hardware Client

{% embed url="https://docs.revrobotics.com/rev-hardware-client/gs/install" %}

## CTRE Tuner X

{% embed url="https://v6.docs.ctr-electronics.com/en/latest/docs/installation/installation-frc.html" %}

## Satıcı URL'leri

Aşağıda, YAGSL'in düzgün çalışması için kurulması gereken URL'lerin bir listesi bulunmaktadır; bunlar satıcı web sitelerinde ve YAGSL dokümantasyonunda yayınlanmaktadır. Bunları kurmak için WPILib belgelerindeki bu kılavuzu izleyin.

{% embed url="https://docs.wpilib.org/en/stable/docs/software/vscode-overview/3rd-party-libraries.html#installing-libraries" %}



<table data-full-width="true"><thead><tr><th width="177">Satıcı</th><th width="597">URL</th><th>Çevrimdışı Kurulum</th></tr></thead><tbody><tr><td>maple-sim</td><td><code>https://shenzhen-robotics-alliance.github.io/maple-sim/vendordep/maple-sim.json</code></td><td></td></tr><tr><td>CTRE Phoenix 6</td><td><code>https://maven.ctr-electronics.com/release/com/ctre/phoenix6/latest/Phoenix6-frc2025-latest.json</code></td><td><a href="https://v6.docs.ctr-electronics.com/en/latest/docs/installation/installation-frc.html">Tuner X</a></td></tr><tr><td>CTRE Phoenix 5</td><td><code>https://maven.ctr-electronics.com/release/com/ctre/phoenix/Phoenix5-frc2025-latest.json</code></td><td><a href="https://store.ctr-electronics.com/software/">Phoenix Tuner</a></td></tr><tr><td>REVLib</td><td><code>https://software-metadata.revrobotics.com/REVLib-2025.json</code></td><td><a href="https://github.com/REVrobotics/REV-Software-Binaries/releases/tag/rhc-1.6.2">REV Hardware Client</a> Çevrimdışı</td></tr><tr><td>Studica (NavX)</td><td><code>https://dev.studica.com/releases/2025/Studica-2025.0.1.json</code></td><td><a href="https://www.studica.ca/en/navx-2-mxp-robotics-navigation-sensor"><code>https://www.studica.ca/en/navx-2-mxp-robotics-navigation-sensor</code></a></td></tr><tr><td>ReduxLib</td><td><code>https://frcsdk.reduxrobotics.com/ReduxLib_2025.json</code></td><td><code>unavailable</code></td></tr><tr><td>YAGSL</td><td><code>https://broncbotz3481.github.io/YAGSL-Lib/yagsl/yagsl.json</code></td><td><code>YAGSL-Example</code></td></tr></tbody></table>

YAGSL'in genel yapısı nedeniyle, satıcı kütüphanesinin desteklediği ürünlerin hiçbirini kullanmasanız bile YAGSL'in çalışması için tüm bu vendordep'lerin (satıcı bağımlılıkları) kurulu olması gerekir.
