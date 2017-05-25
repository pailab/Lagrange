---
layout: post
title: "Programlama Tipleri"
categories: journal
tags: [Types, Programming]
image:
  feature: types.jpg
  teaser: types.jpg
  credit:
  creditlink:
---
Statik tip harika çünkü sizi sıkıntıdan kurtarıyor. Dinamik tip harikadır çünkü yol dışına çıkıyor ve çalışmalarınızın daha hızlı yapılmasını sağlıyor. Güçlü ve dinamik olarak yazılan diller arasındaki tartışma devam eder, ancak konunun anlaşılması weak (zayıf) tip ve C gibi diller ile başlar.
<!--more-->

C her şeyi bir sayı gibi görür. 'D' karakteri, 7 veya % sembolü onu temsil eden ASCII sembolünün sayısıdır. Bool olarak da "True" ve "False", 1 ve 0'ı temsil eder.
C dilinde değişkenler integer için **int**, karakterler için **char** gibi tiplerle tanımlanır fakat bu sadece ne kadar bellek kullanacağını ifade eder. Değişkenlere erişmem ve çıktı alabilmem için onun tipini bilmem gerekir.

```c
int a = 1;
 printf("Numara: %in", a);
 char z = 'z';
 printf("Karakter : %cn", z);
```
Bu kod bloğunu çalıştırdığımda şu şekilde çıktı gösterir.
```
Numara: 1
 Karakter : z
```
**printf** fonksiyonu değişken tipi hakkında bilgi vermedikçe yanlış çıktılar üretebilir. Mesela şu şekilde yazarsak:
```c
char z = 'z';
 printf("Karakter : %in", z);
```
çıktısı da şu şekilde olur:
```
Karakter : 122
```
**C** dili z'nin bir karakter mi veya integer mı olduğunu bilmiyor. Bu yüzden weak(zayıf) tip'e sahip bir dil.

**Weak (zayıf)** tipleme hızlıdır. Çünkü düşündüğünüzde dilin farklı tipler arasında herhangi bir hatırlama yapmadığını ve bu yüzden vakit kaybetmediğini farkedersiniz. Fakat gördüğümüz gibi hızın yanında hataları da yanında getiriyor.

Şimdiye kadar, zayıf tipten bahsettik. "Weak (zayıf) karşı strong(güçlü)" ve "Static(statik)e karşı dynamic(dinamik)" genellikle eşanlamlı olarak söylenir, ancak her biri aynı sorunun farklı bir aşamasını tanımlar. Zımni(ima ile) bir değer yargılama sözcükleri ile de politize olmuşlardır.

 "Weak(Güçsüz) ve strong(güçlü)", bir tanesini diğerinden daha iyi hale getirirken, "statik ve dinamik" birinin sıkıcı ve diğerinin heyecan verici olmasına neden olur.
Bu iki terim birbirinin yerine kullanılır, ancak bir dilin tür tanımlama şekli ve program çalıştığında şekilleri nasıl tanımladığı arasındaki farkı tanımlarlar. Aşağıdaki tabloda da bunlara örnekler var.

| Tiplemeler                     | Açıklama                                                                                                                                                                                                                                                                                        |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Zayıf - tipsiz                              | Assembly gibi diller herhangi bir tip belirtmez. Her şey bir sayıdan ibarettir.                                                                                                                                                                                                                 |
| Zayıf statik tipleme  | C, nesne türlerini yapılar olarak tanımlamanıza izin verir, ancak bunları uygulamak veya hatırlamak için fazla bir şey yapmaz. C otomatik olarak birçok tür arasında dönüştürme. C ++ ve Objective-C tanımlarla birlikte ilerlemekle birlikte yine de sonuçta ortaya çıkan türleri zorlamazlar. |
| Güçlü statik tipleme  | Java her türü tanımlamanızı zorlar ve bunları bir sanal makine ile denetler.                                                                                                                                                                                                                    |
| Güçlü dinamik tipleme | Python, JavaScript ve Ruby, nesneleri tanımlamanıza zorlamak yerine dinamik olarak çıkarır ve program yorumlayıcıda çalıştığında bu türleri zorlar. Dinamik olarak yazılan tüm diller, çalışma zamanında güçlü bir yazım sistemi gerektirir; aksi takdirde nesne türlerini çözemezler.          |
| Zayıf dinamik tipleme | Dinamik olarak düşünülen türler, zayıf olarak yazılan bir dilde çalışmaz çünkü çıkarmak için herhangi bir tür yoktur.                                                                                                                                                                           |

