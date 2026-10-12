# E-posta Spam Sınıflandırma

Bu proje, etiketli e-postaları normal (ham) ve spam olarak sınıflandıran makine öğrenmesi algoritmalarını karşılaştırır. Python ve scikit-learn kullanılır; çalışma Google Colab'da yürütülebilir.

## Proje dosyaları

- notebooks/spam_classification.ipynb: Veriyi yükleyen, dört modeli eğiten ve sonuçlarını karşılaştıran açıklamalı notebook.
- requirements.txt: Gerekli Python paketleri.
- report_template.md: Gerçek sonuçlar alındıktan sonra doldurulacak rapor taslağı.

## Veri seti

UCI Spambase veri seti 4.601 e-posta örneği içerir. Etiket 0 ise normal, 1 ise spam'dir. Girdi sütunları e-postaların ham metni değil, e-postalardan önceden çıkarılmış sayısal özelliklerdir. Bu proje metin temizleme yerine sınıflandırma ve model değerlendirmeye odaklanır.

Kaynak: [UCI Machine Learning Repository — Spambase](https://archive.ics.uci.edu/dataset/94/spambase). Lisans: CC BY 4.0. Kaynak gösterimi: Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). Spambase. UCI Machine Learning Repository. https://doi.org/10.24432/C53G6X

## Algoritmalar

1. Gaussian Naive Bayes
2. Lojistik Regresyon
3. Destek Vektör Makinesi (RBF çekirdeği)
4. Random Forest

Veri, sınıf oranları korunarak eğitim ve test parçalarına ayrılır. Modeller aynı test verisinde accuracy, precision, recall ve F1 ile karşılaştırılır. Notebook her model için confusion matrix de üretir. En yüksek F1 değeri karşılaştırma ölçütü olarak kullanılır; raporda yanlış spam alarmı (FP) ve kaçırılan spam (FN) ayrıca açıklanır.

## Çalıştırma

1. Notebook'u Google Colab'da aç.
2. Hücreleri yukarıdan aşağıya sırayla çalıştır.
3. Gerçek sonuç tablosu ve confusion matrix grafiklerini gözden geçir.
4. Ölçüm sonuçlarını report_template.md dosyasına aktar.

Notebook veriyi UCI'dan indirir; data klasörüne ayrıca dosya koymak gerekmez. İlk hücre, veri indirme paketini kurar.

## Sonuçlar

Notebook bu depodan henüz çalıştırılmadı. Rapor taslağındaki sonuç alanları, notebook çalıştırıldıktan sonra gerçek çıktılarla doldurulmalıdır.
