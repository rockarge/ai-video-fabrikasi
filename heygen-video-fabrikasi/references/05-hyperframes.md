# 5. Yazı katmanı: HyperFrames

HyperFrames, HTML ile yazılan programlanabilir video katmanıdır (HeyGen). İki kullanım yolu var; **yanlış yol en pahalı hatadır.**

| Yol | Ne zaman | Not |
|---|---|---|
| **Bağlayıcı (hosted `compose`)** | Sıfırdan motion graphic: başlık kartı, kapanış kartı, sayı/veri animasyonu, konuşan kişi yok | Girdi sadece metin. **Var olan bir videonun üstüne yazı koymak için KULLANMA**: taban katman kavramı yok, sessizce yanlış çıktı verir |
| **Yerel skill'ler** (`npx skills add heygen-com/hyperframes`) | Var olan videonun üstüne altyazı/kart (`embedded-captions`, `talking-head-recut`), render öncesi kare önizleme | Claude Code / terminal gerekir. Render yerel ve bedava |

Sohbet hattındaysan: kapanış kartını ve tek başına motion parçalarını bağlayıcıyla üret, üstüne yazı işini CapCut'ta yap (Claude'dan zaman damgalı yazı listesi iste).

## Prompt anatomisi (altı parça)

**Rota · Spec · Beat'ler · Kopya · Teknik · Negatifler**

```
Rota: motion-graphics (konuşan kişi yok)
Spec: 1080x1920, 9:16, 30 fps, 3.0 sn, koyu zemin
Beat 1 (0.0-0.6s): ekranın ortasında yorum çubuğu yatıktan kalkar
Beat 2 (0.6-1.8s): çubuğa "Sistemi istiyorum" yazılır, harf harf
Beat 3 (1.8-2.4s): gönder butonu basılır, halka dalgası yayılır
Beat 4 (2.4-3.0s): hafif bir ambient idle'a oturur
Kopya: "Sistemi istiyorum" / "YORUMLARA YAZ"
Teknik: Instagram güvenli alan dışında kalsın: alt 420 px, üst 250 px, sağ 180 px, sol 60 px boş
Negatifler: slayt geçişi yok, logo deforme edilmez, rastgele parıltı yok, no audio at all
```

## Kurallar
- **Beat'leri zaman damgasıyla yaz:** `Beat 2 (4-5s): ...` HyperFrames'in ana dili bu.
- **Ekranda görünecek her metni tırnak içinde ver.** Yoksa başka kelimeyle yazar. Satır sonu için `/`.
- **Spectacle beat:** tek bir abartılı anı adıyla belirt ("Beat 3: BOOM anı"). Adsız patlama düşer.
- **En-boy oranını söyle.** Söylemezsen 1920x1080 yatay gelir.
- "Hareketsiz durur" yazma → donmuş kare olur. "Hafif bir ambient idle'a oturur" yaz.
- Aynı anda iki olay yazma; sırala: "sayaç 4,2 sn'de kaybolur; 4,2 sn'de damga gelir".
- "No narration" sessizlik demek değil. Gerçek sessizlik için "no audio at all".
- Markanın resmi logosuna efekt, oran değişikliği, renk değişikliği uygulama. 3D his logonun **çevresinde** kurulur (ızgara zemin, yörünge halkaları).

## Altyazı modeli (yerel `embedded-captions`)
| Katman | Ne | Kural |
|---|---|---|
| drop | ııı, kekeleme | gösterilmez |
| rail | sıradan konuşma, birebir | varsayılan, alt-orta, okunur |
| embed | zirve kelime ("HAYIR!", "BEDAVA!", "YOK!") | blok başına en fazla 1, öznenin arkasına düşebilir |
**En sık hata her kelimeyi büyük yapmak.** Rail metnin çoğunu taşır; büyük kelime nadir ve hak edilmiş olur. Aktif kelimeyi renkle vurgula (tek renk).

## Türkçe
- Transkripti her zaman düzelt: özel isim, rakam, marka.
- ğ ü ş ı ö ç İ karakterlerini önizleme karesinde **gözle** doğrula; İ/ı en sık kırılan yer.

## Ses değişirse yazı katmanı
Bütün zamanları elle değiştirme. Eski kelime zamanlarını yeni kelime zamanlarına eşleyen parçalı-doğrusal bir `M(t)` fonksiyonu yaz ve timeline'daki her konumu ondan geçir. Eski ve yeni seslendirmede kelime sayısı ve sırası aynı olmalı (önce kontrol et).

## Render öncesi
Önizleme karelerini al (bedava), Türkçe karakterleri, güvenli alanı ve çakışmaları gözle kontrol et. Sonra render.
