---
layout: post
title: PIC16F877 ile Gömülü Sistemler Deneyimlerim 
categories: [pic,mikrodenetleyici,gömülüsistemler] 
---     

PIC mikrodenetleyicilerle tanışmam, gömülü sistemler üzerine staj yapmam ile başladı. Gömülü sistemler ile öncesinde çalışmalarım olsa da eksiklerim oldukça fazla. Bu sebeple temel bilgilerimi tazeleyerek gidiyorum. Bu yazıda PIC16F877 üzerinden öğrendiğim temel konuları, karşılaştığım sorunları ve geliştirdiğim uygulamaları paylaşmak istiyorum.

---

PIC, Microchip firması tarafından üretilen, gömülü sistemlerde sıklıkla kullanılan bir mikrodenetleyici ailesidir. Benim kullandığım model PIC16F877. İlk aşamada yani öğrenme ve pratik yapma aşamasında simülasyon üzerinden ilerliyorum. CCS C derleyicisini kullanarak yazdığım kodları Proteus üzerinde çizdiğim devreler ile simüle ediyorum.  

PIC16F877 Özellikleri:
8-bit yapı
33 Giriş/Çıkış pini
ADC modülü
Timer’lar
Seri iletişim modülleri (USART, I2C, SPI)
EEPROM ve FLASH memory

Derleyici olarak PIC mikrodenetleyiciler için geliştirilen CCS C Compiler kullandım. Kullanımı kolay ve anlaşılır arayüzü ile işimi fazlasıyla kolaylaştırdı. Yazdığım kodların derlenmesi ve hex dosyasının oluşturulması da oldukça hızlı ve sorunsuz gerçekleşti.

Devreleri fiziksel olarak kurmadan önce Proteus ile test etmek bana hem zaman kazandırdı hem de hata riskini azalttı. Simülasyon yaparken Proteus ortamının eksiklikleri veya yanlış çalıştığı yerler konusunda da bazı gözlemlerim oldu. Bu noktalarda yazdığım kodda hata yaptığımı veya devreyi yanlış kurduğumu düşünerek yaptığım her adımı daha derinlemesine araştırdım ve daha iyi öğrendim. İnceledikçe simülasyonun yaptığı hataları fark ettim. 

PIC üzerinden çalışırken anlamadığımı sonradan fark ettiğim bir nokta hafıza birimleri idi. Başta “RAM mi, FLASH mı, EEPROM mu?” gibi kavramlar arasında net bir ayrım yapamıyordum. Zamanla şunu öğrendim:

FLASH bellek, program kodlarının tutulduğu kalıcı hafızadır.
RAM, çalışma anında geçici olarak verilerin saklandığı bellektir. (değişkenler vb)
EEPROM, küçük boyutlu verilerin (örneğin sayaç değeri, ayarlar vs.) güç kesilse bile kalıcı olarak saklanabildiği birimdir.

Giriş/Çıkış (I/O) Portları
Başta çok basit görünen bu konu, zamanla ne kadar hassas olduğunu gösterdi. set_tris_x() komutu ile portların yönü (giriş/çıkış) ayarlanmalı.

```bash
set_tris_b(0b11111110); 
output_high(PIN_B0);    
```
Bu kod ile B portunun ilk pinini çıkış olarak ayarlıyoruz. Ardından B0 pinini 1 yani high yapıyoruz. 

Timer
Timer, mikrodenetleyici içinde yer alan ve zamanı sayan bir donanım modülüdür. Ana amacı, belirli bir süre sonunda olay tetiklemek veya zaman ölçümü yapmaktır.
Zamanlamanın önemli olduğu devrelerde Timer ile örnekler yaptıkça Timer yapısına bakış açım değişti. Başlarda delay ile her şeyi halledebileceğimi ve Timer'a gerek olmadığını düşünürüyordum. Sonrasında delay ile mikrodenetleyiciyi nasıl boş durumda bıraktığımı ve delay fonksiyonu işlemdeyken başka işlemler yapamadığımı farkettim. Bu gibi durumlarla timer kullanımının mantığını kavradım.

```bash
#include <16F877.h>
#fuses XT, NOWDT, NOPROTECT, NOBROWNOUT, NOLVP, NOPUT, NOWRT, NODEBUG, NOCPD
#use delay(clock=4000000)        // 4 MHz kristal kullanılıyor
#use fast_io(b)                  

int i = 0;

#int_timer0
void timer0_kesme() {
   set_timer0(60);   // Taşma noktasına ulaşması için başlangıç değeri
   i++;

   if (i == 10) {
      output_high(PIN_B0);
   }

   if (i == 20) {
      output_low(PIN_B0);
      i = 0;
   }
}

void main() {

   // Port B çıkış olarak ayarlanır
   set_tris_b(0x00);
   output_b(0x00); // Başlangıçta tüm çıkışlar sıfır

   // Timer0 ayarları
   setup_timer_0(RTCC_INTERNAL | RTCC_DIV_256);
   set_timer0(60); // Timer0 başlangıç değeri

   // Kesmeleri aktif et
   enable_interrupts(INT_TIMER0);
   enable_interrupts(GLOBAL);

   while (1) {
   }
}

```

Kesme (Interrupt)
Kesme, mikrodenetleyici çalışırken, belirli bir olay gerçekleştiğinde işlem akışını durdurup, önceden belirlenmiş bir fonksiyona geçmesini sağlayan mekanizmadır. Kesme bitince işlem, kaldığı yerden devam eder. Bu yapının dış dünyadan gelen olaylara anında tepki vermek için çok etkili bir yöntem olduğunu gördüm.

```bash
#include <16F877.h>  // Kullanılacak denetleyicinin başlık dosyası
#fuses XT, NOWDT, NOPROTECT, NOBROWNOUT, NOLVP, NOPUT, NOWRT, NODEBUG, NOCPD
#use delay(clock=4000000)  // 4 MHz kristal için
#use fast_io(b)

 #int_RB
void B_degisiklik(){
   if(input(pin_b4))
      output_high(pin_b0);
   if(input(pin_b5))
      output_high(pin_b1);
   if(input(pin_b6))
      output_high(pin_b2);
   if(input(pin_b7))
      output_high(pin_b3);
      
   delay_ms(2000) ;
   output_b(0x00);
   
   //disable_interrupts(INT_RB);
}

void main() {
 
   set_tris_b(0xF0);
   output_b(0x00);
   
   enable_interrupts(INT_RB); 
   enable_interrupts(GLOBAL);
   
   while(1);
}
```

<img src="/images/kesme2.png" alt="interrupt" width="full">


<img src="/images/lcdtus.png" alt="lcd" width="full">



Sonuç: Öğrendiklerimin Bende Bıraktığı Etki
PIC ile çalışmak bana donanım-yazılım etkileşimini derinlemesine kavrama fırsatı verdi. Sadece kod yazmak değil, devreyi kurmak, simülasyon yapmak, zamanlamaları doğru ayarlamak gibi pek çok disiplini bir arada deneyimledim.

Geriye dönüp baktığımda, en çok fayda gördüğüm şey, her yeni konuda mutlaka küçük bir uygulama yapmam oldu. Uygulamaya dökülmeyen bilgi ne yazık ki akılda kalmıyor.
