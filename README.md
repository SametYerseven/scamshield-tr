# ScamShield TR - Dolandırıcılık Kalkanı

Türkçe dolandırıcılık mesajlarını tespit eden sistem.
Sosyal Sorumluluk Dersi Projesi - Konu: Siber Güvenlik ve Blokzinciri Uygulamaları

## Problem

"Kargonuz teslim edilemedi", "hesabınız bloke oldu", "hakkınızda icra takibi başlatıldı" gibi sahte SMS ve WhatsApp mesajları her gün birçok kişiyi, özellikle yaşlıları dolandırıyor.

## Çözüm

Kullanıcı şüphelendiği mesajı sisteme yapıştırır. Sistem:

1. Metni analiz eder: Dolandırıcılık mı, hangi türden?
2. Mesajdaki linki kontrol eder: Sahte site mi?
3. Sonucu sade bir dille açıklar. Örnek: "Bu mesaj sahte kargo dolandırıcılığına benziyor. Linke tıklamayın."

```
Kullanıcı (Web / Telegram botu)
        |
   Backend API
        |
   +----+------------+
   |    |            |
 Metin  Link        Açıklama
 modeli analizi     üretimi
        |
 Sonuç + açıklama
```

## Mevcut Durum (19 Kasım)

Tamamlananlar:

- **Metin sınıflandırma modelinin ilk versiyonu:** [notebooks/01_baseline_model.ipynb](notebooks/01_baseline_model.ipynb)
  - Veri seti: Turkish SMS Collection, 4.751 mesaj (ayrıntı: [data/README.md](data/README.md))
  - Üç model karşılaştırıldı: Lojistik Regresyon, Naive Bayes, Doğrusal SVM
  - En iyi model Lojistik Regresyon: test setindeki 948 mesajın 947'sini doğru bildi (F1 = 0,999)
  - Önemli not: Veri setindeki spam mesajların çoğu reklam olduğu için bu sonuç gerçek dolandırıcılık mesajlarındaki başarıyı yansıtmıyor. Bu yüzden kendi dolandırıcılık veri setimizi toplayıp BERTurk modeline geçeceğiz.
- **Ara raporun model bölümleri yazıldı:** Yöntem, Mevcut İlerleme, Karşılaşılan Sorunlar ve Çözümler, Sonraki Adımlar, Kaynaklar. Belgenin linki WhatsApp grubunda paylaşıldı. Bu bölümler rapora olduğu gibi eklenebilir.

Ara rapor için kalanlar:

- Kapak (proje adı, takım üyeleri ve numaraları, takım lideri, tarih)
- Giriş, Amaç, Sosyal Katkı
- Benzer Çalışmalar
- Sistem Tasarımı (mimari diyagram) ve Kullanılan Teknolojiler
- Mevcut İlerleme: veri toplama ve arayüz taslağı kısmı
- Görev Dağılımı tablosu
- Zaman Planı
- Etik ve Veri Gizliliği
- Bölümlerin tek dosyada birleştirilmesi, PDF olarak 23 Kasım'a kadar yüklenmesi

## Notebook Nasıl Çalıştırılır?

1. Kaggle'daki [Turkish SMS Collection](https://www.kaggle.com/datasets/onurkarasoy/turkish-sms-collection) sayfasından veriyi indir, zip'i aç. İçinden `TurkishSMSCollection.csv` çıkar.
2. [colab.research.google.com](https://colab.research.google.com) adresine git. **File → Open notebook → GitHub** yolunu seç.
3. Arama kutusuna `SametYerseven/scamshield-tr` yaz, `notebooks/01_baseline_model.ipynb` dosyasını aç.
4. **Runtime → Run all** de. "Not authored by Google" uyarısına **Run anyway** de.
5. **Dosya seç** butonu çıkınca CSV dosyasını seç. Çalışma 2-5 dakika sürer.
6. En sonda `baseline_sonuclari.zip` iner. İçinde rapordaki grafikler ve tablolar var.

## Projedeki İşler

Takım lideri: Samet Yerseven. Görev dağılımı ekip içinde belirlenecek.

| İş | Kapsamı |
|---|---|
| Metin sınıflandırma modeli | Mesajın dolandırıcılık olup olmadığını tahmin eden model (önce basit model, sonra BERTurk) |
| Veri | Veri setlerini bulmak, örnek mesaj toplamak, etiketlemek, kişisel bilgileri maskelemek |
| Link analizi | Sahte linkleri tespit etmek, USOM ve PhishTank listeleri |
| Backend | API (FastAPI), modelleri birbirine bağlamak, açıklama üretimi, sistemi yayına almak |
| Arayüz ve dokümantasyon | Web arayüzü, Telegram botu, tasarım, raporların birleştirilmesi, sunum |

## Ara Rapor (Son teslim: 23 Kasım)

İç teslim: 22 Kasım akşamı. Herkes kendi bölümünü gönderir, 23 Kasım'da birleştirilip yüklenir.

| İş | Rapordaki bölüm | Yapılacak |
|---|---|---|
| Metin sınıflandırma modeli | Yöntem, Mevcut İlerleme | Tamamlandı |
| Veri | Etik ve Veri Gizliliği | Veri setlerini araştırmak, 50-100 örnek mesaj toplamak |
| Link analizi | Benzer Çalışmalar, Kaynaklar | Örnek zararlı linkleri inceleyip ortak özelliklerini çıkarmak |
| Backend | Sistem Tasarımı, Kullanılan Teknolojiler | Mimari diyagram |
| Arayüz ve dokümantasyon | Giriş, Amaç, Sosyal Katkı, Zaman Planı | Arayüz taslağı, raporun birleştirilmesi |

Görev Dağılımı bölümü ekipçe yazılacak. Karşılaşılan Sorunlar ve Çözümler bölümünün model kısmı hazır; diğer işlerde karşılaşılan sorunlar da bu bölüme eklenecek.

## Takvim

| Hafta | Hedef |
|---|---|
| 9 | Ara rapor ve ilk model |
| 10 | Veri toplama ve etiketleme, arayüz tasarımı |
| 11 | BERTurk modeli, link modeli, API |
| 12 | Açıklama üretimi, arayüz ile backend bağlantısı |
| 13 | Parçaların birleştirilmesi, Telegram botu, yayına alma |
| 14 | Kullanıcı testleri, final raporu |
| 15 | Final sunumu ve demo |

## Klasör Yapısı

```
data/          veri setleri (gerçek kişisel veri yüklenmez)
notebooks/     Colab/Jupyter çalışmaları
src/model/     metin modeli
src/url/       link analizi
src/api/       backend
src/bot/       Telegram botu
web/           web arayüzü
docs/          raporlar, diyagramlar, sunum
```

## Teknolojiler

Python, scikit-learn, Hugging Face Transformers (BERTurk), XGBoost, FastAPI, Streamlit/React, Telegram Bot API, Google Colab

## Çalışma Kuralları

- Herkes kendi branch'inde çalışır, main'e Pull Request ile eklenir.
- Gerçek mesajlardaki isim, telefon numarası gibi kişisel bilgiler maskelenir (KVKK).
- Haftada bir kısa toplantı yapılır.
