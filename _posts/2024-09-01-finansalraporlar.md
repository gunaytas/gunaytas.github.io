---
layout: post
title: Finansal Raporlar 
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

<img src="/images/wireframe1.png" alt="mockup" width="300">

![mockup](/images/wireframe1.png?width=300) 
![mockup](/images/liste.png?width=300) 

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

![tasarım](/images/anasayfa.png?width=200) 
![tasarım](/images/image.png?width=300) 

#### **5. Veritabanı Bağlantısı**
Veritabanı bağlantısını Rails’in Active Record özelliğiyle kolayca yaptım. Bir örnek migration dosyası:
```ruby
class CreateTasks < ActiveRecord::Migration[6.1]
  def change
    create_table :tasks do |t|
      t.string :name
      t.text :description
      t.boolean :completed, default: false

      t.timestamps
    end
  end
end
```

#### **6. API Testleri**
Postman aracılığıyla oluşturduğum API’leri test ettim. Özellikle CRUD işlemlerini doğrulamak ve doğru verinin döndüğünden emin olmak için Postman oldukça faydalı oldu.

#### **7. Kullanıcı Deneyimi**
Kullanıcıların listeye veri ekleyip düzenleyebilmesi için şık bir form tasarladım. Formun tasarımı ve işlevselliği hem Tailwind hem de Rails’in yardımıyla oldukça kolay bir şekilde tamamlandı.
---


### Sonuç ve Öğrendiklerim
Bu proje, Ruby on Rails ile neler başarabileceğimi görmek açısından harika bir deneyim oldu. Aynı zamanda öğrendiklerimi pekiştirebildiğim güzel bir örnekti. Rails’in sunduğu kolaylıklar ve Tailwind’in tasarım sürecindeki etkisi birleşerek işlevsel ve şık bir uygulama ortaya koymamı sağladı.
