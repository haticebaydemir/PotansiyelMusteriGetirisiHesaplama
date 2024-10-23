# Gezinomi Kural Tabanlı Sınıflandırma ile Potansiyel Müşteri Getirisi Hesaplama

## Proje Hakkında
Bu proje, **Gezinomi** platformundaki verilere dayalı olarak potansiyel müşterilerin karlılığını analiz etmek amacıyla geliştirilmiştir. Kural tabanlı sınıflandırma yöntemi kullanılarak, şehir, konsept ve sezon gibi kriterler altında satışların analizi yapılmakta ve farklı müşteri segmentleri oluşturulmaktadır. Bu sayede, işletmelerin stratejik kararlarını desteklemek amacıyla veri odaklı içgörüler elde edilmesi hedeflenmektedir. Aynı zamanda MİUUL Python Programming for Data Science kursunun bitirme projesidir.


### Amaç
- Müşteri segmentlerinin belirlenmesi
- Farklı şehir ve konseptler için karlılık analizi
- Satış verilerinin detaylı analizi ve görselleştirilmesi

## Gereksinimler

Projenin çalışması için aşağıdaki yazılım ve kütüphanelere ihtiyaç vardır:

- **Python**: 3.x sürümü
- **Gerekli Kütüphaneler**:
  - `pandas`
  - `numpy`
  - `openpyxl`
  - `matplotlib`
  - `seaborn`
  

## Kurulum

Projenizi yerel makinenize kurmak için aşağıdaki adımları izleyin:

1. **Bu depoyu klonlayın**:
   ```bash
   git clone https://github.com/kullanici_adiniz/gezinomi_potansiyel_musteri.git


##  Temel Analizler
Aşağıdaki kodlar ile veri seti hakkında çeşitli analizler yapabilirsiniz:

a. **Şehir Analizi**
   ```bash
unique_sehirler = df['SaleCityName'].unique()
print(f"Benzersiz şehir sayısı: {len(unique_sehirler)}")
sehir_frekanslari = df['SaleCityName'].value_counts()
print("\nŞehir Frekansları:")
print(sehir_frekanslari)

```
b. **Konsept Analizi**
```bash
unique_concepts = df['ConceptName'].unique()
print(f"Benzersiz konsept sayısı: {len(unique_concepts)}")
concept_frekanslari = df['ConceptName'].value_counts()
print("\nConcept Frekansları:")
print(concept_frekanslari)

```
c. **Kazanç Analizi**
```bash
toplam_kazanc = df.groupby('SaleCityName')['Price'].sum()
print("Şehirlere göre toplam kazanç:")
print(toplam_kazanc)

```
## Veri Analizi

Projede gerçekleştirilen bazı analizler ve çıktılar:
1. **Fiyat Ortalamaları**
```bash
price_mean_by_city = df.groupby('SaleCityName')['Price'].mean()
price_mean_by_concept = df.groupby('ConceptName')['Price'].mean()
```

2. **Yeni Kategorik Değişken Tanımlama**
```bash
bins = [-1, 7, 30, 90, df["SaleCheckInDayDiff"].max()]
labels = ["Last Minuters", "Potential Planners", "Planners", "Early Bookers"]
df["EB_Score"] = pd.cut(df["SaleCheckInDayDiff"], bins, labels=labels)
```
3. **Segmentasyon**
```bash
agg_df = df.groupby(["SaleCityName", "ConceptName", "Seasons"]).agg({"Price": "mean"}).sort_values("Price", ascending=False)
agg_df.reset_index(inplace=True)
agg_df['sales_level_based'] = agg_df[["SaleCityName", "ConceptName", "Seasons"]].agg(lambda x: '_'.join(x).upper(), axis=1)
agg_df["SEGMENT"] = pd.qcut(agg_df["Price"], 4, labels=["D", "C", "B", "A"])

```
## Sonuçlar
Bu projede elde edilen veriler kullanılarak satış analizleri, müşteri segmentleri ve karlılık raporları oluşturulmuştur. Örneğin:

- **En Yüksek Ortalama Fiyatlar**: Belirli şehir ve konsept kombinasyonları için yüksek fiyat ortalamaları tespit edilmiştir.
- **Müşteri Segmentleri**: Müşteri fiyatlarına göre 4 segmente ayrılmıştır (A, B, C, D).

## Örnek Çıktı
```bash
new_user = "ANTALYA_HERŞEY DAHIL_HIGH"
result = agg_df[agg_df["sales_level_based"] == new_user]
print(result)

```

## İletişim
Sorularınız veya geri bildirimleriniz için benimle iletişime geçebilirsiniz:

- Email: baydemirhatice@hotmail.com
- LinkedIn: https://www.linkedin.com/in/haticebaydemir/
