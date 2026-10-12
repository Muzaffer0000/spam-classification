# E-posta Spam Sınıflandırma

Bu proje, e-postaları **normal (ham)** ve **spam** olarak sınıflandırmak için dört makine öğrenmesi algoritmasını karşılaştırır. Kod Python ve scikit-learn kullanır; Google Colab'da çalıştırılabilir.

## Proje dosyaları

- [Açıklamalı Jupyter notebook](notebooks/spam_classification.ipynb): Veri setini yükler, dört modeli eğitir, metrikleri ve confusion matrix'leri üretir.
- [Proje raporu](REPORT.md): Yöntemi, model karşılaştırmasını, en iyi modeli, hata analizini ve veri seti sınırlamasını açıklar.
- [Bağımlılıklar](requirements.txt): Gerekli Python paketleri.

## Veri seti

UCI Spambase veri setinde 4.601 e-posta örneği ve 57 sayısal özellik bulunur. Etiket 0 normal, 1 spam anlamına gelir. Veri seti ham e-posta metinlerini değil, e-postalardan önceden çıkarılmış sayısal özellikleri içerir. Bu nedenle çalışma ham metin temizleme veya kelime vektörleştirme yapmaz.

Kaynak: [UCI Machine Learning Repository — Spambase](https://archive.ics.uci.edu/dataset/94/spambase). Lisans: CC BY 4.0. Kaynak gösterimi: Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). *Spambase*. https://doi.org/10.24432/C53G6X

## Yöntem

Veri, normal ve spam oranları korunarak yüzde 80 eğitim ve yüzde 20 test olarak ayrılır. Dört algoritma aynı bölünmede değerlendirilir:

1. Gaussian Naive Bayes
2. Lojistik Regresyon
3. Destek Vektör Makinesi (RBF)
4. Random Forest

Modeller accuracy, spam precision, spam recall ve spam F1 ile karşılaştırılır. Confusion matrix, doğru tahminlerin yanı sıra normal bir e-postaya yanlış spam alarmı verilmesini (FP) ve spam'in kaçırılmasını (FN) gösterir. En yüksek spam F1 değerine göre bu deneyde Random Forest seçilmiştir.

## Bu çalıştırmanın sonuçları

| Model | Accuracy | Precision (spam) | Recall (spam) | F1 (spam) |
|---|---:|---:|---:|---:|
| Gaussian Naive Bayes | 83,39% | 71,78% | 95,32% | 81,89% |
| Lojistik Regresyon | 92,94% | 92,09% | 89,81% | 90,93% |
| Destek Vektör Makinesi (RBF) | 92,73% | 92,77% | 88,43% | 90,55% |
| **Random Forest** | **94,57%** | **95,10%** | **90,91%** | **92,96%** |

Random Forest confusion matrix'i (satırlar gerçek, sütunlar tahmin; sıra normal, spam):

| Gerçek / Tahmin | Tahmin normal | Tahmin spam |
|---|---:|---:|
| Gerçek normal | 541 | 17 |
| Gerçek spam | 33 | 330 |

Bu sonuçlar 80/20 stratified tek bir eğitim/test bölünmesine ve random_state=42 değerine aittir; başka veri kümelerinde sonuçlar değişebilir. Ayrıntılı yorum için [proje raporuna](REPORT.md) bakın.

## Çalıştırma

1. [Notebook'u](notebooks/spam_classification.ipynb) Colab'a yükleyin veya Python/Jupyter ortamında açın.
2. Hücreleri yukarıdan aşağıya çalıştırın.
3. Karşılaştırma tablosu ve confusion matrix çıktılarını inceleyin.

Notebook veri setini UCI'dan indirir; projeye ayrıca veri dosyası eklemek gerekmez.