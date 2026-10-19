# 3. Sahne görselleri

## Konsept: "nesnenin içinden bakış"

Her sahne, kamera bir nesnenin **içindeymiş** gibi kurulur ve kişi o nesnenin ağzından/kapağından içeri bakar: çamaşır makinesi kapağı, buzdolabı rafı, kahve fincanı, arı kovanı, akvaryum, projektör merceği, uzay gemisi lombozu. İzleyici her sahnede "bu nasıl çekildi?" diye durur. Kıyafet mekâna göre değişir (dalgıç, arıcı, astronot...).

## Kimlik kilidi

- Kullanıcının **kendi fotoğrafını referans olarak ver** (görsel modelin referans/kimlik girişi). Referans: yüz net, ağız kapalı, nötr ifade, düz ışık.
- Her prompt'a: "same person as the reference, same face, same hairline and beard" (sakal/saç gibi belirleyici özellikleri kullanıcıdan al).
- 9:16, 1080x1920 ya da daha yüksek. Konuşan avatar için yüz kadrajın **üst yarısında**, yüz genişliği kadraj genişliğinin en az 1/5'i.

## Konuşan sahne için zorunlu yüz kuralları

- **Ağız kapalı, dudaklar rahat, nötr ifade.** Gülümseyen kaynak görsel, konuşurken daha da sırıtır.
- Yüz kameraya dönük ya da en fazla 20-30 derece açılı; profil olmaz.
- Yüzün önünde nesne yok (el, cam yansıması, buhar yüzü kesmesin).
- Tek kişi. Arka planda yüz varsa (ekran duvarı vb.) küçük ve bulanık olsun.

## Prompt formülü

```
[KAMERA KONUMU: inside the X, looking out through its door/opening],
[KİŞİ: same person as the reference, wearing Y, leaning toward the lens],
calm neutral expression, lips closed and relaxed, looking straight into the lens,
[MEKÂN DETAYI: what is visible around the frame edges from inside the object],
[IŞIK: motivated light source of that object],
wide-angle lens slight distortion, shallow depth of field, cinematic color grade,
photorealistic, vertical 9:16, no text, no watermark
```

## Örnek promptlar (uyarla, kopyalama)

1. **Çamaşır makinesi:** inside a front-loading washing machine drum looking out through the round glass door, same person as the reference wearing a black diving suit with a snorkel mask pushed up on the forehead, leaning toward the door, calm neutral expression, lips closed, a yellow rubber duck floating on soapy water at the bottom of the frame, colorful laundry around the drum edge, laundromat with fluorescent ceiling lights behind him, fisheye distortion, cinematic, photorealistic, vertical 9:16, no text
2. **Buzdolabı:** inside an open refrigerator looking out between the shelves, same person as the reference in a navy three-piece suit and tie leaning into the fridge, neutral expression, lips closed, a cucumber and egg carton in the foreground glass shelf slightly out of focus, cool white fridge light on his face, warm kitchen behind, photorealistic, vertical 9:16, no text
3. **Arı kovanı:** inside a wooden beehive looking out through the opening, honeycomb walls on both sides, same person as the reference in a white beekeeper suit with the veil pulled back, neutral calm face, lips closed, a few bees in soft focus, golden daylight from behind, photorealistic, vertical 9:16, no text
4. **Akvaryum:** inside a home aquarium looking out through the glass, same person as the reference in a vintage white astronaut suit without helmet, leaning toward the tank, neutral expression, lips closed, aquarium plants and a small crab on white sand in the foreground, bubbles rising, cool blue light, photorealistic, vertical 9:16, no text
5. **Kahve fincanı:** looking up from inside a coffee cup, the round rim framing the shot, same person as the reference in a cream knit sweater looking down into the cup, neutral expression, lips closed, soft steam at the edges not covering the face, warm morning window light, photorealistic, vertical 9:16, no text
6. **Projektör:** inside a film projector looking out through the lens, light beam and dust particles, same person as the reference in a dark jacket illuminated by projected light patterns, neutral expression, lips closed, lens flare rings around the frame, cinematic, vertical 9:16, no text
7. **Uzay gemisi:** inside a retro spaceship cabin, round porthole with Earth and stars behind, same person as the reference in a rust-orange flight suit standing with hands behind his back, neutral calm expression, lips closed, brass pipes and warm practical lights, cinematic, vertical 9:16, no text

## Açılış ve "herkes aynı" sahneleri

- Kanca sahnesi: telefon ekranının içinden bakış (kişi parmağını ekrana uzatmış, kaydırıyor).
- "Herkes aynı" sahnesi: tepeden bakış, kişi yüzlerce aynı avatar videosunun oynadığı ekran duvarının önünde. Duvardaki yüzler küçük ve bulanık kalsın (yoksa konuşan avatar onları da oynatmaya çalışır).

## Kontrol (üretmeden önce)

- [ ] Ağız kapalı mı, ifade nötr mü
- [ ] Yüz net, önden, üst yarıda mı
- [ ] Kimlik referansla tutarlı mı (sakal, saç, yüz şekli)
- [ ] Görselde yazı/logo yok mu
- [ ] 9:16 mı
Kullanıcıya tüm sahneleri tek bir pano (grid) olarak göster, onay al.
