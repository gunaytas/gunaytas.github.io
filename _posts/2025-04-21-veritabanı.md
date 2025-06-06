---
layout: post
title: Veritabanı Yolculuğum
categories: [sql,veritabanı] 
---     

Son günlerde veritabanı dünyasında epeyce vakit geçirdim. Başta sadece bir ders içeriği gibi gelse de işin içine girdikçe ne kadar geniş ve güçlü bir alan olduğunu fark ettim. Veritabanı ile ilgili bilgim olsa da eksiğim çoktu. Bu yüzden en baştan tekrar başlamak istedim. 

---
Temel kavramlardan başlayarak ilişkilendirme, sorgulama ve modelleme konularına kadar birçok şey öğrendim ve uyguladım. ER diyagramlarından ilişkisel cebire, oradan da SQL sorgularına uzanan bol denemeli, bol yanlışlı ama bir o kadar da öğretici bu süreci hem kendim için özetlemek hem de kayıt altında tutmak adına bu yazıyı yazmak istedim. 

## Veritabanına Giriş: Temel Kavramlar
Verilerin organize ve anlamlı bir şekilde saklanması, erişilmesi ve işlenmesi için veritabanları vazgeçilmez bir rol oynuyor. Bu aşamada kavramsal, mantıksal ve fiziksel veri modelleri hakkında temel bilgiler edindim.

İlk adım olarak ER (Entity-Relationship) diyagramlarıyla çalıştım. Bu diyagramlar sayesinde tablolar (varlıklar), bu tabloların sahip olduğu özellikler (nitelikler) ve aralarındaki ilişkiler çok daha net bir şekilde anlaşılır hâle geliyor. ER diyagramı çizmek, veri modelini zihnimde oturtmama ve sistemin genel yapısını görselleştirmeme oldukça yardımcı oldu.

ER diyagramlarından yola çıkarak veritabanı tablolarını oluşturdum. Normalizasyon adımlarını da göz önünde bulundurarak, tekrar eden verileri ortadan kaldırmaya ve tutarlı bir yapı kurmaya dikkat ettim. Primary key, foreign key gibi kavramlarla tanıştım ve bunları aktif olarak kullandım.

## İlişkisel Cebir
Veritabanı çalışmalarımın önemli bir parçası da ilişkisel cebir (relational algebra) oldu. İlk başta matematiksel ifadelerle uğraşmak biraz yabancı gelse de zamanla σ (seçim), π (projeksiyon), ⋈ (birleşim)gibi işlemlerin mantığını kavrayınca oldukça keyifli bir hâl aldı. Bu bölüm, SQL gibi pratik sorgulama dillerinin temelini anlamamı sağladı. Ayrıca daha ileri safhalarda SQL ile sorgu yazarken önce ilişkisel cebir ifadelerini oluşturmak işimi çok kolaylaştırdı.


## SQL ile Sorgu Yazma: Öğrendiklerimi Uygulama Zamanı
Teorik bilgilerin ardından uygulama kısmına geldim: SQL ile sorgular yazmak! Veritabanına veri eklemek (INSERT), güncellemek (UPDATE), silmek (DELETE) ve sorgulamak (SELECT) gibi temel işlemleri bol bol pratik ettim.

```bash
CREATE TABLE SporKompleksi (
    kompleksID INT PRIMARY KEY,
    kompleksAdi VARCHAR(100),
    toplamAlan INT,
    tip VARCHAR(10)
);

CREATE TABLE AltKompleks (
    altKompleksID INT PRIMARY KEY,
    kompleksID INT,
    konum VARCHAR(100),
    altKompleksAdi VARCHAR(100),
    FOREIGN KEY (kompleksID) REFERENCES SporKompleksi(kompleksID)
);
```

Ve en eğlenceli ve çıldırtıcı kısım sorgu yazmak. Özellikle çoklu tablo sorguları, JOIN'ler, alt sorgular ve gruplama işlemleri (GROUP BY, HAVING) ile çalışmak hem zorlayıcı hem de öğreticiydi.


Her bir ürün için, o ürünün ortalama fiyatından fazla fiyat veren üreticilerin adlarını listeleme
```bash
SELECT DISTINCT f.üreticiAdı
FROM Katalog k
JOIN Üretici f ON k.üreticiKodu = f.üreticiKodu
WHERE k.fiyat > (
    SELECT AVG(k2.fiyat)
    FROM Katalog k2
    WHERE k2.ürünKodu = k.ürünKodu
);
```
Bu sorguda yer alan WHERE k2.ürünKodu = k.ürünKodu ifadesinin gruplama yaptığını öğrenmem büyük bir aydınlanma noktasıydı. 


Minimum sayıda derse kaydolmuş öğrencilerin isimlerini listeleme
```bash
SELECT O.OgrenciAdı FROM Ogrenci O, 
(SELECT OgrenciNo, COUNT(DersAdı) AS sayi FROM Ders_kayıt 
GROUP BY OgrenciNo) as Ders_sayi
WHERE Ders_sayi.OgrenciNo= O.OgrenciNo AND Ders_sayi.sayi IN (SELECT MIN(sayi) FROM Ders_sayi)
```


Bu Süreçten Neler Öğrendim?
- Veri modellemesi doğru yapılmadan sistemin sağlıklı çalışması zor.

- İlişkisel cebir, SQL sorgularının mantığını anlamada gerçekten çok işe yaradı.

- Sürekli pratik yapmak, teorik bilginin oturmasını sağlıyor.

- Hatalar yapmak, sürecin bir parçası ve her hatada yeni bir şey öğreniliyor.


Bu süreç hâlâ devam ediyor, ama geldiğim noktada bile veritabanlarına ve veriyle çalışma prensiplerine dair oldukça sağlam bir temel edindiğimi hissediyorum. Gözümde büyüyen her kavram zamanla çok tanıdık hâle geliyor. 