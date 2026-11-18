# Complaint Triage Intelligence
### Türkçe Müşteri Geri Bildirimlerini Aksiyon Alınabilir İçgörülere Dönüştürmek

**%95,15 Doğruluk · %94,86 Macro F1 · %49 Daha Az Kaçırılan Şikâyet**

[English](README.md) | [Türkçe](README_TR.md)

Müşteri geri bildirimleri, ürün ve hizmet kalitesini anlamanın en doğrudan yollarından biri. Asıl zorluk, çok sayıda yorumun içinde gerçekten ilgilenilmesi gereken şikâyetleri doğru tespit etmek; özellikle de farklı yazım biçimleri ve olumlu-olumsuz görüşlerin bir arada bulunduğu metinlerde.

**Complaint Triage Intelligence**, Türkçe müşteri yorumlarında şikâyetleri tespit etmek ve farklı NLP yaklaşımlarının performansını karşılaştırmak için geliştirdiğim bir makine öğrenmesi projesi. Buradaki hedef yalnızca yorumları sınıflandırmak değil; **kaçırılan şikâyetleri azaltırken sonuçları ölçülebilir ve yorumlanabilir hâle getirmek**.

## Öne çıkan sonuçlar

| Metrik | İyileştirilmiş model |
|---|---:|
| Sınıflandırma doğruluğu | **%95,15** |
| Macro F1 skoru | **%94,86** |
| Şikâyet sınıfı recall | **%94,82** |
| Kaçırılan şikâyet sayısı | **53 → 27** |
| Kaçırılan şikâyetlerde azalma | **~%49** |

En iyi sonucu **karakter tabanlı TF-IDF (3–5 gram) + dengelenmiş Linear SVM** yaklaşımı verdi. Model, çapraz doğrulamayla seçildi ve 1.382 yorumdan oluşan ayrılmış test kümesinde değerlendirildi.

## İş dünyasında neden önemli?

Müşteri deneyimi ekipleri açısından gözden kaçan bir şikâyet, geciken bir müdahale veya kaçırılan bir iyileştirme fırsatı anlamına gelebilir. Bu çalışma, metin analiziyle şu süreçlerin nasıl desteklenebileceğini gösteriyor:

- **Şikâyetleri daha erken fark etmek:** Yüksek hacimli müşteri yorumlarında öncelikli geri bildirimleri belirlemek.
- **Destek ekiplerinin önceliklendirmesini kolaylaştırmak:** Şikâyet içeren yorumları diğerlerinden ayırmak.
- **Tekrarlanan müşteri problemlerini analiz etmek:** Dil kalıpları ve keşifsel analizle sorun alanlarını görünür kılmak.
- **Model sonuçlarını anlaşılır hâle getirmek:** Özellik analizi ve hata incelemesiyle tahminlerin nedenlerini araştırmak.

Bunlar yaklaşımın potansiyel kullanım alanlarıdır; proje, üretim ortamına alınmış bir müşteri hizmetleri sistemi değil, deneysel bir sınıflandırma çalışmasıdır.

## Projede neler geliştirdim?

**1. Veri hazırlama ve keşifsel analiz**  
Herkese açık Türkçe müşteri geri bildirimi veri setini inceledim, çelişkili etiketli tekrarları ayıkladım ve **6.906 yorumu** analiz için hazırladım. Sınıf dağılımlarını, yorum uzunluklarını ve metin örüntülerini araştırdım.

**2. Türkçeye özgü NLP işleme hattı**  
Türkçe karakterleri dikkate alan normalizasyon, tokenizasyon, stopword işlemleri, N-gram analizi, sözcük türü etiketleme (POS), varlık tanıma (NER) ve bağımlılık çözümlemesi uyguladım.

**3. Metin temsili ve model karşılaştırması**  
**Bag of Words, TF-IDF, Word2Vec ve BERTurk** yaklaşımlarını inceledim. Geleneksel sınıflandırma deneylerinde **Naive Bayes, Logistic Regression ve Linear SVM** modellerini karşılaştırdım.

**4. Hedef odaklı model iyileştirme**  
Yanlış sınıflandırılan yorumları analiz ederek kelime/karakter N-gramları, düzenlileştirme ve sınıf ağırlıkları üzerinde **18 deney** gerçekleştirdim. Ana değerlendirmede en güçlü sonucu karakter tabanlı TF-IDF + Linear SVM sağladı.

**5. Açıklanabilirlik ve değerlendirme**  
Modelin kararlarını etkileyen metin özelliklerini, confusion matrix sonuçlarını, hata örüntülerini ve yorum uzunluğunun etkisini analiz ettim. Önceden eğitilmiş BERTurk temsillerini ayrı bir karşılaştırma deneyinde değerlendirdim.

## Başlangıçtan iyileştirilmiş modele

| Aşama | Macro F1 | Doğruluk |
|---|---:|---:|
| Başlangıç: Kelime TF-IDF + Logistic Regression | %93,10 | %93,56 |
| İyileştirilmiş: Karakter TF-IDF + Linear SVM | **%94,86** | **%95,15** |

En önemli kazanım yalnızca genel performansın yükselmesi değil: **Aynı test kümesinde kaçırılan gerçek şikâyet sayısını 53'ten 27'ye indirdim.**

## Kullanılan teknolojiler

`Python` · `pandas` · `NumPy` · `scikit-learn` · `NLTK` · `Stanza` · `gensim` · `Transformers / BERTurk` · `Matplotlib` · `Seaborn` · `Jupyter Notebook`

## Projeyi inceleyin

Notebook; veri hazırlama, görsel analizler, model karşılaştırmaları, optimizasyon deneyleri ve BERTurk analizini baştan sona içeriyor.

**[Analiz notebook'unu aç](notebooks/)**

Deneyleri tekrar çalıştırmak için `requirements.txt` içindeki bağımlılıkları kurup notebook hücrelerini sırayla çalıştırabilirsiniz. Bazı NLP modellerinin indirilmesi internet bağlantısı gerektirebilir.

## Veri seti ve değerlendirme

- **Veri seti:** nanelimon tarafından Hugging Face üzerinde yayımlanan Complaint Classification Dataset (kaynak ve lisans bilgisi notebook'ta yer alıyor).
- **Ana değerlendirme:** 5.524 eğitim, 1.382 test örneği; sınıf oranlarını koruyan ayırma ve model seçimi için üç katlı çapraz doğrulama.
- **Transformer karşılaştırması:** Önceden eğitilmiş BERTurk embedding'leri, TF-IDF yaklaşımlarıyla ayrı bir 1.000 yorumluk alt kümede karşılaştırıldı.

## Proje hakkında

Bu projeyi, yapılandırılmamış Türkçe müşteri geri bildirimlerinin NLP ile nasıl ölçülebilir bir analiz sürecine dönüştürülebileceğini araştırmak için geliştirdim. Veri analizi, özellik mühendisliği, model karşılaştırması, optimizasyon ve açıklanabilir değerlendirme süreçlerini bir araya getiriyor.

**Geliştiren:** [Ceren Sinmec](https://github.com/cerensinmec)
