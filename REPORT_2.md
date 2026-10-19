# Ödev 2 — Model iyileştirme ve ROC analizi

## Amaç

İlk ödevdeki spam/normal e-posta sınıflandırma deneyini geliştirmek; model parametrelerini eğitim verisinde çapraz doğrulamayla ayarlamak ve algoritmaları ROC eğrileri ile ROC-AUC kullanarak karşılaştırmak.

## Veri ve deney düzeni

UCI Spambase veri kümesi kullanılmıştır. Veri setinde 4.601 örnek ve e-postalardan çıkarılmış 57 sayısal özellik bulunur; ham e-posta metni içermez. Etiket 0 normal, 1 spam anlamına gelir.

Veri, sınıf oranları korunarak `random_state=42` ile yüzde 80 eğitim ve yüzde 20 test olarak ayrılmıştır. Parametre araması yalnızca eğitim kümesinde beş katlı StratifiedKFold çapraz doğrulamasıyla yapılmıştır. Ölçekleme gereken modellerde StandardScaler, veri sızıntısını önlemek için Pipeline içinde kullanılmıştır. Test kümesi nihai değerlendirme için ayrılmıştır.

Karşılaştırılan algoritmalar:
- Gaussian Naive Bayes
- Lojistik Regresyon
- RBF çekirdekli Destek Vektör Makinesi
- Random Forest

Arama hedefi çapraz doğrulamada spam F1 skorudur. Arama aralıkları ve kod `notebooks/model_iyilestirme_roc.ipynb` içindedir.

## Sonuçlar

Notebook'u Colab'da baştan sona çalıştırdıktan sonra aşağıdaki tablodaki boş alanları, notebook'un “Temel ve ayarlanmış karşılaştırma” çıktısından doldurun. Değerler 0 ile 1 aralığındadır.

| Model | Aşama | Accuracy | Spam precision | Spam recall | Spam F1 | ROC-AUC |
|---|---|---:|---:|---:|---:|---:|
| Gaussian Naive Bayes | Temel | — | — | — | — | — |
| Gaussian Naive Bayes | Ayarlanmış | — | — | — | — | — |
| Logistic Regression | Temel | — | — | — | — | — |
| Logistic Regression | Ayarlanmış | — | — | — | — | — |
| SVM (RBF) | Temel | — | — | — | — | — |
| SVM (RBF) | Ayarlanmış | — | — | — | — | — |
| Random Forest | Temel | — | — | — | — | — |
| Random Forest | Ayarlanmış | — | — | — | — | — |

**En iyi ayarlanmış model (test spam F1'e göre):** Notebook çıktısından buraya yazın.

**ROC-AUC yorumu:** AUC 1'e yaklaştıkça model normal ve spam e-postaları farklı eşiklerde daha iyi ayırt eder. ROC grafiğinin sol üst köşesine yakın olması tercih edilir. Kesikli çapraz çizgi rastgele tahmin seviyesini (AUC=0,5) gösterir.

## Confusion matrix ve hata analizi

En iyi ayarlanmış modelin notebook'ta gösterilen confusion matrix'ini buraya aktarın:

| Gerçek / Tahmin | Tahmin normal | Tahmin spam |
|---|---:|---:|
| Gerçek normal | TN: — | FP: — |
| Gerçek spam | FN: — | TP: — |

FP, normal bir e-postaya yanlışlıkla spam denmesidir. FN, spam e-postanın normal sanılıp kaçırılmasıdır. TN ve TP doğru sınıflandırmalardır.

## Değerlendirme

Temel ve ayarlanmış modelleri test spam F1 ve ROC-AUC açısından karşılaştırın. Ayar aramasının sonucu her ölçütte iyileştireceği garanti değildir; sonucu notebook'un gerçek çıktısına göre yorumlayın. Spam'i kaçırmanın mı yoksa normal e-postaya yanlış alarm vermenin mi daha maliyetli olduğuna göre precision ve recall dengesini de açıklayın.

## Sınırlama

UCI Spambase ham e-posta gövdelerini değil, önceden çıkarılmış sayısal özellikleri içerir. Bu deney metin temizleme, kelime vektörleştirme veya yeni e-postalardan özellik çıkarma yapmaz. Sonuçlar bu veri seti, veri bölünmesi ve denenmiş parametre aralıklarıyla sınırlıdır.
