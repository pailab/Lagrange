---
layout: post
title: "C# Rectangle ve Pen Nedir?"
categories: journal
tags: [C#,Rectangle]
image:
  feature: rectangle.png
  teaser: rectangle.png
  credit:
  creditlink:
---

**Rectangle Yapısı** C# dilinde kolayca dörtgen oluşturmamıza yarar.Bu yazımızda rectangle yapısını nasıl kullancağımızı,
rectangle yapısının üyelerini,özelliklerini ve yapıcı metodunun nasıl oluşturulduğunu inceleyeceğiz.


Öncelikle rectangle yapısını kullanmak istiyorsak projemize *System.Drawing* isim alanını(namespace) eklememiz gerekir.
İsim alanımızı projemize dahil ettikten sonra dörtgen nesnemizi oluşturuyoruz.

```cs
Rectangle dortgen = new Rectangle();
```
Şimdi yarattığımız dortgen nesnemizin konumunu ve ebatlarını belirleyeceğiz.
```cs
dortgen.X = 0;  //Dörtgenimizin X koordinatı
 dortgen.Y = 0; // Dörtgenimizin Y koordinatı
 dortgen.Width = 300; //Dörtgenimizin genişliği
 dortgen.Height = 200; //Dörtgenimizin yüksekliği
```
Yukarıdaki işlemi **constructor** kullanarakta yapabilirdik.
```cs
Rectangle dortgen= new Rectangle(0,0,300,200);
```
Dörtgenimizi Form ekranına çizdirmek için bir grafik nesnesi oluşturuyoruz.
 Graphics nesne_dortgen;

```cs
nesne_dortgen = CreateGraphics();
 nesne_dortgen = CreateGraphics();
```
Grafik nesnemizi oluşturduktan sonra ***Pen*** sınıfından bir kalem oluşturuyoruz.
Dörtgeni ekrana çizdirmek için ise DrawRectangle komutunu kullanıyoruz.
```cs
Pen kalem_dortgen = new Pen(Color.Brown, 6);
 nesne_dortgen.DrawRectangle(kalem_dortgen, 50, 60, 200, 50);
```
![enter image description here](https://i.hizliresim.com/p01kyn.png)

Dörtgenimizin koordinatlarını verdik,boyutlarını ayarladık ve çizdik.
Oluşturduğumuz dörtgenin alanını hesaplamak istersek aşağıdaki metodu kullanabiliriz.
```cs
 public class Rectangle
  {
     public int Width;
     public int Height;

       public int AlanıGetir()
      {
          Hesaplama h= new Hesaplama();
          return h.AlanHesapla(this);
      }
  }   
      public class Hesaplama
     {
         public int AlanHesapla(Rectangle r)
         {
          return r.Width * r.Height;
              }
     }
```

Rectangle yapısının aşağıdaki kullanışlı özellikleri de işinize yarayabilir.
```cs
 //Dörtgenimizin boyutlarını değiştirmemizi sağlayan metot.
 dortgen.Inflate(genislikdegistir, yükseklikdegistir);

 //İki dörtgenin boyutlarını ve konumlarını karşılaştıran metot.
 Equality(Rectangle, Rectangle);

 //Son olarak aşağıdaki şekilde yıkıcı metotumuzu çağırabiliriz
 public class Rectangle
 {
    ~Rectangle(){
      Console.WriteLine("Destructor çağrıldı.");
    }
 }
```
Buraya kadar hep bir dörtgen oluşturmayı ve dörtgen üzerinde değişiklikler yapmayı ve çizmeyi gördük.Peki ya projemiz gereği bir grafik çizmemiz gerekiyorsa ne yapmalıyız?
Şimdi  C# form application  da bir grafik çizeceğiz ve çizdiğimiz bu grafiğin üzerinde çalışacağız.


Grafik çizimi için yine Rectangle yapısında kullandığımız  ***System.Drawing;***  
isim alanımızı(namespace) projemize dahil ediyoruz.
Şimdi bir grafik nesnesi oluşturacağız.
```cs
Graphics grafik_nesne;
 grafiknesne = this.CreateGraphics();
```
Grafik nesnemizi oluşturduk.Şimdi bu grafiğimize çizgi çizmemiz için gerekli olan kalem adında  bir nesne oluşturacağız.Kalem nesnemizi ***Pen*** sınıfından üretiyoruz.
```cs
Pen kalem = new Pen(Color.Blue, 7);
```
Kalem nesnemizin çizgi rengini mavi ve kalınlığını 7 olarak belirledik.

Artık çizgimizi çizebiliriz.Bunun için ***DrawLine***  komutunu kullanıyoruz ve ardından 4 adet parametre veriyoruz.
```cs
grafiknesne.DrawLine(kalem, 100, 100, 100, 200);

```
Artık başlangıç noktası 100,100(X,Y) ve bitiş noktası 100,200(X,Y) olan çizgimizi çizdik.


![enter image description here](https://i.hizliresim.com/j8ZrVD.png)


Şimdi bir koordinat sistemi çizelim.Bu koordinat sisteminde X ve Y eksenlerini belirtelim.
```cs
Graphics x_ekseni;
 x_ekseni= this.CreateGraphics();

 Graphics y_ekseni;
 y_ekseni= this.CreateGraphics();
```
Koordinat sistemimiz için 2 adet grafik nesnesi oluşturduk.

Şimdi yine çizgimizi çizmemiz için kalemimizi oluşturuyoruz.
```cs
Pen eksen_kalem = new Pen(Color.White, 5);
```
Sonra parametreleri doğru bir şekilde verip koordinat sistemimizi oluşturuyoruz.
```cs
x_ekseni.DrawLine(eksen_kalem,90,160,370,160);
 y_ekseni.DrawLine(eksen_kalem, 230, 70, 230, 270);
```

![enter image description here](https://i.hizliresim.com/8MBWJW.png)

Şimdi tek yapmamız gereken çizgilerin uçlarına eksenleri belirleyen X ve Y
harflerini yazmak.
Yazıyı yazabilmemiz için ***Font*** sınıfından bir nesne üretip özelliklerini paremetreler ile veriyoruz.
```cs
Font eksen_yazi = new Font("Tahoma", 17, FontStyle.Bold);
```
Yazımızın rengini ***Brush*** sınıfından bir nesne üreterek belirliyoruz.Biz iki yazı içinde aynı rengi ve özellikleri kullanıcaz.Dilerseniz iki farklı Font ve Brush nesnesi oluşturabilirsiniz.
```cs
Brush yazi_rengi = new SolidBrush(Color.White);
```
Son olarak yazımızı yazmak için ***DrawString*** komutunu kullanıyoruz.
(Çizgilerimizi çizmek için DrawLine komutunu kullanmıştık.)
```cs
x_ekseni.DrawString("X", eksen_yazi, yazi_rengi, 65, 145);
 y_ekseni.DrawString("Y", eksen_yazi, yazi_rengi, 220, 40);
```
![enter image description here](https://i.hizliresim.com/p01kGn.png)

Özetlersek bu yazımızda C# ile kodladığımız bir proje de bir dörtgenin ve grafiğin nasıl oluşturulup çizildiğini öğrenmiş olduk.Hepinize kolay gelsin arkadaşlar.
