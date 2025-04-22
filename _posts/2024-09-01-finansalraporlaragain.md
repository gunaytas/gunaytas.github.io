---
layout: post
title: Finansal Raporlar 2
categories: [ruby,rails] 
---     

Ruby on Rails öğrenme sürecimde geliştirdiğim web projesini sizinle paylaşmak istiyorum. Bu proje, hem backend hem de frontend tarafında öğrendiklerimi pekiştirmeme yardımcı oldu. Rails’in sunduğu basitlik ve gücü kullanarak bir veritabanı bağlantılı bir web uygulaması geliştirdim ve bu uygulamanın ön yüzünü Tailwind CSS ile tasarladım.

---

### Projenin Amacı
Bu proje, kullanıcıların finansal harcamalarını etkin bir şekilde takip edip analiz edebilecekleri kullanıcı dostu ve güvenli bir platform geliştirmek amacıyla oluşturuldu. Proje, kullanıcıların gelir ve giderlerini düzenli olarak kaydedebilmelerini, bu verileri farklı kategorilere göre analiz edebilmelerini, sonuçları anlamlı raporlar ve grafikler aracılığıyla görüntüleyebilmelerini sağlamayı hedeflemektedir.

### Projenin Ana Hedefleri
1. **Finansal Durumun Anlaşılması:** Kullanıcıların harcamalarını detaylı bir şekilde takip ederek, gelir ve gider dengelerini anlamalarını ve bütçelerini daha iyi yönetmelerini sağlamak.
2. **Harcamaların Analizi ve Raporlanması:** Harcama verilerini kategorize ederek, kullanıcıların hangi alanlarda daha fazla harcama yaptıklarını görmelerine olanak tanımak. Bu sayede, gereksiz harcamalar tespit edilebilir ve maliyet azaltma stratejileri geliştirilebilir.
3. **Güvenli ve Kullanıcı Dostu Bir Deneyim Sunmak:** Kullanıcıların finansal verilerini güvenli bir şekilde saklayabilmelerini ve yönetebilmelerini sağlamak, aynı zamanda basit ve anlaşılır bir arayüz ile kullanıcı deneyimini iyileştirmek.

---

### Kullanılan Teknolojiler

1. **Ruby on Rails:** Projenin backend kısmını oluşturdum. Rails sayesinde veritabanı bağlantıları ve veri yönetimi oldukça kolay hale geldi.
2. **Tailwind CSS:** Ön yüz tasarımında minimalist ve estetik bir görünüm sağladı. Kullanıcı dostu arayüzlerle tasarım süreci keyifli bir hale getirdi.
3. **SQLite3:** Web uygulamasının veritabanı için uygun buldum.
4. **Postman:** API testlerini gerçekleştirmek ve backend işlemlerini doğrulamak için kullandım.
5. **Devise:** Kullanıcı kimlik doğrulama ve yetkilendirme işlemlerini kolaylıkla uygulamak için kullandım.

---

### Proje Geliştirme Adımları

#### **1. Gereksinim Analizi**
Projenin ilk aşamasında, kullanıcıların ihtiyaçlarını ve hedeflerini anlamak için detaylı bir gereksinim analizi gerçekleştirdim. Bu aşama, hangi özelliklerin öncelikli olduğunu ve nasıl bir yapının kurulması gerektiğini belirlememe yardımcı oldu.

#### **2. Algoritma ve Sayfa Tasarımlarının Oluşturulması**
Sayfaların işlevselliklerini belirlemek için uygun algoritmaları ve akış diyagramlarını oluşturdum ve kullanıcı deneyimini optimize etmek adına her sayfa için mockup oluşturdum. Bu adım ilerlememi büyük bir ölçüde hızlandırdı. 

<img src="/images/wireframe1.png" alt="mockup" width="400">
<img src="/images/liste.png" alt="mockup" width="400">


<!-- Model, controller ve view yapıları arasındaki ilişkiyi kullanarak CRUD (Create, Read, Update, Delete) işlemlerini uyguladım. -->

#### **3. Backend Geliştirme: Devise ile Kimlik Doğrulama**
Projenin backend kısmında ilk adım olarak, kullanıcı kimlik doğrulama işlemleri için Devise gem'ini entegre ettim. Bu sayede kullanıcıların güvenli bir şekilde giriş yapabilmelerini ve hesap oluşturabilmelerini sağladım. 

