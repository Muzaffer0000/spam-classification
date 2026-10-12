# E-posta Spam Sınıflandırma — Rapor Taslağı

> Köşeli parantezli sonuç alanlarını notebook'u çalıştırdıktan sonra gerçek değerlerle doldur. Sonuçları önceden tahmin etme.

## 1. Amaç

Bu çalışmanın amacı, etiketli e-posta örneklerinden bir e-postanın spam mı yoksa normal (ham) mı olduğunu tahmin etmek ve makine öğrenmesi algoritmalarını aynı test verisinde karşılaştırmaktır.

## 2. Veri seti

- Kaynak: [UCI Spambase](https://archive.ics.uci.edu/dataset/94/spambase)
- Örnek sayısı: 4.601 e-posta
- Girdi: 57 sayısal özellik
- Hedef: 0 = normal, 1 = spam
- Not: Veri seti ham e-posta metnini değil, e-postalardan çıkarılmış sayısal özellikleri içerir.

## 3. Uygulanan yöntem

Veri, sınıf dağılımı korunarak yüzde 80 eğitim ve yüzde 20 test olarak ayrıldı. Eğitim verisi modelleri öğretmek, test verisi ise daha önce görülmemiş örneklerde başarıyı değerlendirmek için kullanıldı. Tekrarlanabilirlik için rastgelelik tohumu 42 olarak ayarlandı.

Karşılaştırılan algoritmalar:
- Gaussian Naive Bayes
- Lojistik Regresyon
- Destek Vektör Makinesi (RBF)
- Random Forest

## 4. Confusion matrix açıklaması

Confusion matrix, gerçek sınıf ile model tahminini karşılaştırır. Sınıf sırası normal, sonra spam olduğunda:

| Gerçek / Tahmin | Normal tahmini | Spam tahmini |
|---|---:|---:|
| Gerçek normal | TN | FP |
| Gerçek spam | FN | TP |

- FP: Normal e-posta yanlışlıkla spam sayılır.
- FN: Spam e-posta normal sanılır.
- TP: Spam doğru yakalanır.
- TN: Normal e-posta doğru tanınır.

## 5. Sonuçlar

Notebook'tan gelen değerleri aktar:

| Model | Accuracy | Precision (spam) | Recall (spam) | F1 (spam) |
|---|---:|---:|---:|---:|
| Gaussian Naive Bayes | 83,39% | 71,78% | 95,32% | 81,89% |
| Lojistik Regresyon | 92,94% | 92,09% | 89,81% | 90,93% |
| Destek Vektör Makinesi | 92,73% | 92,77% | 88,43% | 90,55% |
| Random Forest | 94,57% | 95,10% | 90,91% | 92,96% |

**En yüksek F1 değerini veren model:** Random Forest (92,96%)

**Seçim gerekçesi:** Bu çalıştırmada Random Forest en yüksek accuracy ve F1 değerlerini verdi. Spam tahminlerinde precision değeri %95,10 olduğundan spam dediği e-postaların çoğu gerçekten spamdi; recall değeri %90,91 olduğundan test kümesindeki spam'lerin çoğunu yakaladı. Naive Bayes daha yüksek recall (%95,32) verdi, ancak spam precision değeri daha düşüktü (%71,78), yani daha fazla normal e-postayı spam diye işaretledi.

## 6. Hata analizi

Random Forest confusion matrix'i, sınıf sırası [normal, spam] ve satırlar gerçek/sütunlar tahmin olacak şekilde:

| Gerçek / Tahmin | Tahmin normal | Tahmin spam |
|---|---:|---:|
| Gerçek normal | 541 (TN) | 17 (FP) |
| Gerçek spam | 33 (FN) | 330 (TP) |

Model 558 normal e-postanın 541'ini doğru bıraktı; 17'sine yanlış spam alarmı verdi. 363 spam e-postanın 330'unu yakaladı, 33'ünü kaçırdı. FP normal bir iletinin spam klasörüne düşmesi; FN spam'in gelen kutusunda kalması anlamına gelir.

## 7. Sonuç ve sınırlamalar

Bu deneyde Random Forest, test kümesinde en yüksek F1 (%92,96) ve accuracy (%94,57) değerlerini verdi. 17 yanlış spam alarmı ve 33 kaçırılan spam üretti. Bu sonuç, UCI Spambase veri setindeki seçilen stratified eğitim/test ayrımı için geçerlidir. Veri seti ham e-posta metnini içermez; bu nedenle sonuçlar gerçek zamanlı gelen kutularına doğrudan genellenemez. Başka e-posta koleksiyonlarında başarı farklı olabilir.

## Kaynakça

Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). Spambase. UCI Machine Learning Repository. https://doi.org/10.24432/C53G6X
