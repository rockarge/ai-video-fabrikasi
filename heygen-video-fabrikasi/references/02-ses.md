# 2. Ses: klon ve duygulu seslendirme

## A. Kendi sesinin klonu

### Kayıt (kullanıcıya bu haliyle ver)
- iPhone: **Ayarlar > Sesli Notlar > Ses Kalitesi > Kayıpsız.** Kayıt modu **mono** kalsın (stereo klona bir şey katmaz, faz sorunu getirir). Android: WAV/FLAC kaydeden bir uygulama.
- Oda: halılı, perdeli, eşyalı. Boş salon yankı yapar. Klima, buzdolabı, kahve makinesi kapalı, yakındaki şarj aletleri prizden çekili.
- Telefon ağızdan 20-30 cm, mikrofon hafif yandan (p/b patlaması olmasın), bir yere yaslı.
- 2-3 dakika. Takılınca durma: 2 sn bekle, cümleyi baştan oku. Okuma bitince 20-30 sn serbest konuşmak klonun daha doğal çıkmasını sağlar.
- **Mesajlaşma uygulamasıyla gönderme** (WhatsApp vb. sesi sıkıştırır, klon boğuk çıkar). AirDrop, bulut ya da dosya olarak.

### Okuma metni şablonu (kullanıcının hayatına göre doldur)
Metni 5 tona böl; klon kayıtta ne duyarsa onu öğrenir:
1. **Sakin sohbet:** kim olduğu, nerede olduğu, bugün ne yaptığı.
2. **Enerjik soru-cevap:** "Peki neden? Çünkü... Sorun X mi? Hayır!"
3. **Tempolu anlatım:** sayılar, saat, kısa bir anekdot.
4. **Duygu değişimi:** şaşırma ("Vay be!"), hafif gülme, rahatlama.
5. **Sıcak kapanış:** izleyiciye hitap, vedalaşma.
Videoda geçecek özel kelimeleri (marka adı, ürün, teknik terim) metne serpiştir; klon onları kişinin ağzından öğrensin.

### Kaydı ölç (dinlemek yerine)
- Format: kayıpsız (ALAC/WAV/FLAC), 44.1-48 kHz, mono.
- Seviye: ortalama -14 ile -20 LUFS arası, tepe -1 dB'nin altında (kırpılma yok).
- Gürültü: sessiz anlarda -50 dB ve altı iyi.
- **Tam bant mı:** konuşma anında 8-12 kHz bandının enerjisi, sessiz anlara göre en az ~20 dB yukarıda olmalı. Değilse kaynak dar bantlıdır, klon boğuk çıkar; yeniden kayıt iste.
- Baştaki ve sondaki sessizliği kırp. Aradaki 1-2 sn'lik boşluklar kesilmez.

### Klonu aç
- **HeyGen:** dosyayı asset olarak yükle, `clone_voice` (dil kodu ver, gürültü temizleme sessiz odada KAPALI), durum `complete` olana kadar bekle.
- **ElevenLabs (Instant Voice Cloning):** dosya sınırı **11 MB**. 2-3 dk'lık 24-bit WAV bunu aşar; aynı kaydı **16-bit FLAC**'a çevir (kayıpsız, ~5 MB). Gürültü temizleme kapalı.
- **A/B testi:** eski ve yeni ses (ya da iki aday ses) aynı cümleyi okusun; "önce A, 1 sn sessizlik, sonra B" tek dosya yap. Kararı kullanıcı ve güvendiği bir kulak versin.

## B. Duygulu seslendirme

### Model ve ayar
- ElevenLabs **eleven_v4** (yoksa eleven_v3). Ayar: stability 0.5, similarity 0.8, hız 1.04-1.08 (Reels için hafif hızlı).
- HeyGen üzerinden de olur: `create_speech` + `engine: elevenlabs` + `model_id: eleven_v4`.
- **Satır satır üret** (sahne başına bir dosya). Tek parça uzun seslendirme, sahne kesimini ve dudak senkronunu zorlaştırır.
- Her satıra **2 alım** (farklı seed). Sonra satır bazında en iyisini seç ve karıştır.

### Duygu etiketleri (metnin içine, köşeli parantezle; okunmaz, tonu yönlendirir)

| Etiket | Nerede |
|---|---|
| `[curious]` | Kanca sorusu, "Peki ... mı?" |
| `[exasperated]` | "Aynı stüdyo! Aynı ışık!" gibi bıkkın sayım |
| `[firmly]` | "Hayır!", "Yok!" |
| `[excited]` | Vaat ve kanıt cümleleri, "Hem de bedava!" |
| `[playful]` | Absürt mekân cümleleri |
| `[confident]` | Açıklama, "Gerisini ... hallediyor." |
| `[whispers]` | Twist itirafı: "Aslında... ben de yokum." |
| `[warmly]` | Kapanış |
| `[amused]` | Gülümseyen ton |

⛔ **`[laughs]` kullanma.** Gülme, konuşan avatarda ağzı aşırı açar ve dişli sırıtma üretir. Yerine `[amused]`.

Örnek satır:
`[playful] Çamaşır makinesinin içine mi? [excited] Olur!`

### Alım seçimi (dinleyemiyorsan ölç)
- Süre: aynı satırın daha kısa alımı genelde daha tempolu.
- İç sessizlik: 0,4 sn'yi aşan anlamsız duraklama varsa ele.
- Dinamik aralık (LRA): heyecanlı satırda yüksek olan, sakin satırda düşük olan.
Kullanıcıya iki alımı birleştirilmiş halde dinlet ("A dosyası", "B dosyası"), satır satır karışım öner.

### Kelime zamanları
ElevenLabs `/with-timestamps` karakter zamanı verir; etiket karakterlerini atlayarak kelimelere çevir. Bu zamanlar altyazının ve yazı katmanının tek kaynağıdır.