```bash
rails generate devise:install
rails generate devise User
rake db:migrate
```

#### **4. Tailwind CSS ile Sayfa Tasarımlarının Uygulanması**
Tasarımları hayata geçirmek için Tailwind CSS kullandım. Bu araç, utility-first yaklaşımıyla karmaşık CSS dosyaları yazmayı gereksiz kıldı ve doğrudan HTML üzerinde stil vermemi sağladı. 

<img src="/images/anasayfa.png" alt="mockup" width="400">
<img src="/images/image.png" alt="mockup" width="400">

#### **5. Model Dosyalarının ve Veritabanının Oluşturulması**
Backend geliştirme sürecinde bir sonraki adım model dosyalarını oluşturarak veritabanını tanımlamak oldu. Rails'in Active Record yapısını kullanarak gerekli modelleri ve ilişkileri oluşturdum. Bu aşama, verilerin güvenli ve doğru bir şekilde saklanması açısından önem taşıyordu.

```bash
rails generate model Transaction desc:string date:date category:string amount:integer income:boolean user:references
rake db:migrate
```

```ruby
ActiveRecord::Schema[7.1].define(version: 2024_08_10_200913) do
  create_table "transactions", force: :cascade do |t|
    t.string "desc"
    t.date "date"
    t.string "category"
    t.integer "amount"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.boolean "income"
    t.integer "user_id", null: false
    t.index ["user_id"], name: "index_transactions_on_user_id"
  end
end
```

#### **6. Controller Dosyalarının Oluşturulması**
Kullanıcı isteklerini işlemek ve veritabanı ile etkileşimi sağlamak için gerekli controller dosyalarını oluşturdum. CRUD işlemlerini gerçekleştirebilmek için temel fonksiyonlar ekledim.

#### **6. API Testleri**
Postman aracılığıyla oluşturduğum API’leri test ettim. Özellikle CRUD işlemlerini doğrulamak ve doğru verinin döndüğünden emin olmak için Postman oldukça faydalı oldu. Kimlik doğrulama, veri ekleme, güncelleme ve silme gibi işlemler test edildi.


#### **7. Kullanıcı Deneyimi**
Gerçek kullanıcılar ile testler yapılarak, sistemin kullanılabilirliği ve kullanıcı deneyimi değerlendirildi. Kullanıcı geri bildirimleri dikkate alınarak, gerekli iyileştirmeler yapıldı.
---

### Sonuç ve Öğrendiklerim
Proje geliştirme sürecinde belirlenen hedefler büyük ölçüde gerçekleştirildi. Kullanıcılar için güvenli, hızlı ve kullanımı kolay bir finans yönetim platformu oluşturuldu.

Bu proje, Ruby on Rails ile neler başarabileceğimi görmek açısından harika bir deneyim oldu. Aynı zamanda öğrendiklerimi pekiştirebildiğim güzel bir örnekti. Rails’in sunduğu kolaylıklar ve Tailwind’in tasarım sürecindeki etkisi birleşerek işlevsel ve şık bir uygulama ortaya koymamı sağladı. 

### **Eklenecek Özellikler**
- **Banka Hesap Hareketi İçeri Aktarma:** Kullanıcıların bankalarından hesap hareket döküm tablolarını içeri aktararak manuel giriş yapmadan verilerini sistemde kullanabilmesini sağlayan bir özellik.
- **Bütçe Planlama:** Kullanıcıların aylık bütçelerini belirleyerek harcamalarını kontrol altında tutmalarına yardımcı olacak bir özellik.
- **Grafik ve Analiz Geliştirmeleri:** Kullanıcıların finansal durumlarını daha iyi anlamalarına yardımcı olacak detaylı grafikler ve istatistikler eklenmesi.
- **Çoklu Para Birimi Desteği:** Kullanıcıların farklı para birimlerinde finansal işlemlerini takip edebilmeleri için çoklu para birimi desteği sağlanması.
- **Uyarı Sistemi:** Kullanıcıların belirli harcama limitlerine ulaştıklarında veya önemli finansal olaylar gerçekleştiğinde uyarı almasını sağlayacak bir sistem.
