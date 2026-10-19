---
name: heygen-video-fabrikasi
description: "Tek bir fotoğraftan ve kendi sesinden, kamerasız, absürt mekânlarda konuşan sinematik AI videosu (Reels/Shorts) üretir. Kullanıcıyı sorularla tanır, sonra HeyGen, ElevenLabs ve HyperFrames için test edilmiş promptları ve adımları uygular. Tetikleyici: heygen videosu, ai avatar videosu, kamerasız video, ses klonu, avatar konuşturma, reels üret, video fabrikası."
---

# HeyGen Video Fabrikası

Bu skill, kullanıcının **kendi yüzü ve kendi sesiyle**, hiç kamera kullanmadan, her sahnesi farklı ve absürt bir mekânda geçen (çamaşır makinesinin içi, buzdolabı, arı kovanı, akvaryum, uzay...) kısa bir dikey video üretir.

Skill kişiye özel bilgi taşımaz. Her şeyi kullanıcıya sorarak kurar. Promptlar ve kalite kuralları gerçek üretimde denenmiş, hatası ölçülmüş yöntemlerdir.

## Altın kurallar

1. **Önce tanı, sonra üret.** Aşağıdaki "Tanışma" adımı bitmeden hiçbir kredi harcayan çağrı yapılmaz.
2. **Soruları tek tek sor.** Bir mesajda tek soru, cevabı al, sonrakine geç. Kullanıcı "sen karar ver" derse varsayılanı söyle ve devam et.
3. **Kredi harcamadan önce bir sahnede dene.** 10 sahne üretmeden önce en zor sahneyi (en heyecanlı cümle) tek başına üret, kullanıcıya göster, onay al.
4. **Kulak ve göz yerine ölç.** Ses ve görüntüyü dinleyemiyor/izleyemiyorsan "dinledim" deme. Ölçtüğünü söyle (süre, ses seviyesi, spektrum, kare görüntüsü) ve kararı kullanıcının kulağına bırak.
5. **Her yeni ders kullanıcının notlarına.** Kullanıcı bir şeyi beğenmediyse (ör. "ağız çok açılıyor") bunu proje notuna yaz, sonraki sahnelerde de uygula.

## Tanışma (ilk konuşma, sırayla, tek tek)

Cevapları en sonda tek bir **"Video Profili"** notunda özetle ve kullanıcıya göster; bir sonraki oturumda bu notu yapıştırmasını iste.

1. **Amaç:** Video ne için? (kişisel hesap, marka tanıtımı, ürün, eğitim, eğlence) Hangi platform? (Instagram Reels, TikTok, YouTube Shorts). Varsayılan: Reels, 9:16, 45-70 sn.
2. **Mesaj:** İzleyici videonun sonunda tek bir şeyi hatırlasa, ne olmalı? Bir cümleyle.
3. **Ton:** Enerjik/eğlenceli mi, sakin/güven veren mi, ironik/kuru mizah mı?
4. **Dil:** Seslendirme hangi dilde? (Türkçe varsayılan)
5. **Yüz:** Kullanılacak fotoğrafın var mı? Gerekli: yüz net, önden ya da hafif açılı, **ağız kapalı ve nötr**, iyi ışık, tek kişi. Yoksa HeyGen'deki bir avatar mı kullanılacak?
6. **Ses:** Kendi sesin klonlansın mı, hazır bir ses mi? Klon istenirse `references/02-ses.md` içindeki kayıt rehberini ver.
7. **Araçlar:** Hangileri hesabında açık? HeyGen (plan ve kalan kredi), ElevenLabs (opsiyonel), Claude'da HeyGen bağlayıcısı, HyperFrames (bağlayıcı ya da yerel kurulum), kurgu için CapCut ya da benzeri.
8. **Teknik seviye:** Terminal/Claude Code kullanıyor musun, yoksa sadece sohbet mi? Cevap hattı belirler (aşağıda).
9. **Mekânlar:** Kendi fikrin var mı, yoksa ben önerip seçtireyim mi? (5-10 sahne)

## İki hat

| Hat | Kim için | Nasıl |
|---|---|---|
| **Sohbet hattı** | Kod yok, Claude sohbeti + HeyGen bağlayıcısı | Senaryo, ses, sahne görselleri, konuşan klipler Claude üzerinden; birleştirme CapCut'ta, Claude kesim listesi verir |
| **Tam hat** | Claude Code / terminal + ffmpeg | Yukarıdakiler + otomatik kurgu, müzik/efekt mix, ses mastering, HyperFrames yazı katmanı, hızlandırılmış sürümler |

## Üretim sırası

| Adım | Ne | Rehber |
|---|---|---|
| 1 | Senaryo: kanca, soru-cevap ritmi, sahne başına bir cümle | `references/01-senaryo.md` |
| 2 | Ses: klon (gerekirse) + duygulu seslendirme, satır satır | `references/02-ses.md` |
| 3 | Sahne görselleri: "nesnenin içinden bakış" kareleri, kimlik kilidi | `references/03-sahne-gorselleri.md` |
| 4 | Konuşan klipler: Avatar IV + ağız düzeltmesi | `references/04-heygen-avatar.md` |
| 5 | Yazı katmanı: altyazı rayı, vurgu kelimeleri, kapanış kartı | `references/05-hyperframes.md` |
| 6 | Kurgu, ses mix, teslim ve kontrol listesi | `references/06-kurgu-ve-teslim.md` |

Her adımın sonunda kullanıcıya bir şey göster (dosya, kare, ses) ve "devam mı, düzeltme mi" diye sor. Adım atlanmaz; adım 2'deki ses süreleri adım 4'ü ve 6'yı belirler.

## En sık 5 hata (hepsi gerçek üretimde yaşandı)

1. **Dişlerin uydurulması.** Tek fotoğraftan konuşan avatar, kişinin gerçek dişlerini bilmediği için heyecanlı yerlerde geniş, beyaz, yapay bir sırıtma üretir. Çözüm `references/04-heygen-avatar.md` içinde: Avatar IV + üstüne lipsync (speed).
2. **Dar bantlı ses klonu.** WhatsApp sesli mesajından ya da telefon görüşmesinden alınan klon boğuk çıkar. Kayıt kayıpsız alınır, mesajlaşma uygulamasıyla gönderilmez.
3. **Tek tonda seslendirme.** Klon kayıtta ne duyduysa onu öğrenir; seslendirme de satır satır duygu yönlendirmesi ister.
4. **Ses ile yazının kayması.** Ses değişince yazı katmanının bütün zamanları kayar. Zamanları elle düzeltme; kelime zamanlarından otomatik eşle.
5. **Sesin bir sahnede bağırıp diğerinde fısıldaması.** Teslimden önce ses seviyesi tek standarda çekilir (-14 LUFS).
