# haberai-runner

Zamanlayıcı deposu. **İçinde haber hattının kodu yoktur.**

Asıl kod ve veri private [`fruyorsan/haberai`](https://github.com/fruyorsan/haberai)
deposunda durur. Bu depo yalnızca GitHub Actions üzerinden hattı çalıştırır:

1. `actions/checkout` + deploy key ile private depoyu çeker (`HABERAI_DEPLOY_KEY`).
2. `pipeline.yml` adımlarını çalıştırır (RSS → AI → kapak → derleme).
3. Veriyi private depoya geri iter, siteyi Cloudflare Pages'e yayınlar.
4. Zinciri `tetik` dalına push ile sürdürür (`CHAIN_DEPLOY_KEY`).

Neden böyle: GitHub Actions dakikaları **public** depolarda sınırsız, private
depoda aylık 2.000 dk (Free). Hat tur başına ~18–22 dk ve zincirle sürekli
koştuğu için ayda ~36.000 dk tüketiyor; private kotası 1–2 günde biterdi.
Private depoda Actions bu yüzden kapatıldı.

Gizli anahtarlar (secret) burada tanımlıdır; değerleri GitHub üzerinden
okunamaz, yalnızca yazılabilir.
