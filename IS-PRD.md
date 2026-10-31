# İş PRD'si — Kişiye Özel Gezi Sitesi Hizmeti (çalışma adı: "Gezi Kitapçığı")

> Sürüm 0.2 · 1 Kasım 2026 · Hazırlayan: Veli Öztürk
> Teknik temel: Japonya 2026 sitesinin teknik PRD'si (ayrı, özel depoda). Bu belge yalnız **iş tarafını** ele alır.
> İşaretler: **[tahmin]** = doğrulanmamış varsayım · **[kaynak]** = bağlantısı verilen veri · **[karar]** = Veli'nin vermesi gereken karar.

---

## 0. Tek paragrafta

Japonya'ya (sonra Kore'ye) giden, alışveriş ağırlıklı Türk çiftlere/arkadaş gruplarına, gezi başına bir kez kurulan, telefonda internetsiz çalışan, iki kişinin ortak kullandığı özel bir gezi sitesi (PWA) satmak. Bu ürünü farklı kılan beş şey var: kullanıcının Instagram'da kaydettiği önerileri plana çevirmek, Türkiye fiyatıyla kıyaslı alışveriş listesi, iki kişilik ortak liste ve harcama, Telegram'dan sabah/akşam özeti ile deprem/tren uyarıları, internetsiz çalışma. Uygulama mağazası yok. Önce 3–5 tanıdıkla elle kurulup ölçülecek. İşin kendini taşıyıp taşımayacağına kurulum saati ve ödeme isteği karar verecek.

### 0.1 Son durum (1 Kasım 2026) — referans sitede neler var, ne öğretti

Referans site 25–31 Ekim arasında 6 aktif günde, 109 commit ile kuruldu. 119 Instagram gönderisi işlendi (sesli incelemeler dahil). 27 Ekim'den sonra eklenenler ve iş açısından anlamları:

