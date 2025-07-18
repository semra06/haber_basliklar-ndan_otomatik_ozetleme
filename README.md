# haber_basliklar-ndan_otomatik_ozetleme

Her Dosyanın Görevi:
1_preprocessing.py-> Veriyi indirir, temizler, tokenize eder ve kaydeder.

2_model_setup.py-> Model ve tokenizer’ı hazırlar, kaydeder.

3_training.py-> Modeli eğitir, kaydeder.

4_evaluation.py-> Eğitilmiş modelle özet üretir, ROUGE-L skorunu hesaplar, örnek çıktıları gösterir.

report.md-> Kısa rapor: Model, hiperparametreler, geliştirme süreci, gözlemler.

# NLP Ödevi Raporu: Haber Başlıklarından Otomatik Özetleme

## Model Seçimi
- Kullanılan model: **T5-small** (Huggingface Transformers kütüphanesinden)
- Neden T5-small? Düşük donanım gereksinimi, hızlı prototipleme ve özetleme görevlerinde başarılı sonuçlar vermesi nedeniyle tercih edilmiştir.

## Hiperparametreler
- Maksimum giriş uzunluğu: 512 token
- Maksimum özet uzunluğu: 64 token
- Öğrenme oranı: 2e-5
- Batch size: 4
- Epoch sayısı: 3
- Değerlendirme stratejisi: Her epoch sonunda
- Model kaydetme: En fazla 2 checkpoint

## Geliştirme Süreci
1. **Veri Ön İşleme:**
   - CNN/DailyMail veri seti indirildi.
   - Metinler küçük harfe çevrildi, noktalama ve fazla boşluklar temizlendi.
   - Tokenizer ile giriş ve hedef dizileri hazırlandı, padding ve truncation uygulandı.
2. **Model Kurulumu:**
   - T5-small modeli ve tokenizer indirildi ve kaydedildi.
3. **Eğitim:**
   - İşlenmiş veri ile model 3 epoch boyunca eğitildi.
   - Hızlı prototip için eğitim ve validasyon setlerinden küçük birer subset kullanıldı.
4. **Değerlendirme:**
   - Test setinden 5 örnek için model özetleri üretildi.
   - ROUGE-L metriği ile otomatik değerlendirme yapıldı.
   - Örnek çıktılar insan gözüyle incelendi.

## Gözlemler
- Model, kısa ve öz özetler üretme konusunda başarılıdır ancak bazen önemli detayları atlayabilir.
- ROUGE-L skorları, modelin temel özetleme yeteneğini göstermektedir.
- Daha uzun eğitim ve tam veri seti ile daha iyi sonuçlar alınabilir.
- T5-small modeli, donanım kısıtlı ortamlarda hızlıca prototip geliştirmek için uygundur.
