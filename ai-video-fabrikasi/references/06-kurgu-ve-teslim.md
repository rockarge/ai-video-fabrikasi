# 6. Kurgu, ses mix, teslim

## Zaman planı
- Sahneler sırayla: `konuşan klip → geçiş (0,65 sn) → konuşan klip ...`. Kanca sonrası kaydırma geçişi daha uzun olabilir (1,3-1,6 sn) ve üstünde kısa bir cümle ("Kaydırıp geçiyorsun!") akabilir.
- Her konuşan klip kendi ses dosyasının süresi kadar sürer. Plan, ses süreleri ölçüldükten sonra yazılır.
- Kapanış kartı son sahneden sonra 2-3 sn.

## Müzik ve efekt
- Müzik bölümlere göre değişebilir: kanca (merak), sorun (tuhaf/gergin), fabrika ve absürt zincir (enerjik), twist öncesi **müzik susar** ("Aslında..." sessizlikte gelir), kapanışta boom + enerjik dönüş.
- Geçişlere whoosh; riser + boom vaat cümlesinden önce.
- Seslendirme müziği bastırsın (sidechain/ducking, yaklaşık 4:1). Seslendirmeye hafif EQ (80 Hz altı kes, 280 Hz -2 dB, 3,4 kHz +1,5 dB, hafif de-esser). Yapay tiz ekleme (exciter) sadece dar bantlı seste gerekir.

## Mastering
- Hedef **-14 LUFS**, true peak **-1,3 dBTP** (Instagram, YouTube, Spotify uyumlu).
- Lineer kazanç + oversample'lı true-peak limiter; dinamik loudnorm tek geçişte konuşmayı ezebilir.
- Görüntü 1 kare geride kalıyorsa sesi ~40 ms geciktir (ölçerek).
- Son dosya: H.264, 1080x1920, 30 fps, AAC 320k. 4K/60 fps gereksiz, platform zaten küçültür.

## Hızlandırılmış sürümler
Reels'te 1.1x genelde daha iyi tutar. ffmpeg: `setpts=PTS/1.1` + `atempo=1.1` (1.2x için 1.2). Orijinali her zaman sakla.

## Sohbet hattında (CapCut)
Claude kullanıcıya şunu verir: sahne sırası, her klibin dosya adı ve başlangıç saniyesi, geçiş süreleri, ekrana çıkacak yazılar ve zamanları, müzik bölümleri. Kullanıcı CapCut'ta bu listeyle kurar.

## Teslim öncesi kontrol listesi
- [ ] Her sahnede ağız/diş kontrolü yapıldı (en yüksek sesli kelime anı)
- [ ] Ses-görüntü kayması ölçüldü (0 ya da en fazla 1 kare)
- [ ] Yazılar doğru kelimeye oturuyor (vurgu anlarından kare al)
- [ ] Türkçe karakterler doğru
- [ ] Ses -14 LUFS, tepe -1,3 dBTP altı
- [ ] Bir kare telefonda gerçek Reels arayüzünde açıldı; kullanıcı adı/açıklama yazının üstüne binmiyor
- [ ] Videoda yapay zekâ ile üretildiği belirtildi (platform etiketi ya da ekranda küçük not)
- [ ] Kapanış çağrısı ve anahtar kelime net