Hiç bir programlama dili yukarıdaki tanımlardan hiç birine tamamen uymaz. [Sebebi...](https://www.youtube.com/watch?v=hh7gQhNFzlc)

Java en statik dillerden biri olarak kabul edilmekle birlikte, çalışma zamanında sınıfları değiştirmenize, dolayısıyla daha dinamik dillere benzeyen kapsamlı bir yansıma API'sı uygulamaktadır. Bu özellik, Java Virtual Machine'in Groovy gibi çok dinamik dilleri desteklemesine olanak tanır.

**Lisp**, **Erlang** ve **Haskell** gibi işlevsel programlama dilleri satırları daha da bulanıklaştırıyor.


## Zayıf Statik Diller: C, C++ ve Objective-C
Bu programlama dilleri, dilin gevşek doğasını iyileştirmek için C işlevinin bir alt kümesini ve katı yönergelerini kullanır. C ++ ve Objective-C, C ile aynı bytelara derlenir, ancak yazabileceğiniz kodu kısıtlamak için derleyiciyi kullanırlar.

C ++ ve Objective-C'de, sayımız (1229799107) bir anlam taşıyor. Bir karakter dizisi olarak tanımlayabilir ve kimsenin bir para birimi veya tarih olarak kullanmadığından emin olabilirim. Derleyici düzgün kullanımını zorlar.

Statik yazım(typing), nesneleri her zaman iyi tanımlanmış bir şekilde çalışan işlevsellik kümeleri ile destekler. Şimdi bir Person nesnesi oluşturabilir ve getName işlevinin her zaman birisinin adının dizesini döndürdüğünden emin olabilirim.

```c
class Person {
    public:
        string getName() {
            return "Mustafa Oluc";
        }
};
```
Ve nesnemi şu şekilde çağırabilirim:

```c
Person p;
 printf("İsim : %sn", p.getName().c_str());
```

## Güçlü Statik Diller: JAVA

C ++, C'yi kullanmanın daha sıkı yollarını sunar. Java onları kullandığınızdan emin olmaktadır. Java, tanımlamak için her şeye ihtiyaç duyar; böylece hangi nesne tipine sahip olduğunuzu, nesnenin hangi fonksiyonları olduğunu ve bunları doğru bir şekilde çağırdığınızdan emin olabilirsiniz.

Java, C kodunu ve statik yazımdan çıkmanın diğer yollarını desteklemeyi de bıraktı.

Aynı Person nesnesi Java'da şu şekildedir:

```java
public class Person {
    public String getName() {
        return "Mustafa Oluc";
    }
}
```
Ve nesneyi çağırmam da şu şekilde:

```java
public class Main {
    public static void main (String args[]) {
        Person person = new Person();
        System.out.println("İsim : " + person.getName());
    }
}
```
Bu kod, yeni bir `Person` nesnesi oluşturur, bu adını `person` adlı bir değişkene atar, `getName` işlevini çağırır ve değeri yazdırır.

**Java sınıfın dışındaki kodlara izin vermiyor**. İnsanlara, Java'nın sizi çok fazla özet yazması için zorlaması nedeniyle şikayet etmesinin önemli bir nedeni var.

Java popülerliği ve güçlü yazmaya olan bağlılığı programlama camiasında (sanki spor programı sunuyoruz😃) üzerinde büyük etki yarattı. Güçlü tip yazan taraftarlar, çatlakları C ++ 'da gidermek için övdü. Ancak birçok programcı, Java'yı aşırı derecede kuralcı ve katı buldu. Java ekstra tanımı olmadan kod yazmanın hızlı bir yolunu istediler.


## Güçlü Dinamik Diller: Ruby, Python, Javascript ve dahası..
**JavaScript**'te, `int` veya `char` gibi bir tür yerine bir anahtar kelime `var` ile bir değişken tanımladım. Bu değişkenin türünü bilmiyorum ve aslında ona erişmek isteyene kadar buna ihtiyacım yok.

Javascriptte yine getName diye bir fonksiyon oluşturursak:

```javascript
var person = {
    getName: function() {
        return 'Mustafa Oluc';
    }
};

alert('İsim : ' + person.getName());
```

Bu kod, `person` adlı bir değişken oluşturur ve bir `getPerson` işlevine sahip bir nesneye atar, ancak bu değişkeni 5 sayısına yeniden atar. Bu kod çalıştırıldığında, sonuç `TypeError`'dır: Nesne 5'in '**getName**' yöntemi yoktur. JavaScript nesne 5'in `getName` adlı bir işleve sahip olmadığını söylüyor. Java'da derleme sırasında bu hata ortaya çıkıyor, ancak **JavaScript çalışma zamanı için bekletiyor.**

Ayrıca, aynı şekilde programın koşullarına dayanarak nesnenin türünü de değiştirebilirim.

```javascript
var person = {
    getName: function() {
        return 'Mustafa Oluc';
    }
};

if (new Date().getMinutes() > 29) {
    person = 5;
}

alert('İsim : ' + person.getName());
```
Şimdi bu kod 9: 15'te çalışacak, ancak saat 9: 30'da başarısız olacak. Java bunu bir **tür(type) hatası** olarak adlandırır, ancak JavaScript'te sorun yoktur.

Kodun, türü belirlemek için çalışma zamanında nesneye baktığı ve "ördek gibi vakladığı ve ördek gibi yürüdüğü için ördek olmalı" dendiği için, dinamik yazmanın en popüler şekli **"Ördek Yazımı" (Duck Typing)** olarak adlandırılır.

Duck typing, programın ortasındaki herhangi bir nesneyi yeniden tanımlamanıza izin verir. Ördek gibi başlayıp kuğu veya kaz haline dönüşebilir.

```javascript
var person = {
    getName: function() {
        return 'Mustafa V. Oluc';
    }
};

person['getBirthday'] = function() {
    return 'Ocak 1';
};

alert('Isim : ' + person.getName() + ' ' +
      'Dogum Gunu : ' + person.getBirthday());
```

## Peki Hangisi Daha İyi?

Dinamik kod genellikle statik koddan daha kısadır, çünkü kodun ne yapacağına dair daha az açıklama gerekir.

Peki hangisi?

|Statik Programcıların dedikleri          | Dinamik Programcıların dedikleri                                                                                                                                                                                                                                                                                        |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| "Statik tip, derleyiciyle hatalar yakalar ve sizi sıkıntıdan kurtarır."        | "Statik tip yalnızca bazı hatalar yakalar ve derleyiciye testlerinizi yapacak kadar güvenemezsiniz. "                                                                                                                                                                                                                 |
| "Statik dillerin okunması daha kolaydır, çünkü kodun ne işe yaradığını açıkça ortaya koymaktadırlar."  | "Dinamik dillerin okunması daha kolaydır, çünkü daha az kod yazarsınız." |
| "En azından kodun derlendiğini biliyorum."  | "Kod sadece derlenmesi çalıştığı anlamına gelmez."                                                                                                                                                                                                              |
| "Ekibimin iyi bir kod yazdığından emin olmak için statik yazmaya güveniyorum." | "Derleyici kötü kod yazmanıza engel değil."          |
| "Bilinmeyen bir nesnenin hata ayıklanması imkansızdır."                                                                                                                                                                           | "Aşırı karmaşık nesne hiyerarşilerinde hata ayıklama hiç çekilmez." |


Statik yazım, `Person` nesnenizi anlamayı kolaylaştırdı. Bir `Person`'ı bir isimle tanımladık ve hangi alanların vaktinden önce anlaştığına karar verdik. Her şeyin kurulması açıkça `Person`ımızı hata ayıklamayı kolaylaştırır, ancak değiştirmek daha zorlaşır.

Başvurumuzdaki birisi **ikinci bir e-posta adresine ihtiyaç duyarsa ne olur?** Statik bir dilde, çoğu insanın bilmese de herkesin iki e-posta adresine sahip olması için nesneyi yeniden tanımlamamız gerekir. Bir doğum gününde, favori renginde ve birkaç öğe ekleyin ve her `Person`'ın ihtiyaç duyduğu alanın iki katı kadar alanına sahip olursunuz.

**Dinamik diller bu sorunun daha kolay olmasını sağlar**. Bir `Person`'a herkesi eklemeden ikinci bir e-posta alanı ekleyebiliriz. Şimdi, her nesnenin yalnızca ihtiyaç duyduğu alanlar vardır. Statik bir dil, bunu kapsamlı bir değer haritasıyla idare edebilir, ancak o zaman dinamik kodu yazmak için statik ortamla savaşıyorsunuz demektir. C programcıları, tip dönüşümlerinde hatalar, bozuk değerler ve küçük yazım hatalarından kaynaklanan berbat hatalar yüzünden saçlarını yolarak yıllarını harcadılar..

## Sonuç
Kesin bir sonuç yok. Dinamik olarak yazılan diller şimdi popüler. Sarkaç önümüzdeki yıllarda ileri geri sallanacak bilemeyiz tabi. Tek çözüm esnekliktir. Her bir ortamda çalışmayı öğrenin ki herhangi bir ekiple iyi çalışabilesiniz..
