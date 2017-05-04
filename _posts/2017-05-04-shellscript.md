---
layout: post
title: "Shellscript Nedir?"
categories: journal
tags: [Shellscript,Linux]
image:
  feature: example.jpg
  teaser: example.jpg
  credit:
  creditlink:
---

Shellscript Nedir?

Shellscriptin ne olduğundan bahsetmeden önce kısaca “shell” nedir onu anlatmam gerek.

Shell: “Shell” Türkçe “Kabuk” anlamına gelmektedir.Kullanıcının yazdığı komutların sistem üzerinde çalışmasını sağlayan kısımdır.Birden fazla kabuk bulunmaktadır örnek vericek olursak:

=>Bornue Shell(sh)

=>Bourne Again Shell(Bash)

=> C Shell

Kısaca shell bu şekildedir.Artık shellscriptden bahsedebiliriz.

Linux altında hızlı ve pratik programlama yapmanın en kısa yolu shellscript ile yapılır.İşletim sisteminin doğal komutlarını çalıştırma ve ek herhangi bir yorumlayıcı istememesi shell script(betik) dilini diğerlerinden ayıran en önemli faktördür. Yazdığınız bir kodu tüm Linux/UNIX sistemlerde kullanabiliriz.Shellscript konsoldan verilen komutları belirli bir düzene uyarak çalıştırmaktan ibarettir.

Shellscriptin Yetenekleri

Çevre Değişkenleri

Aritmetik İşlemler

Diziler

İf yapısı

Case Yapısı

For Döngüsü

While Döngüsü
Shellscript nasıl yazılır?

Herhangi bir metin editörüyle programı yazıp kaydedip çıktıktan sonra yazdığımız programa “chmod +x programismi “şeklinde çalıştırma yetkisi vermemiz gerekir.Bu yetkiyi verdikten sonra “./programismi” yazarak scriptimizi çalıştırabiliriz.

    Değişkenler

Çevre değişkenleri değişken adından sonra “=” işareti yazılarak kurulur;DEGISKENADI=deger

Komut satırında degiskenin adının önüne “$” işareti atılarak da değişkenin değeri okunur.

    Tırnaklar

Tırnaklar kullanılarak katarlar(string) tanımlanır.Bashde üç çeşit tırnak kullanımı vardır.

“ ”(Çift Tırnak)=Çift tırnağın içine yazılan katarda değişken yakalanır ve neye eşitse o yakalanır ama komut yakalanmaz yani komut çalıştırmaz.

‘ ’(Tek Tırnak)=>Ters tırnak içerisinde yazılmış olan katarda değişkenler ve komutlar yakalanıp çalıştırılmaz.

` `(Ters Tırnak)=>Ters tırnak içerisinde yazılmış olan katarda yer alan değişkenler ve komutlar yakalanır ve çalıştırılır.
  ![image](/images/example2.png)![image](/images/example3.png)  
  Aritmetik Operatörler

Kabukta aritmetik işlemler “let” komutuyla yapılır.

“+” ”-” ”\*” “/” işaretleri sırasıyla toplama,çıkarma,çarpma ,bölme işlemleri için kullanılır.Çarpma işlemi için ters bölü işaretinin kullanılmasının sebebi bashin “ * “ özel karakter olarak algılamasından kaynaklandığı içindir.

”%” bölümden kalanı bulmak içindir.

  + ve — teker teker sayiyi azaltmak için kullanılır.
  << >> işleçleri sola ve sağa işlecin sağındaki sayı kadar kaydırma için kullanılır(Örnek:üzerinde işlem yapılan sayıyı ikinin üsleriyle çarpma veya bölmeye karşılık gelir)
  & | bunlarda bildiğimiz mantık operatörlerimizdir.Sırasıyla “Ve” ve “Veya” demektir.
  ![image](/images/example4.png)

  Döngüler ve Koşullar

Burda da “if” koşulu vardır ama burda kullanımı daha farklıdır.Köşeli parantez ve koşul bitişi için “fi” kullanılır.

İf kullanılırken bazı parametreler bize çok yardımcı olur.Bunlar şu şekildedir:


    eq =>eşittir
    -lt =>; küçüktür.
    -gt =>; büyüktür
    -ge =>; büyük eşittir
    -le =>; küçük eşittir

Bunu hemen ufak bir örnekle açıklayalım.
![image](/images/example5.png)

Örnekte kullanmışken bu $1 ve $2 nedir açıklayalım hemen.Bunlar biz dosyamızı çalıştırırken dosyamıza parametre göndermemizi sağlar.$1 ilk parametre $2 de ikinci paremetremizdir.

İf ve while yapısındaki durumlar test komutu ile kullanılmaktadır.

“test ifade” biçiminde kullanılmaktadır.

İfade değerleri de bunlardır:

    f dosya =>Dosya varsa ve türü dosya ise doğrudur.
    -d dosya => Dosya varsa ve türü dizin ise doğrudur.
    -s dosya => Dosya varsa ve boş değilse doğrudur.
    -w dosya => Dosya varsa ve yazılabilir ise doğrudur.
    -x dosya => Dosya varsa ve çalıştırılabilir ise doğrudur.
    -O dosya => Dosya varsa ve sahibi geçerli kullanıcı ise doğrudur.

Kullanımı da test [ ifade dosya ] şeklindedir.Burda parantezlerin içinde bir boşluk bırakmaya dikkat etmelisiniz.

    For Yapısı

Burdaki for yapısı aslında bizim bildiğimiz for yapısından biraz daha farklıdır.

    for isim in kelime (burdaki isim değişkenimizdir)

    do

    komutlar

    done

Burda değişkenimize kelime kümesindeki değerleri sırasıyla isim adlı değişkenimize aktarmaktadır.Kelime kümesindeki değerler bitene kadar do done arasındaki komutlar çalıştırılıcaktır.

    #!/bin/bash
    i=1
    gunler="pazartesi sali carsamba persembe cuma cumartesi pazar"
    for gun in $gunler
    do
            echo "$((i++)).Gün: $gun"
            done

  While Yapısı

While döngüsünde bu durum hemen hemen aynıdır diyebiliriz.

    while durum

    do
                  komutlar
                  done    

Syntax bu şekildedir.

Case


    case  $değişken ismi  in
                  durum1)       
     		           komutlar
                      ...
                      ....
                      ;;
                      durum2)
     		               komutlar
                       ...
                       ....
                       ;;            
                       durum3)       
     		                komutlar
                        ...
                        ....
                        ;;
                        *)              
                        esac

Mantık olarak bildiğimiz case yapısıdır ama syntax olarak biraz farklılık göstermektedir.Örneğin * tüm durumlar olmadığında çalışması gerekeni belirtir yani tüm durumları kontrol eder aslında diyebiliriz.”esac” ise döngümüzü bitirmek için yazmamız gerekir.Bu şekilde havada kalabilir o yüzden hemen basit bir örnekle açıklayalım.

  #!/bin/bash
    while true
    do
    echo "ls:1"
    echo "rm -rf:2"
    echo "date:3"

    echo "Çalıştırmak istediğiniz komutun numarasını giriniz:"
    read kom

    case $kom in
            1)echo `ls` ;;
            2)echo `rm -rf` ;;
            3)echo `date` ;;
            *)echo "Bu numarada komut yoktur" ;;
            esac
            done

Shellscript ile ilgili ilk aklıma gelenler şimdilik bu şekilde bir sonra ki yazıda devamı gelicek.Görüşmek üzere
