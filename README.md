# AI Video Fabrikası

Tek bir fotoğrafından ve kendi sesinden, **hiç kamera kullanmadan**, her sahnesi farklı ve absürt bir mekânda geçen (çamaşır makinesinin içi, buzdolabı, arı kovanı, akvaryum, uzay...) konuşan bir Reels/Shorts videosu üretmen için bir Claude skill'i.

Skill seni önce sorularla tanır (amaç, ton, fotoğraf, ses, hangi araçların var), sonra HeyGen, ElevenLabs ve HyperFrames için gerçek üretimde test edilmiş promptlarla adım adım ilerletir.

## ⬇️ İndir

**[ai-video-fabrikasi.zip](https://github.com/rockarge/ai-video-fabrikasi/releases/latest/download/ai-video-fabrikasi.zip)**

> Linki **bilgisayardan** aç. Skill, Claude'a bilgisayardan yükleniyor.

## Claude'a yükleme (4 adım)

1. Claude'da **Ayarlar > Yetenekler (Capabilities)** bölümünde **"Kod çalıştırma ve dosya oluşturma"** açık olsun.
2. **[claude.ai/customize/skills](https://claude.ai/customize/skills)** sayfasını aç.
3. **+** > **Create skill** > **Upload a skill** ile indirdiğin zip'i yükle. Listede açık olduğundan emin ol.
4. Yeni bir sohbet aç ve yaz: **"AI video fabrikasını başlat."**

Önerilen: Claude'da **HeyGen bağlayıcısını** (connector) bağla. Varsa HyperFrames bağlayıcısını da ekle.

## Claude Code ile

```bash
npx skills add rockarge/ai-video-fabrikasi
```
Tam hat için `ffmpeg` kurulu olsun; yazı katmanı için `npx skills add heygen-com/hyperframes`.

## Ne lazım

- HeyGen hesabı (konuşan klipler kredi harcar; skill önce tek sahnede dener, sonra devam eder)
- Yüzünün net, ağzının kapalı olduğu bir fotoğraf
- Kendi sesin için 2-3 dakikalık sessiz bir oda (opsiyonel; hazır bir ses de olur)

## İçinde ne var

| Bölüm | Konu |
|---|---|
| `SKILL.md` | Tanışma soruları, iki hat (sohbet / tam), üretim sırası, en sık 5 hata |
| `references/01-senaryo.md` | Kanca, soru-cevap ritmi, twist, kapanış |
| `references/02-ses.md` | Ses kaydı rehberi, okuma metni şablonu, ses klonu, duygu etiketleri |
| `references/03-sahne-gorselleri.md` | "Nesnenin içinden bakış" konsepti, kimlik kilidi, hazır görsel promptları |
| `references/04-heygen-avatar.md` | Avatar IV + dudak senkronu ile doğal ağız, geçiş klipleri |
| `references/05-hyperframes.md` | Yazı katmanı, prompt anatomisi, altyazı modeli, Türkçe karakter kontrolü |
| `references/06-kurgu-ve-teslim.md` | Müzik, ses seviyesi, hızlandırılmış sürüm, teslim kontrol listesi |

## Lisans

MIT. Kullan, değiştir, paylaş; kaynak olarak bu depoyu belirt.
