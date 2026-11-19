# 🛡️ ScamShield TR — Dolandırıcılık Kalkanı

Türkçe dolandırıcılık mesajlarını yapay zekâ ile tespit eden sistem.
*Sosyal Sorumluluk Dersi Projesi — Konu: Siber Güvenlik ve Blokzinciri Uygulamaları*

---

## Problem

"Kargonuz teslim edilemedi", "hesabınız bloke oldu", "hakkınızda icra takibi başlatıldı"…
Bu tür sahte SMS ve WhatsApp mesajları her gün binlerce kişiyi, özellikle de yaşlıları dolandırıyor.

## Çözüm

Kullanıcı şüphelendiği mesajı sisteme yapıştırır. Sistem:

1. **Metni analiz eder:** Dolandırıcılık mı? Hangi türden?
2. **Linki kontrol eder:** Sahte site mi?
3. **Sade bir Türkçeyle açıklar:** *"Bu mesaj sahte kargo dolandırıcılığına benziyor. Linke tıklamayın."*

```
Kullanıcı (Web / Telegram botu)
        │
        ▼
   Backend API
        │
   ┌────┼────────────┐
   ▼    ▼            ▼
 Metin  Link        Açıklama
 modeli analizi     (LLM)
        │
        ▼
 Sonuç + açıklama
```

---

## Ekip ve Görevler

| Kişi | Rol | Ne yapacak? |
|---|---|---|
| _İsim_ (Takım Lideri) | **Yapay Zekâ / NLP** | Mesaj metnini sınıflandıran model (önce basit model, sonra BERTurk) |
| _İsim_ | **Veri** | Veri setlerini bulmak, örnek mesaj toplamak, etiketlemek, kişisel bilgileri maskelemek |
| _İsim_ | **Siber Güvenlik / Link Analizi** | Sahte linkleri tespit eden model, USOM ve PhishTank listeleri |
| _İsim_ | **Backend + LLM** | API (FastAPI), modelleri birbirine bağlamak, LLM ile açıklama üretmek, canlıya almak |
| _İsim_ | **Arayüz + Dokümantasyon** | Web arayüzü, Telegram botu, Figma tasarımı, raporları birleştirmek, sunum |

> Etiketleme işi herkese bölünecek. Rapordaki her bölümü o işin sorumlusu yazacak.

---

## ⏰ Bu Hafta: Ara Rapor (Son teslim: 23 Kasım)

**İç teslim: 22 Kasım akşamı.** Herkes kendi bölümünü gönderiyor, 23'ünde birleştirilip yükleniyor.

| Rol | Rapordaki bölümü | Yapılacak somut iş |
|---|---|---|
| Yapay Zekâ | Yöntem, Mevcut İlerleme, Görev Dağılımı, Sorunlar ve Çözümler | Basit model eğitip sonuçları çıkarmak (doğruluk, grafik) |
| Veri | Etik ve Veri Gizliliği | Hazır veri setlerini araştırmak, 50–100 örnek mesaj toplamak |
| Siber Güvenlik | Benzer Çalışmalar, Kaynaklar | Örnek zararlı linkleri incelemek, ortak özelliklerini çıkarmak |
| Backend + LLM | Sistem Tasarımı, Kullanılan Teknolojiler | Mimari diyagram çizmek |
| Arayüz + Dok. | Giriş, Amaç, Sosyal Katkı, Zaman Planı | Figma'da arayüz taslağı, raporu birleştirip formatlamak |

---

## 📅 Genel Takvim

| Hafta | Hedef |
|---|---|
| 9 | Ara rapor + ilk model |
| 10 | Veri toplama ve etiketleme, arayüz tasarımı |
| 11 | BERTurk modeli, link modeli, API iskeleti |
| 12 | LLM açıklama, arayüz ↔ backend bağlantısı |
| 13 | Her şeyi birleştirme, Telegram botu, canlıya alma |
| 14 | Gerçek kullanıcılarla test, final raporu |
| 15 | 🎤 Final sunumu ve canlı demo |

---

## 📁 Klasör Yapısı

```
data/          → veri setleri (gerçek kişisel veri YÜKLENMEZ)
notebooks/     → Colab/Jupyter denemeleri
src/model/     → metin modeli
src/url/       → link analizi
src/api/       → backend
src/bot/       → Telegram botu
web/           → web arayüzü
docs/          → raporlar, diyagramlar, sunum
```

## 🧰 Teknolojiler

Python · scikit-learn · Hugging Face Transformers (BERTurk) · XGBoost · FastAPI · Streamlit/React · Telegram Bot API · Google Colab

## 🤝 Çalışma Kuralları

- Herkes kendi **branch**'inde çalışır, `main`'e Pull Request ile eklenir.
- Gerçek mesajlardaki isim, telefon numarası gibi bilgiler **mutlaka maskelenir** (KVKK).
- Haftada bir 30 dakikalık toplantı: *Ne yaptım, ne yapacağım, nerede takıldım?*
