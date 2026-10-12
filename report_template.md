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
| Gaussian Naive Bayes | [çalıştırınca doldur] |  |  |  |
| Lojistik Regresyon |  |  |  |  |
| Destek Vektör Makinesi |  |  |  |  |
| Random Forest |  |  |  |  |

**En yüksek F1 değerini veren model:** [model adı]

**Seçim gerekçesi:** [F1 değerini ve precision/recall dengesini gerçek sonuçlarla açıkla.]

## 6. Hata analizi

En iyi modelin confusion matrix'ine göre:

- Yanlış spam alarmı (FP): [sayı]
- Kaçırılan spam (FN): [sayı]

Bu hataların kullanıcı açısından ne anlama geldiğini açıkla. Örneğin FP, normal bir e-postanın spam klasörüne düşmesine; FN ise spam'in gelen kutusunda kalmasına yol açabilir.

## 7. Sonuç ve sınırlamalar

[Hangi modelin bu veri setinde daha iyi sonuç verdiğini, bunu hangi ölçütlerle belirlediğini ve veri setinin ham e-posta metni içermediğini özetle.]

Sonuçlar kullanılan veri seti ve eğitim/test ayrımı için geçerlidir; başka e-posta koleksiyonlarında başarı farklı olabilir.

## Kaynakça

Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). Spambase. UCI Machine Learning Repository. https://doi.org/10.24432/C53G6X
