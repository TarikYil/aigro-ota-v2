# AIgro OTA — v2 kart

Public OTA manifestleri ve firmware dosyaları — **yalnızca v2 kart** (ESP32-S3, `BOARD_ID = s3-v2`).

* Firmware kaynağı (private): `TarikYil/aigro-firmware-v2`
* Bu repoya yalnızca o reponun GitHub Actions iş akışları yazar (`OTA_REPO_TOKEN` yalnız bu repoya yetkili).
* **v1 kartlar bu repoyu okumaz.** v1'in OTA dosyaları ayrı repoda durur (`TarikYil/aigro_ota`);
  bu repodaki hiçbir şey onları etkilemez.

## Düzen

```
ota/s3-v2/beta/manifest.json              <- beta kanalındaki v2 cihazların okuduğu manifest
ota/s3-v2/beta/<sürüm>/AIgro_Firmware.bin
ota/s3-v2/stable/manifest.json            <- stable kanalındaki v2 cihazların okuduğu manifest
ota/s3-v2/stable/<sürüm>/AIgro_Firmware.bin
```

Cihaz şu adresi okur: `https://raw.githubusercontent.com/TarikYil/aigro-ota-v2/main/ota/s3-v2/<kanal>/manifest.json`

Manifest alanları: `version`, `url`, `sha256`, `channel`, `board` (`s3-v2`). Cihaz; kart adı uyuşmayan,
sürümü çalışandan yeni olmayan ya da SHA-256'sı tutmayan imajı reddeder; yeni imaj internete
bağlanamazsa eski sürüme geri döner.

Elle dosya eklemeyin. Yayınlar `aigro-firmware-v2` reposundaki "Beta Firmware Release" (elle
tetiklenir) ve "Stable Firmware Release" (`v*.*.*` etiketi) iş akışlarıyla yapılır.