| Eklenen | İş açısından anlamı |
|---|---|
| **Telegram'dan soru sorma** (`/jp`): bot, sitenin bilgi paketinden (bölüm, gün, öneri, hatırlatma; tamamlananlar işaretli) yanıt veriyor | Yeni ayırt edici özellik: "gezinin asistanı". Standart pakete girer |
| **Birden çok alıcı**: bildirimler iki kişiye birden gidiyor | Ortak gezi vaadini tamamlıyor; §10'daki bot sorusunu kolaylaştırıyor |
| **Akşam "yarının işleri"** (gezi öncesi TR 20.00, gezide gün sonu) | Hatırlatma sisteminin en çok değer üreten parçası olabilir; pilotta ölçülmeli |
| **Yedekli hatırlatmalar** (A/B/C planı; ana iş tiklenince yedekler kalkıyor; ör. otobüs bileti) | Bilet/rezervasyon riskini azaltır; sorumluluk riskine (R4) karşı iyi bir önlem |
| **Yolculuk lojistiği**: eSIM karşılaştırması (doğrulanmış fiyatlarla 10+ seçenek), havalimanı otoparkı, havalimanı oteli, ilaç sınırları, şarj/priz, powerbank kuralı, uzun uçuş çantası, valiz kargosu (Yamato ücretleri), drone bataryası | İçeriğin büyük kısmı **kişiden bağımsız** → içerik havuzuna girer, sonraki gezilerde yeniden kullanılır (§6.4 hedefini destekler). Ama kapsamı da genişletiyor (R11) |
| **Otel kararı kullanıcıda kaldı**; otel adayları tablosu kaldırıldı | "Otel önerisi yok" MVP kararını doğruluyor |
| **Ana ekran uygulamasında giriş sorunu** (iOS'ta ana ekran uygulamasının ayrı çerez kutusu → bağlantıyı yapıştırma formu eklendi) | Yeni müşteride kurulum sürtünmesi; teslim adımlarına "ana ekran testi" girmeli (R12) |
| **Masaüstü genel arama**, sekme ikonu | Gezi öncesi planlama bilgisayarda da yapılıyor; yalnız mobil varsayımı gevşedi |

---

## 1. Problem ve değer önerisi

### 1.1 Problem
- Japonya'ya ilk kez giden Türk gezgin bilgiyi **dağınık** topluyor: Instagram kayıtları, YouTube, ekşi/forum, arkadaş WhatsApp mesajları, Google Maps yıldızları.
- Bilgi **plana dönüşmüyor**: hangi gün hangi semtte ne alınacak, nerede ne kapalı, hangi restoran rezervasyon istiyor belli değil.
- Alışverişte "**Türkiye'den ucuz mu?**" sorusu her ürün için ayrı ayrı araştırılıyor. Tax-free kuralları 2026'da değişiyor (çıkışta iade usulü).
- İki kişi **ayrı uygulamalar** kullanıyor: liste birinde, harcama ötekinde (ya da Excel'de).
- Gezide internet/roaming kesintisi, deprem ve tren aksaması gibi **yerel riskler** var ve Türkçe takip edilemiyor.

### 1.2 Değer önerisi
"Gezinizin kendi sitesi: kaydettiğiniz her şey güne, semte ve saate yerleşmiş; ne alacağınız, Türkiye'ye göre ne kadar kazandığınız ve ikinizin harcaması tek yerde. İnternet olmasa da çalışır, önemli bir şey olursa Telegram'dan haber verir."

### 1.3 Rakiplerden ayıran özellikler

| Özellik | Neden önemli | Rakiplerde durum |
|---|---|---|
| Instagram kayıtlarını plana çevirme (kullanıcının paylaştığı bağlantı/metinden) | Türk gezgin araştırmayı Instagram'da yapıyor | Yok. Wanderlog'a elle yer eklenir |
| Türkiye fiyatıyla kıyaslı alışveriş + tax-free | Japonya gezisinin ana nedenlerinden biri alışveriş | Yok (genel planlayıcılar fiyat kıyası yapmaz) |
| İki kişilik ortak liste/tik/harcama | Çift/arkadaş gezisi | Wanderlog'da ortak plan ve harcama var; TL ve tax-free fişi yok |
| Telegram sabah/akşam özeti, yarının işleri, deprem/tren uyarısı (iki kişiye birden) | Türkçe ve proaktif | TripIt Pro uçuş uyarısı veriyor; yerel afet/tren uyarısı yok |
| Telegram'dan gezi hakkında soru sorma | "Bugün nerede ne alıyorduk?" sorusuna sitenin kendi bilgisinden yanıt | Genel sohbet botları gezinin kendi planını bilmez |
| Yolculuk lojistiği (eSIM, otopark, ilaç, şarj, valiz kargosu) doğrulanmış fiyatla | Gezi öncesi en çok zaman alan küçük kararlar | Dağınık blog/Instagram içerikleri |
| İnternetsiz çalışma | Roaming/eSIM kesintisi | Wanderlog'da Pro'da var; Google listeleri sınırlı |
| Kaynaklı ve tarihli bilgi (saat, kapalı gün, rezervasyon) | Yanlış bilgi gezi gününü bozar | Kullanıcı yorumlarına dayalı, tarih yok |

---

## 2. Hedef kitle ve persona

### 2.1 Aşamalar
1. **Aşama 1 — Japonya:** Türkiye'den Japonya'ya giden, alışveriş ağırlıklı, 2 kişilik (çift/arkadaş) gruplar; 7–16 gün; ilk ya da ikinci Japonya gezisi.
2. **Aşama 2 — Kore:** Aynı kitle (K-beauty, moda, elektronik alışverişi). Japonya modülleri kanıtlandıktan sonra.

### 2.2 Pazar büyüklüğü

| Gösterge | Değer | Durum |
|---|---|---|
| Türkiye'den Japonya'ya ziyaretçi, 2025 | ~107.800 (+%73,6) | [kaynak: FTN News, JNTO verisi](https://ftnnews.com/?p=68720) |
| Türkiye'den Japonya'ya, Oca–Eyl 2025 | +%76,8 artış; TÜRSAB'a göre ~70 bin | [kaynak: Türkiye Today](https://www.turkiyetoday.com/business/visa-free-access-direct-flights-help-drive-turkish-surge-in-travel-to-japan-3211231) |
| 2024 tabanı | ~62 bin | [tahmin] 2025 rakamı ve artış oranından geri hesap; resmî JNTO 2024 değeri [statistics.jnto.go.jp](https://statistics.jnto.go.jp) üzerinden doğrulanmalı |
| Büyüme nedeni | ANA'nın Şubat 2025'te açtığı Haneda–İstanbul direkt hattı, Expo 2025 | [kaynak: Türkiye Today](https://www.turkiyetoday.com/business/visa-free-access-direct-flights-help-drive-turkish-surge-in-travel-to-japan-3211231) |
| Türkiye'den Güney Kore'ye ziyaretçi | **Bulunamadı.** Kore Turizm Örgütü (KTO) verisi aramada çıkmadı; vize muafiyeti 1 Nisan 2022'den beri var | [tahmin] 30–60 bin/yıl; KTO yıllık turizm istatistikleri (kto.visitkorea.or.kr) ya da Kore Adalet Bakanlığı giriş verisi üzerinden doğrulanmalı |

**Ulaşılabilir pazar (Japonya) [tahmin]:**

| Adım | Varsayım | Sonuç |
|---|---|---|
| Ziyaretçi (2025) | 107.800 kişi | 107.800 |
| İş/aile ziyareti değil, bireysel turist (tur paketi dışı) | %50 [tahmin] | ~54.000 kişi |
| 2 kişilik gruplar | ÷ 2 | ~27.000 gezi |
| Alışveriş ağırlıklı + dijital planlayan | %30 [tahmin] | ~8.000 gezi/yıl |
| İlk 2 yılda ulaşılabilir pay | %1–3 [tahmin] | **80–240 gezi/yıl** |

Sonuç: bu tek başına küçük bir **yan gelir/butik hizmet** pazarı, büyük bir girişim pazarı değil. Ölçek ancak (a) Kore ve başka ülkeler, (b) kurulumun büyük ölçüde otomatikleşmesi ya da (c) acente/rehber ortaklığıyla (B2B) gelir.

### 2.3 Persona

**Persona A — "Alışverişçi çift" (birincil)**
- Ece (31) ve Mert (33), İstanbul, beyaz yaka; 12 günlük Kasım/Nisan gezisi; bütçe 250–400 bin TL [tahmin].
- Instagram'da 100+ Japonya gönderisi kaydetmiş; kamera, kozmetik, bıçak, Uniqlo/GU, eczane ürünleri alacak.
- Acı noktaları: "Hangisi gerçekten ucuz?", "Kaydettiklerim hangi semtte?", "Harcamayı kim tutacak?"
- Ödeme isteği: Gezi bütçesinin %1–2'si; "rehberli tur almıyoruz ama biri planlasın" diyor.

**Persona B — "İki arkadaş, ilk uzak gezi" (ikincil)**
- 25–30 yaş, bütçe hassas; anime/Akihabara, ikinci el elektronik ve kamera.
- Ortak harcama bölüşümü ve internetsiz harita onlar için daha önemli; ödeme isteği daha düşük.

**Persona C — "Rehber/acente" (B2B, sonraki aşama)**
- Küçük butik acente ya da Instagram'da Japonya içeriği üreten kişi; müşterisine marka adıyla site vermek istiyor.

---

## 3. Rakip analizi

| Rakip | Ne yapıyor | Fiyat | Eksikleri (bu kitle için) |
|---|---|---|---|
| **Wanderlog** | Ortak gezi planı, harita, bütçe/harcama, yer önerileri | Ücretsiz; Pro ~39,99 $/yıl (çevrimdışı, PDF) [kaynak: [Pilot karşılaştırması](https://www.pilotplans.com/compare/wanderlog-alternative-feature-comparison), resmî sayfadan doğrulanmalı] | Planı kullanıcı kendi kurar; Instagram→plan yok; TR fiyat kıyası ve tax-free yok; Türkçe içerik zayıf |
| **TripIt** | E-postadaki rezervasyonlardan yol planı; Pro'da uçuş uyarıları | Ücretsiz; Pro 49 $/yıl [kaynak: [TripIt fiyatlar](https://www.tripit.com/uhp/pricing)] | Lojistik odaklı; ne yapılacağını/alınacağını söylemez; yerel afet/tren uyarısı yok |
| **Google Maps listeleri / Google Travel** | Yer kaydetme, paylaşılan listeler, çevrimdışı harita | Ücretsiz | Gün/saat planı yok, açık saat çakışması kontrolü yok, alışveriş/harcama yok |
| **Polarsteps** | Rota takibi, gezi günlüğü, basılı gezi kitabı | Uygulama ücretsiz; basılı kitap ~30–116 € [kaynak: [Wanderlog incelemesi](https://wanderlog.com/blog/?p=695), [Pilot incelemesi](https://www.pilotplans.com/blog/polarsteps-review)] | Gezi sonrası anı odaklı; planlama/alışveriş yok |
| **Notion/Excel şablonları** | Hazır gezi şablonu, elle doldurma | Ücretsiz–birkaç yüz TL [tahmin] | Tamamen elle; mobilde zayıf; uyarı/bildirim yok |
| **Seyahat acenteleri (paket tur)** | Uçak+otel+rehberli program | Kişi başı ~2.500–4.500 € [tahmin] | Esnek değil; alışveriş zamanı az; bireysel gezgine pahalı |
| **Özel rehber / "gezi planlama danışmanı"** (Instagram hesapları) | Kişiye özel PDF/WhatsApp planı | 2.000–10.000 TL [tahmin] | Statik PDF; ortak liste, harcama, uyarı yok; güncellenmez |
| **ChatGPT/Claude ile kendi planı** | Ücretsiz/abonelikle sohbetten plan | 0–20 $/ay | Doğrulanmamış bilgi; site, ortak kullanım, bildirim yok; kurulum için teknik bilgi gerekir |

**Konum:** "Danışmanın kişiye özel planı" ile "uygulamanın ortak kullanımı ve uyarıları" arasında. En yakın tehdit: Wanderlog'un yapay zekâ özellikleri ve kullanıcının kendi yapay zekâ asistanıyla planı kurması. Savunma: Türkçe + TR fiyat kıyası + doğrulanmış ve tarihli bilgi + hazır uyarı altyapısı.

---

## 4. Ürün biçimi

### 4.1 İlk biçim: gezi başına kurulan kişisel PWA (hizmet)
- Her gezi için ayrı, özel bağlantıyla korunan site (`<gezi>.pages.dev`, ileride kendi alan adının alt alan adı).
- Ana ekrana eklenir, internetsiz çalışır, iki telefon ortak veri kullanır (teknik PRD §5, §8).
- Telegram botu: müşteri kendi botunu açar **ya da** hizmetin ortak botu kullanılır [karar] (ortak bot kurulumu kolaylaştırır ama bot token hizmet sahibinde kalır, KVKK yükü artar). Bildirim iki kişiye birden gider; bot `/jp` benzeri bir komutla gezinin bilgi paketinden soru yanıtlar.
- Teslim: gezi −21 gün ilk sürüm, −5 gün bilgi tazeleme, gezi bitiminden 30 gün sonra salt-okunur arşiv (günlük + harcama raporu indirilebilir).

**Neden mağaza uygulaması değil:**
- Uygulama mağazası onayı, iOS/Android ayrı kod ve hesap ücretleri (Apple 99 $/yıl) gerekir; talep kanıtlanmadan bu maliyete girmek erken.
- Değer **içerikte** (araştırılmış plan); kabuk ikincil. PWA bu kabuğu yeterince karşılıyor.
- Gezi başına özelleştirme (ülke modülleri, kişiye özel bölümler) statik üretimle daha ucuz.

### 4.2 Native uygulamaya geçiş koşulları (hepsi birlikte)
1. Yılda **≥ 150 ücretli gezi** ya da ≥ 3 ülke modülü canlı.
2. Kurulumun **≥ %70'i** self-servis (kullanıcı formu → otomatik iskelet) yapılabiliyor.
3. PWA'nın açıkça yetmediği kanıtlanmış ihtiyaçlar: iOS'ta güvenilir anlık bildirim (Telegram dışında), arka planda konum, Apple Watch, mağazada keşfedilme.
4. Tekrar kullanım (aynı kullanıcının 2. gezisi) **≥ %25** — abonelik modeli düşünülebiliyorsa.

Ara adım: native yerine **tek çok-kiracılı web uygulaması** (tüm geziler tek kod, tek Worker, gezi id ile ayrılmış veri). Bu adım, gezi sayısı ~10'u geçince gerekir (bkz. §6.3).

---

## 5. Fiyatlandırma

### 5.1 Seçenekler

| Paket | İçerik | Önerilen fiyat [tahmin] | Hedef |
|---|---|---|---|
| **Temel** | Program + harita + pratik/acil + internetsiz + ortak tik; Instagram'dan en çok 30 gönderi; Telegram yok | 3.500 TL | Persona B, fiyat duyarlı |
| **Standart** (ana ürün) | Temel + alışveriş listesi ve TR fiyat kıyası (≤ 40 ürün) + harcama/tax-free + Telegram sabah/akşam/yarının işleri (iki kişiye) + Telegram'dan soru sorma + deprem/tren uyarısı + yolculuk lojistiği (eSIM, ilaç, şarj, valiz kargosu; havuzdan) + −5 gün tazeleme | 7.500 TL | Persona A |
| **Kişisel** | Standart + sınırsız Instagram (≤ 150) + gezi sırasında 3 kez "plan değişikliği" (ör. yağmur, kapanış) + 30 dk görüntülü ön görüşme | 13.000 TL | Bütçesi yüksek çift |
| **Ek: ikinci ülke/şehir eklentisi** | Aynı gezide Kore aktarması vb. | +2.500 TL | — |
| **Tanıdık deneme fiyatı** | Standart, karşılığında görüşme + ölçüm izni | 0 TL ya da "beğenirsen öde" (önerilen: 3.000 TL) | §8 pilotu |

### 5.2 Gerekçe
- **Gezi başı tek ödeme**, çünkü ihtiyaç gezi başına doğuyor ve tekrar sıklığı düşük (yılda 0–1 uzak gezi). Abonelik bu kitlede satılmaz.
- **Değere göre çapa:** Çift için Japonya gezisi ~250–400 bin TL [tahmin]; Standart paket bunun ~%2–3'ü. Tek bir doğru alışveriş kararı (ör. kamera/lenste %20–40 fark) ücreti karşılayabiliyor; bu satış mesajı olur.
- **Rakip çapası:** Uygulamalar yıllık 40–50 $ (~1.700–2.300 TL [tahmin, 1 $ ≈ 45 TL varsayımı]) ama planı kullanıcı kurar. Danışman PDF'leri 2–10 bin TL [tahmin]. "Danışman + uygulama" konumu 7.500 TL'yi savunuyor.
- **Maliyet tabanı:** §6'ya göre insan saati baskın maliyet; Temel paketin altındaki fiyat insan saatini karşılamaz.
- **Ödeme zamanı:** %50 sipariş, %50 ilk sürüm tesliminde (gezi −21 gün). İade: ilk sürümden önce tam iade, sonra yok [karar].

---

## 6. Birim maliyet

### 6.1 Varsayımlar
- Kurulum yapay zekâ asistanıyla (Claude Code) yapılır; araştırma alt ajanlarla paralel.
- Model fiyatları (Anthropic API, Ekim 2026): Opus 5.5 giriş 4 $/milyon token, çıkış 20 $/milyon, önbellekten okuma 0,20 $/milyon; Sonnet 5.5 2 $ / 10 $; Haiku 5.5 0,10 $ / 0,50 $ [kaynak: Anthropic API fiyat tablosu, `claude-api` başvuru belgesi, 6 Ekim 2026 önbelleği].
- 1 $ = 45 TL [tahmin, ödeme gününde güncellenmeli].
- Japonya sitesi bir kez kurulmuş durumda; yeni Japonya gezisi **şablon + yeni içerik**tir (kod çoğunlukla yeniden kullanılır).
- İnsan saat değeri: 750 TL/saat [tahmin; Veli'nin fırsat maliyeti olarak karar verilmeli].

### 6.2 Yapay zekâ maliyeti (gezi başı, Standart paket) [tahmin]

| İş | Token (giriş / çıkış) | Not |
|---|---|---|
| İskelet + veri dosyaları (trip, travel, plan) | 3 M / 0,3 M | |
| Araştırma: saat, kapalı gün, rezervasyon, koordinat (40–80 durak) | 8 M / 0,6 M | Alt ajanlar; Sonnet ile yapılabilir |
| Alışveriş + TR fiyat kıyası (≤ 40 ürün) | 5 M / 0,3 M | Web sayfaları uzun → giriş baskın |
| Instagram (≤ 60 gönderi; kullanıcının verdiği bağlantı/metin/ekran görüntüsü) | 4 M / 0,2 M | Görsel varsa giriş artar |
| Test, düzeltme, yayın, −5 gün tazeleme | 4 M / 0,3 M | |
| **Toplam** | **~24 M / ~1,7 M** | Girişin ~%70'i önbellekten okunur varsayımı |

| Senaryo | Hesap | Gezi başı |
|---|---|---|
| Tümü Opus 5.5 | (7,2 M × 4 $ + 16,8 M × 0,20 $) + 1,7 M × 20 $ = 28,8 + 3,4 + 34 | **~66 $ ≈ 3.000 TL** |
| Karma (araştırma Sonnet 5.5, kurgu/kod Opus 5.5) | ~%40 daha ucuz | **~40 $ ≈ 1.800 TL** |
| Kötü durum (çok deneme, uzun Instagram) | ×2 | ~130 $ ≈ 5.900 TL |

Not: Claude abonelik planıyla (Max) yapılırsa marjinal maliyet düşük görünür ama kullanım sınırları ayda kaç gezi kurulabileceğini belirler. Ayrıca abonelik koşullarının ücretli müşteri işine uygunluğu kontrol edilmeli [karar/açık soru]. Hesaplar API fiyatıyla yapıldı.

### 6.3 Cloudflare maliyeti

| Kaynak | Ücretsiz katman sınırı | Bir gezi ne kullanır [tahmin] | Sonuç |
|---|---|---|---|
| KV yazma | **1.000 yazma/gün, hesap başına**; okuma 100.000/gün; aynı anahtara 1 yazma/sn [kaynak: [KV limits](https://developers.cloudflare.com/kv/platform/limits)] | Gezi günü: tik + harcama + günlük + uyarı kaydı ≈ 100–250 yazma | Aynı anda **en çok 3–4 aktif gezi** bir ücretsiz hesaba sığar |
| Workers istek | 100.000/gün; istek başına 10 ms CPU [kaynak: [Workers limits](https://developers.cloudflare.com/workers/platform/limits)] | ~1–3 bin/gün | Sorun değil |
| Cron tetikleyici | **Hesap başına 5** (ücretli planda 250) [kaynak: [Workers limits](https://developers.cloudflare.com/workers/platform/limits)] | Bir gezi 3–4 cron kullanıyor (sabah, akşam, gezi öncesi, 10 dk uyarı) | Ücretsiz hesapta **yalnız 1 gezinin bildirimi** çalışır |
| Pages | Statik yayın | — | Sorun değil |

**Karar:** Ürünleşince iki yol var:
1. Her müşteri **kendi** Cloudflare hesabını açar (ücretsiz). Hizmetin maliyeti 0 olur, kurulum zorlaşır, müşteri verisi müşteride kalır (KVKK açısından iyi).
2. Hizmet sahibi **Workers Paid** planına geçer (~5 $/ay [tahmin, [Workers pricing](https://developers.cloudflare.com/workers/platform/pricing/) üzerinden doğrulanmalı]) ve tüm gezileri **tek Worker + tek cron** çalıştırır, gezi id ile ayırır. 10+ gezide gezi başı < 1 $.

Pilot için 1. yol önerilir; 10 geziyi geçince 2. yol.

### 6.4 İnsan süresi (gezi başı, Standart) [tahmin]

| İş | Pilot (ilk 3 gezi) | Hedef (10. gezi sonrası) |
|---|---|---|
| Ön görüşme + bilgi toplama (teknik PRD §3) | 1,5 sa | 0,5 sa (form) |
| Yapay zekâ kurulumunu yönetme | 8 sa | 3 sa |
| İnsan doğrulama (saat, fiyat, rezervasyon, rota çakışması örneklemi) | 5 sa | 2,5 sa |
| Telefon testi + teslim | 1,5 sa | 0,5 sa |
| −5 gün tazeleme + gezide destek | 2 sa | 1 sa |
| **Toplam** | **18 sa** | **7,5 sa** |

**Referans siteden gerçek veri (0. pilot):** Kurulum 25–31 Ekim'de 6 aktif günde 109 commit sürdü ve gezi yaklaştıkça iş artmaya devam etti (31 Ekim'de tek günde 25 commit). İnsan saati ölçülmedi; kabaca 25–40 saat [tahmin]. Bu tablodaki "pilot 18 sa" varsayımı ancak lojistik içerik havuzdan gelirse ve kapsam sınırlanırsa tutar (R11).

### 6.5 Gezi başı marj (Standart, 7.500 TL)

| Senaryo | Gelir | Yapay zekâ | Cloudflare | Ödeme/vergi kesintisi (%20 [tahmin]) | İnsan (750 TL/sa) | **Kâr** | Marj |
|---|---|---|---|---|---|---|---|
| Pilot (18 sa, tümü Opus) | 7.500 | 3.000 | 0 | 1.500 | 13.500 | **−10.500** | −%140 |
| Pilot, insan saati sayılmazsa | 7.500 | 3.000 | 0 | 1.500 | — | 3.000 | %40 |
| Olgun (7,5 sa, karma model) | 7.500 | 1.800 | 50 | 1.500 | 5.625 | **−1.475** | −%20 |
| Olgun, Kişisel paket (13.000 TL, 10 sa) | 13.000 | 2.500 | 50 | 2.600 | 7.500 | **350** | %3 |
| Hedef (4 sa, karma, Standart 9.000 TL) | 9.000 | 1.500 | 50 | 1.800 | 3.000 | **2.650** | %29 |

**Sonuç:** Mevcut haliyle hizmet, insan saati değerlenince **zarar ediyor**. Kârlılık için üç koşuldan en az ikisi gerekli: (a) gezi başı insan süresi ≤ 4 saat, (b) fiyat ≥ 9.000 TL, (c) yeniden kullanılabilir içerik havuzu (aynı şehirde ikinci gezi için saat/fiyat verisinin %50+'sı hazır). Pilotun asıl amacı (a) ve (b)'yi ölçmek.

---

## 7. Riskler ve önlemler

| # | Risk | Etki | Olasılık | Önlem |
|---|---|---|---|---|
| R1 | **Bilgi doğruluğu ölçeklenmez**: her yer için saat/fiyat/rezervasyon kontrolü insan saati ister | Yüksek | Yüksek | Paylaşılan, tarihli **içerik havuzu** (şehir başına yer/saat/fiyat; 60 günden eski kayıt yeniden kontrol); yalnız gezi günü planına girenler doğrulanır; doğrulanamayan "tahmini" etiketi; örneklemeli insan kontrolü (her gezide 20 rastgele kayıt) |
| R2 | **Her ülke ayrı modül** (afet, tren, tax-free, dil, adres) | Yüksek | Kesin | 2027'ye kadar yalnız Japonya; Kore ancak Japonya'da ≥ 10 ücretli gezi sonrası; modül arayüzü teknik PRD §13'teki tabloya bağlı; modülü olmayan ülkede o özellik kapalı ve satış sayfasında yazılı |
| R3 | **Instagram verisini sunucudan çekmek** kullanım şartlarına aykırı (yetkisiz otomatik toplama yasak; Meta dava açıyor) | Yüksek (hesap kapanması, hukuki) | Orta | Yalnız **kullanıcının kendisinin verdiği** bağlantı, açıklama metni, ekran görüntüsü işlenir; sunucudan otomatik tarama, kullanıcı oturumuyla toplu indirme, başkasının hesabını izleme **yok**; gönderi içeriği saklanmaz, yalnız özet + bağlantı [kaynak: [Instagram yardım](https://help.instagram.com/740480200552298), [Meta v. Social Data Trading](https://www.jurist.org/news/wp-content/uploads/sites/4/2021/12/Meta-Platforms-Inc.-v.-Social-Data-Trading-Ltd.pdf)] |
| R4 | **Yasal sorumluluk**: yanlış saat, kapalı yer, kaçan tren/rezervasyon, yanlış tax-free bilgisi | Orta | Orta | Sözleşmede "bilgi amaçlıdır, resmî kaynak esastır" ve sorumluluk üst sınırı = ödenen ücret; her kayıtta kaynak + kontrol tarihi; rezervasyon/bilet yapılmaz; kritik bilgilerde (uçuş, tax-free, acil) resmî kaynağa bağlantı; mesleki sorumluluk sigortası araştırılır [karar]; bir avukata sözleşme kontrolü |
| R5 | **Kişisel veri (KVKK)**: ad, tarih, otel adresi, harcama, fiş fotoğrafı, günlük; sunucular yurt dışında (Cloudflare) | Yüksek | Kesin | Veri en aza: PNR/pasaport/kart no asla (teknik PRD §3.3); aydınlatma metni + açık rıza; yurt dışına aktarım için 6698 s. Kanun md. 9 (2024 değişikliği) kapsamında standart sözleşme ve Kurul'a bildirim gerekip gerekmediği hukukçuya sorulmalı [tahmin, doğrulanmalı]; tercihen müşterinin **kendi** Cloudflare hesabı; gezi +30 gün sonra veri silme/teslim; VERBİS yükümlülüğü kontrol |
| R6 | **Tekrar kullanım az**: müşteri yılda en çok 1 uzak gezi yapar | Yüksek (müşteri edinme maliyeti her seferinde) | Kesin | Gelir modelini tekrar satışa değil **tavsiyeye** dayandır (gezi sonrası tavsiye indirimi); B2B (acente/rehber markalı site); gezi sonrası "günlük kitabı" PDF/baskı ek ürünü |
| R7 | Yapay zekâ maliyeti/fiyatı değişir | Orta | Orta | Fiyatlamada yapay zekâ payını ≤ %25 tut; karma model; içerik havuzu ile tekrar araştırmayı azalt |
| R8 | Bağımlılık: Telegram, Cloudflare, Yahoo路線情報 sayfa yapısı, P2P地震情報 | Orta | Orta | Uyarı ayrıştırıcıları testli (teknik PRD §11); kaynak bozulursa uyarı kapanır ve kullanıcıya "bu uyarı şu an çalışmıyor" denir; Telegram yoksa e-posta/yalnız site |
| R9 | Rakip (Wanderlog vb.) yapay zekâ ile benzer planı ücretsiz verir | Orta | Yüksek | Türkçe + TR fiyatı + doğrulanmış/tarihli bilgi + uyarılar; hız: pilotu 2026 kış/2027 bahar (kiraz) sezonuna yetiştir |
| R10 | Tek kişiye bağımlılık (Veli'nin zamanı) | Yüksek | Yüksek | Pilotta haftada en çok 1 gezi; kurulum adımlarını belgeleyip (teknik PRD §14) ikinci kişiye devredilebilir hale getir |
| R11 | **Kapsam kayması**: gezi yaklaştıkça her soru yeni bir bölüme dönüşüyor (referans sitede son haftada eSIM, otopark, ilaç, şarj, drone eklendi) | Yüksek (insan saati patlar) | Yüksek | Paket başına sabit kapsam listesi; ek istek = "plan değişikliği" hakkından düşer ya da ücretli; kişiden bağımsız lojistik içerik önce havuza yazılır, sonra siteye bağlanır |
| R12 | **Ana ekran kurulumu sürtünmesi**: iOS'ta ana ekrana eklenen uygulama ayrı çerez kutusu kullanıyor, özel bağlantı ilk açılışta tanınmayabiliyor | Orta (ilk izlenim) | Orta | Engel sayfasındaki "bağlantıyı yapıştır" formu; teslimde müşteriyle birlikte iki telefonda ana ekran testi; 1 sayfalık kurulum kılavuzu |

---

## 8. İlk deneme planı (pilot)

### 8.1 Kapsam
- **3–5 tanıdık**, gerçek ve tarihi belli Japonya gezisi (tercihen Aralık 2026–Nisan 2027).
- Elle kurulum, mevcut Japonya şablonundan; her gezi ayrı Cloudflare projesi (müşterinin ya da Veli'nin hesabı, cron sınırına dikkat).
- Ücret: "beğenirsen öde" ya da 3.000 TL deneme fiyatı [karar]; ödeme isteğini ölçmek için gezi sonrasında Standart fiyat da sorulur.

### 8.2 Ölçülecekler

| Ölçü | Nasıl | Başarı eşiği |
|---|---|---|
| Kurulum süresi (insan saati) | Kronometre, iş kalemine göre (§6.4 tablosu) | 3. gezide ≤ 10 sa; eğilim 4 saate doğru |
| Yapay zekâ maliyeti | API/abonelik kullanım raporu | Gezi başı ≤ 60 $ |
| Bilgi hatası | Kullanıcının bildirdiği + gezi sonrası örneklem (yanlış saat/kapalı yer/yanlış fiyat) | Gezi başı ≤ 2 hata, hiçbiri gezi gününü bozan türden değil |
| En çok kullanılan bölümler | Sayfa açılış sayacı (çerezsiz, sayfa başına toplam, KV'de; kişisel veri yok) + görüşme | İlk 3 bölüm belirlenir; kullanılmayan bölümler MVP'den çıkarılır |
| Gezide etkin kullanım | Gezi günlerinin kaçında site açıldı | ≥ %70 gün |
| Telegram yararlılığı | Görüşme: "mesajı okudun mu, işe yaradı mı"; en yararlı mesaj türü (sabah / yarının işleri / uyarı / soru-cevap) | ≥ 3/5 kişi "yararlı" |
| Telegram'dan soru sorma | Gezi başına soru sayısı (yalnız sayı, içerik saklanmaz) | Gezi başına ≥ 5 soru |
| Kapsam dışı istek | Teslimden sonra gelen ek bölüm istekleri ve süresi | Gezi başına ≤ 2 saat ek iş |
| Ödeme isteği | Gezi sonrası: "Bunu 7.500 TL'ye bir arkadaşına önerir misin / kendin tekrar alır mısın?" + Van Westendorp 4 soru | ≥ 3/5 kişi 7.500 TL'yi "makul" ya da "ucuz" der |
| Memnuniyet | 0–10 tavsiye puanı (NPS) | Ortalama ≥ 8; en az 2 gerçek tavsiye (yeni müşteri adayı) |

### 8.3 Karar kuralı (8. haftanın sonunda)
- **Devam (ücretli lansman):** Ödeme isteği + memnuniyet eşikleri tuttu ve 3. gezide kurulum ≤ 10 sa.
- **Pivot:** Memnuniyet yüksek ama kurulum > 12 sa → B2B (acente/rehbere araç olarak sat) ya da yalnız "Alışveriş + fiyat kıyası" modülüne daralt.
- **Dur:** Ödeme isteği < 3/5 ya da gezide kullanım < %50 → kişisel proje olarak bırak.

### 8.4 8 haftalık takvim (başlangıç: 2 Kasım 2026 varsayımı)

| Hafta | Tarih | İş |
|---|---|---|
| 1 | 2–8 Kas | Japonya sitesini şablona çevirme planı (kişisel bilgilerin ayrılması); ön görüşme formu; aydınlatma metni + basit hizmet sözleşmesi taslağı; 5–8 tanıdık adayına mesaj |
| 2 | 9–15 Kas | (Veli Japonya'da — kendi gezisi = **0. pilot**: kendi kullanım verisini topla, hataları not al) |
| 3 | 16–22 Kas | (Gezi sürüyor, 24 Kas dönüş) — günlük not: hangi bölüm, hangi bildirim işe yaradı |
| 4 | 23–29 Kas | Kendi gezisinin değerlendirmesi; şablonu temizle; 3–5 pilot katılımcıyı kesinleştir; Pilot 1 ön görüşme |
| 5 | 30 Kas–6 Ara | Pilot 1 kurulumu (kronometreli); Pilot 2 ön görüşme |
| 6 | 7–13 Ara | Pilot 1 teslim + telefon testi; Pilot 2 kurulumu; içerik havuzunun ilk sürümü (Pilot 1–2'nin ortak yerleri) |
| 7 | 14–20 Ara | Pilot 3 kurulumu; Pilot 2 teslim; ara ölçüm (kurulum saati eğilimi) |
| 8 | 21–27 Ara | Teslimler; gezisi bitenlerle görüşme; ödeme isteği anketi; **karar toplantısı** (§8.3) |

Not: Pilotların gezileri 8 haftanın dışına taşabilir (Ocak–Nisan); o durumda "gezide kullanım" ve "memnuniyet" ölçüleri gezi sonrasında tamamlanır ve karar ara verilerle verilir, nihai karar son pilot gezisinden sonra yenilenir.

---

## 9. MVP kapsamı

### 9.1 MVP'de olacaklar (pilot = Standart paket)
- Özel bağlantıyla korunan PWA, ana ekran ikonu, internetsiz çalışma.
- Ana sayfa (geri sayım, iki saat, sıradaki işler), Program (gün kartı, saatli duraklar, günün haritası, Google/Apple bağlantı), Harita (yakınımdakiler: açık/kapalı), Pratik + Acil.
- Alışveriş listesi: iki kişiye ayrı, TR fiyat kıyası ve değer rozeti (≤ 40 ürün), tax-free notu.
- Ortak tik + harcama (TL/JPY, kişi, tax-free fişi işareti, CSV).
- Instagram: kullanıcının verdiği bağlantı/metin/ekran görüntüsünden öneri çıkarma (≤ 60).
- Telegram (iki alıcı): gezide sabah + akşam özeti, yarının işleri, yedekli hatırlatmalar; deprem (şiddet eşiği) ve izlenen hat aksaması; gezinin bilgi paketinden soru-cevap.
- Yolculuk lojistiği: havuzdaki eSIM, ilaç, şarj, valiz kargosu rehberleri (kişiye göre yalnız seçim yapılır).
- −5 gün bilgi tazeleme.
- Aydınlatma metni, sözleşme, veri silme (gezi +30 gün).

### 9.2 MVP'de olmayacaklar
- Native uygulama, uygulama mağazası.
- Self-servis kayıt/ödeme sayfası (pilotta havale/elden).
- Rezervasyon ya da bilet satın alma, otel önerisi (kullanıcı otelini kendisi seçer).
- Instagram'dan otomatik toplama, kullanıcının oturumuyla tarama.
- Japonya dışı ülke, çok dillilik (yalnız Türkçe).
- Günlük fotoğrafları için büyük depolama, basılı kitap.
- 3+ kişilik gruplar (veri modeli iki kişi için).
- Çok-kiracılı tek uygulama (gezi başı ayrı proje yeterli).

### 9.3 Sonraki aşamalar

| Aşama | Ne zaman (koşul) | Ne |
|---|---|---|
| A1 — Ücretli lansman | Pilot "devam" kararı | Basit satış sayfası, ön görüşme formu, ödeme bağlantısı; Standart + Kişisel paket; Japonya içerik havuzu |
| A2 — Ölçek | ≥ 10 ücretli gezi | Çok-kiracılı tek uygulama + Workers Paid; form → otomatik iskelet; gezi başı insan süresi ≤ 4 sa |
| A3 — Kore | ≥ 20 Japonya gezisi ya da Kore'ye ≥ 5 ön talep | Kore modülleri (afet/tren/tax-free/dil); K-beauty fiyat kıyası |
| A4 — B2B | 2+ acente/rehber ilgisi | Markalı site, toplu fiyat |
| A5 — Native | §4.2 koşulları | Mağaza uygulaması ya da PWA sarmalayıcı |

---

## 10. Açık sorular / Veli'den alınacak kararlar

1. **[karar] Amaç:** Bu bir yan gelir mi, tam zamanlı iş adayı mı? (§2.2 pazar hesabı tek başına tam zamanlı işi taşımıyor.)
2. **[karar] Saat değeri:** Kendi saatinizi kaç TL sayıyoruz (marj tablosu 750 TL/sa varsaydı)?
3. **[karar] Pilot ücreti:** Ücretsiz, "beğenirsen öde" ya da 3.000 TL?
4. **[karar] Cloudflare hesabı:** Pilotta her müşteri kendi hesabını mı açacak (KVKK'ya daha uygun, kurulum zor), yoksa sizin hesabınız mı (cron sınırı 5 → aynı anda tek gezinin bildirimi)?
5. **[karar] Telegram botu:** Müşterinin kendi botu mu, ortak hizmet botu mu? (Çoklu alıcı ve soru-cevap artık çalışıyor; ortak botta soru-cevap için gezi ayrımı gerekir.)
6. **[açık] Yapay zekâ kullanımı:** Kurulumlar Claude aboneliğiyle mi API ile mi yapılacak? Aboneliğin ücretli müşteri işine uygunluğu ve kullanım sınırları kontrol edilmeli.
7. **[açık] Hukuk:** Şahıs şirketi/fatura, hizmet sözleşmesi, sorumluluk sınırı, KVKK yurt dışı aktarım ve VERBİS için bir avukat/mali müşavir görüşmesi ne zaman?
8. **[açık] Pilot adayları:** Önümüzdeki 6 ayda Japonya'ya gidecek 5–8 tanıdık var mı? Gezi tarihleri?
9. **[karar] Kendi gezisi (9–24 Kasım) 0. pilot olarak ölçülsün mü?** (Kullanım sayacı eklemek site deposunda değişiklik ister; ayrı iş olarak ele alınmalı.)
10. **[açık] Pazar verisi:** JNTO 2024 Türkiye rakamı ve Kore (KTO) Türkiye ziyaretçi sayısı resmî kaynaktan doğrulanacak.
11. **[karar] Marka/adı ve alan adı:** pages.dev mi, kendi alan adı mı?
12. **[karar] İçerik havuzunun sahipliği:** Müşteri gezilerinden çıkan doğrulanmış bilgiler (saat, fiyat) sonraki müşterilerde kullanılabilir mi? (Sözleşmeye yazılmalı; kişisel veri içermez.)
13. **[karar] Lojistik içerik havuzu:** Referans sitedeki eSIM, ilaç, şarj, valiz kargosu rehberleri şimdiden kişiden bağımsız bir havuza ayrılsın mı? (Fiyatların tarihi var; gezi başına tazeleme gerekir.)

---

## Kaynaklar
- FTN News — Turkish visitor numbers to Japan jump 73.6% in 2025, says JNTO: https://ftnnews.com/?p=68720
- Türkiye Today — Visa-free access, direct flights help drive Turkish surge in travel to Japan: https://www.turkiyetoday.com/business/visa-free-access-direct-flights-help-drive-turkish-surge-in-travel-to-japan-3211231
- JNTO aylık ziyaretçi bültenleri (ör. Ekim 2025): https://asset.japan.travel/image/upload/v1763626725/pdf/Number_of_visitor_arrivals_to_Japan_in_October_2025.pdf
- TripIt fiyatlar: https://www.tripit.com/uhp/pricing
- Pilot — Wanderlog karşılaştırması: https://www.pilotplans.com/compare/wanderlog-alternative-feature-comparison
- Wanderlog blog — Polarsteps incelemesi: https://wanderlog.com/blog/?p=695
- Pilot — Polarsteps incelemesi: https://www.pilotplans.com/blog/polarsteps-review
- Cloudflare KV limitleri: https://developers.cloudflare.com/kv/platform/limits
- Cloudflare Workers limitleri: https://developers.cloudflare.com/workers/platform/limits
- Cloudflare Workers fiyatlandırma: https://developers.cloudflare.com/workers/platform/pricing/
- Instagram yardım merkezi (veri kazıma): https://help.instagram.com/740480200552298
- Meta Platforms v. Social Data Trading (dava dilekçesi): https://www.jurist.org/news/wp-content/uploads/sites/4/2021/12/Meta-Platforms-Inc.-v.-Social-Data-Trading-Ltd.pdf
