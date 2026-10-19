# 4. Konuşan klipler: HeyGen Avatar IV + ağız düzeltmesi

## Temel bilgi

Tek bir fotoğrafı konuşturmak için HeyGen **Avatar IV** (`create_video_from_image`) kullanılır. Dudak, verilen sesten sürülür. Sorun: model kişinin gerçek dişlerini hiç görmediği için **dişleri uydurur**; heyecanlı cümle başlarında geniş, tek sıra beyaz bir sırıtma üretir. Ağız ayarı, ifade ayarı ve hareket komutu bunu tek başına çözmez (denendi).

## Çalışan yöntem: iki geçiş

### Geçiş 1: Avatar IV (baş, beden ve enerji buradan)
```
create_video_from_image(
  image: <sahne görseli>,
  audio: <sahnenin "sürücü" sesi>,
  expressiveness: "low",
  motion_prompt: "Natural relaxed talking. Moderate mouth opening only, relaxed jaw, lips keep a normal speaking shape even on loud or excited words. No wide grin, no big jaw drops, no laughing. Face shape and teeth stay stable and undistorted. Small natural head movement.",
  resolution: "1080p",
  aspect_ratio: "9:16"
)
```
Twist sahnesi (fısıltı) için motion prompt sonuna: "At the end he leans slightly closer and speaks softly."

### Geçiş 2: Lipsync (ağız buradan)
```
create_lipsync(
  video: <Geçiş 1 klibinin video_url'si>,
  audio: <AYNI sürücü ses>,
  mode: "speed",
  enable_dynamic_duration: false
)
```
Sonuç: baş/beden hareketi Avatar IV'ten kalır, ağız daha ölçülü yeniden çizilir, dişler geri çekilir. Ses-görüntü kayması ölçüldü: sıfır.

### Denenip elenenler (tekrar deneme)
- Sadece `expressiveness: low` + "teeth barely visible" komutu: sırıtma cümle başında yine çıkar.
- Ağzı kapalı, sessiz bir taban klip (`image_to_video`) + lipsync: ağız doğal ama sahne **çok durgun**. `precision` modu ilk saniyelerde ağzı hiç oynatmayabilir.
- Hareketli sessiz taban + lipsync: gözler ve yüz abartılı açılır, bozulur.

## Sürücü ses ve kurgu sesi ayrı

- **Kurgu sesi:** doğal dinamikli seslendirme (izleyicinin duyduğu).
- **Sürücü ses:** aynı dosyanın sıkıştırılmış kopyası; sadece Avatar IV ve lipsync'e verilir. Bağırılan yerlerde çene aşırı açılmaz.
  ffmpeg: `acompressor=threshold=-20dB:ratio=4:attack=3:release=90:makeup=2,alimiter=limit=0.7`
- İkisinin zamanlaması **birebir** aynı olmalı: aynı kırpma, başa 0,10 sn, sona 0,25 sn sessizlik.
- Sohbet hattında ffmpeg yoksa: sürücü ses = kurgu sesi; geçiş 2 yine çalışır.

## Akış

1. Önce **en heyecanlı sahneyi** tek başına iki geçişten geçir, kullanıcıya göster.
2. Onay gelince kalan sahneleri **paralel** başlat (aynı anda en fazla 10 render).
3. Her klibi indir; süresi sesle eşleşiyor mu kontrol et.
4. Görsel/ses dosyalarını HeyGen'e bir kez yükle; aynı asset kimliğini tekrar kullan.

## Kontrol: ağız ve dişler (her teslimden önce)
- Her sahnenin en yüksek sesli kelimesinin anından bir kare al, yüze kırp, eski/yeni yan yana koy.
- Bak: tek sıra beyaz diş var mı, yanak/yüz bozuluyor mu, gözler doğal mı.
- Kullanıcı "fazla" ya da "durgun" derse ara yolu öner: Geçiş 1'i koru, Geçiş 2'yi uygula.

## Geçiş klipleri (sahneler arası)
HeyGen `image_to_video` ya da başka bir görüntüden videoya modeli. Geçiş, önceki konuşan klibin **gerçek son karesinden** başlamalı (atlama olmasın). Prompt kalıbı:
```
Continuous camera move starting exactly from this frame: the camera pulls back out of the [MEKÂN 1] and flies smoothly into [MEKÂN 2], one unbroken motion, no cut, motion blur, cinematic, same lighting continuity, vertical 9:16, no text
```
Geçişi kurguda cümle arasındaki nefese (0,6-0,7 sn) sığdır: ilk yarı hızlı, sonu yavaşlayarak sahneye otursun.

## Maliyet disiplini
Üretimden önce ve sonra kalan krediyi oku, farkı kullanıcıya söyle. Tek ölçümden birim maliyet çıkarma.
