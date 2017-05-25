---
layout: post
title: "C# Control Sınıfı Nedir?"
categories: journal
tags: [C#,Control,Class]
image:
  feature: control3.png
  teaser: control3.png
  credit:
  creditlink:
---
Bu yazımızda c# kontrol sınıfını inceleyeceğiz. buton ,textbox, label gibi form araçları oluşturup bu araçları  konsol ekranında düzenleyeceğiz.
 Konsolda yazdığımız kodlarla da form ekranı elde etmeye çalışacağız.

 İlk olarak form araçlarını kullanabilmemiz için projemize **System.Windows.Forms** isim alanını
eklemek zorundayız.Namespace ekledikden sonra   "frm"  adında bir form  nesnesi oluşturuyoruz.
Ve formumuza bir isim veriyoruz.
```cs
Form frm = new Form( );//frm nesnemiz..
frm.Text = "PROGRAMLAMA";//form ekranımıza isim verdik..
```
Eğer istirsek form ekranımızın arka planınıda renklendirebiliriz.Bunu yapmak için **System.Drawing**
isim alanını eklemek zorundayız.bu namespace sayesinde renklendirme işlemlerini yapabiliriz.
```cs
frm.BackColor = Color.Yellow;//arka planımıza sarı rengini verdik..
```
Oluşturduğumuz formu programı çalıştırdığımız zaman görüntülemek için aşağıdaki komutu kullanıyoruz.
```cs
Application.Run(frm);
```
![enter image description here](https://i.hizliresim.com/AL9yD7.png)
Programı çalıştırdığımız zaman form ekranıyla beraber consol ekranıda açılacaktır.Consol ekranını kapatmak için şu yolu izliyoruz:

1) Projemize sağ tıklıyoruz.

2) Tıkladıkdan sonra en altta bulunan properties'i seçiyoruz.

3) Karşımıza çıkan ekrandan output type'a tıklıyoruz.

4) Ve windows application'u seçiyoruz

Artık karşımıza sadece form ekranımız çıkacaktır.Şimdi form ekranımıza **TextBox** ekleyelim.bunun için " txt " adında bir textbox  nesnesi oluşturuyoruz.
```cs
TextBox txt = new TextBox();
```
Textbox 'ımızı şekillendirme işlemine başlıyoruz .
```cs
txt.Location = new Point(90,90);//textbox'ın konumunu belirttik.
frm.Controls.Add(txt);//txt nesnemizi form ekranımıza ekledik.
```
![enter image description here](https://i.hizliresim.com/YDYOB2.png)

Şimdi ise Textbox'ımızın altına bir buton ekleyelim.Bunun için " btn " adında bir button nesnesi oluşturuyoruz.
```cs
Button btn = new Button();
```
Butonumuzu şekillendirmeye başlıyoruz.
```cs
btn.Location = new Point(100,120);//butonumuzun konumunu belirledik.
btn.Text = "Kaydet";//butonun üzerinde yazılacak yazıyı belirledik.
btn.BackColor = Color.Red;//butonun rengini belirledik.
frm.Controls.Add(btn);//butonumuzu form ekranımıza ekledik.
```
![enter image description here](https://i.hizliresim.com/37mpRA.png)

Form ekranımızıın görsellik açısından güzel gözükmesi ve daha açıklayıcı bi ekran olması için TextBox'ımızın üstüne bir label ekleyelim.

Yukarıda yaptığımız nesne oluşturma işlemleri gibi " lbl " adında bir **Label** nesnesi oluşturuyoruz.
```cs
Label lbl = new Label();
```
Labelımızı şekillendirmeye başlıyoruz.
```cs
lbl.Location = new Point(100,65); //label'imizin konumunu belirledik.
lbl.Text = "E-POSTA";//label'imize bir text ekledik.
lbl.Font = new Font("Georgia",13);//yazı tipimizi ve boyutumuzu belirledik.
frm.Controls.Add(lbl);//label ' i form ekranına ekledik.
```
![enter image description here](https://i.hizliresim.com/yEBzLN.png)
Consol ekranından form oluşturmak bu kadar basit. Bir daha ki yazımızda görüşmek üzere.
