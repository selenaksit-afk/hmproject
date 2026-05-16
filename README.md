# H&M Kişiselleştirilmiş Moda Öneri Sistemi Projesi

Bu proje, H&M Personalized Fashion Recommendations veri seti kullanılarak müşteri davranışı analizi, trend analizi, tahminleme (forecasting) ve öneri sistemleri geliştirmeyi amaçlamaktadır.

## Kullanılan Teknolojiler

- SQL
  ## SQL Aşamasında Yapılan Çalışmalar

### Transactions Tablosu
- Toplam satır sayısı, unique müşteri ve unique ürün sayıları analiz edildi.
- Null değer kontrolleri yapıldı.
- Fiyat kolonunda sıfır veya negatif değer kontrolü gerçekleştirildi.
- Duplicate transaction kayıtları analiz edildi.
- Aynı müşteri, aynı ürün, aynı tarih ve aynı satış kanalına ait tekrar eden kayıtlar incelendi.
- Duplicate benzeri kayıtların veri setinin yapısından mı yoksa gerçek tekrar eden işlemlerden mi kaynaklandığı değerlendirildi.

### Customers Tablosu
- Unique müşteri kontrolü yapıldı.
- Null değer analizleri gerçekleştirildi.
- `age` kolonundaki minimum, maksimum ve ortalama yaş değerleri incelendi.
- Yaş dağılımı kontrol edilerek outlier analizi yapıldı.
- `club_member_status` kolonundaki boş değerler `UNKNOWN` olarak düzenlendi.
- `fashion_news_frequency` kolonundaki yazım tutarsızlıkları (`None` / `NONE`) standartlaştırıldı.
- `FN` ve `Active` kolonları binary flag yapısına dönüştürüldü.
- Temizlenmiş `customers_clean` tablosu oluşturuldu.

### Articles Tablosu
- Unique `article_id` kontrolü yapıldı.
- Ürün metadata kolonları için null analizleri gerçekleştirildi.
- `detail_desc` kolonundaki eksik veriler `UNKNOWN` olarak güncellendi.
- `product_code` ve `article_id` ilişkisi detaylı analiz edildi.
- Aynı `product_code` altında birden fazla `article_id` bulunduğu gözlemlendi.
- `article_id` kolonunun SKU/varyant seviyesinde ürünleri temsil ettiği değerlendirildi.
- Analiz ve machine learning süreçlerinde kullanılacak önemli kolonlar belirlendi.

  
- Google BigQuery
- dbt
- Python
- Makine Öğrenmesi

  

## Proje Amaçları

- Veri Temizleme (Data Cleaning)
- Keşifsel Veri Analizi (EDA)
- Müşteri Segmentasyonu
- Öneri Sistemleri Geliştirme
- Tahminleme (Forecasting)
