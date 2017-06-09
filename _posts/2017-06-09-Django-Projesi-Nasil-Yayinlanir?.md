---
layout: post
title: "Bir Django Projesi Sıfırdan Nasıl Yayınlanır?"
categories: journal
tags: [Python,Django,Linux,Nginx,Gunicorn,Supervisor]
image:
  feature: django.png
  teaser: django.png
  credit:
  creditlink:
---
Selamlar.

Bu yazımda django ile yazılmış bir uygulamayı sıfırdan nasıl deploy edebiliceğimizi onu anlatıcam.Hadi başlayalım.

Ben uygulamayı yayınlamak için Ubuntu 16.04, Nginx, Gunicorn,Git ve Supervisor kullanıcam.

İlk olarak DigitalOceandan 10 dolarlık ufak bir server satın alıyoruz.
![DigitalOcean](../images/digitalocean.gif)


Gif'de gösterilen adımları kendimize göre uygulayarak yeni bir droplet oluşturuyoruyoruz.

Gİf de ki adımları sorunsuz yaptıysak resimdeki gibi bir ekranla karşılaşmalıyız.
![DigitalOcean](https://i.hizliresim.com/j8d17j.png)
Digital Ocean'a kayıt olurken kullandığımız gmail hesabımıza root kullanıcısı için geçici bir parola yollanır ve bu tek kullanımlık bir paroladır.Bu sunucuya bağlandıktan sonra değiştirilir.Eğer herhangi bir UNİX türevi kullanıyorsanız SSH ile sunucuya bağlanabilirsiniz.Eğer windows kullanıcısıysanız Putty kullanarak ssh ile bağlanabilirsiniz veya
DigitalOceanın konsolunu da kullanabilirsiniz.
```cs
ssh root@<ipadresiniz>
```
Komutunu yazdıktan sonra bizden tek kullanımlık parolayı girmemizi istenicek.Bunu doğru girdikten sonra otomatik olarak parolanızı değiştirmeniz istenicek.Güvenilir unutamayacağınız bir parola ile değiştiriyoruz.
Sunucuyu yeni açtığımız için güncellenmesi gereken paketler olabilir bu yüzden ilk olarak;
```cs
sudo apt-get update
sudo apt-get -y upgrade
```
komutlarını çalıştırarak paketleri güncelliyoruz.
Artık Django uygulamamızı kurmak için gerekli programları kurmaya başlayabiliriz.
<h3>PostgreSQL</h3>
İlk olarak Python/Django'da PostgreSQL kullanmak için gerekli bağımlılıkları kuruyoruz.
```cs
sudo apt-get -y install build-essential libpq-dev python-dev
```
Gerekli bağımlılıkları kurduktan sonra PostgreSQL Serverımızı kuruyoruz.
```cs
sudo apt-get -y install postgresql postgresql-contrib
```
<h3>NGINX </h3>
Bir proxy arkasında Django uygulamamızı koşturabilmemiz için nginx kuruyoruz.
```cs
sudo apt-get -y install nginx
```
<h3>SUPERVISOR</h3> 
Sunucumuzun crash olması ya da reboot edilmesi durumunda projeyi tekrar ayaklandırması için supervısor kuruyoruz.
```cs
sudo apt-get -y install supervisor
```
Şimdi supervisorı enable hale getirip çalıştırmaya başlatıyoruz.
```cs
sudo systemctl enable supervisor
sudo systemctl start supervisor
```
<h3>Python Virtualenv</h3>
Django uygulamamızı daha iyi yönetebilmemiz için sanal ortamımız içinde bulundurucaz bu yüzden virtual enviromentımızı kuruyoruz.
```cs
sudo apt-get -y install python-virtualenv
//python3 kullananlar için:
sudo apt-get -y install python3-virtualenv
```
<h3>PostgreSQL  Ayarları</h3>
Kullanıcı değiştiriyoruz:
```cs
su - postgres
```
Şimdi veritabanımız için bir kullanıcı yarattıktan sonra uygulamamız için de bir veritabanı oluşturuyoruz.
```cs
createuser d_volkan
createdb volkandb_prod --owner volkan
psql -c "ALTER USER volkan WITH PASSWORD '123'"
exit
```
Veritabanı ayarlarımızı tamamladık "exit" komutuyla çıkış yapıyoruz ve root kullanıcımıza geri dönüyoruz.Şimdi sunucumuzda kendimize bir kullanıcı yaratıyoruz.
```cs
adduser volkan
```
volkan isimli kullanıcımızı yaratırken bize sorulan soruları da cevapladıktan sonra kullanıcımızı oluşturuyoruz. 
```cs
Adding user "volkan" ...
Adding new group "volkan" (1000) ...
Adding new user "volkan" (1000) with group "volkan" ...
Creating home directory "/home/volkan" ...
Copying files from "/etc/skel" ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for volkan
Enter the new value, or press ENTER for the default
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n] 
```
Kullanıcımızı sudoers dosyasına kaydediyoruz.
```cs
gpasswd -a volkan sudo
```
Yeni oluşturduğumuz kullanıcıya geçiyoruz.

```cs
su - volkan
```
<h3>Python Virtualenv Ayarları </h3>
Oluşturduğumuz kullanıcının home dizinine gidiyoruz ve sanal ortamımızı oluşturuyoruz.
```cs
cd /home/volkan
virtualenv .
```
Aktif hale getiriyoruz.

```cs
source bin/activate
```
Ufak bir proje olduğu için githubdan direk bu şekilde projemizi alıyorum ama büyük bir proje olsaydı git archive kullanmamız gerekirdi.
```cs
git clone https://github.com/olucvolkan/volkanoluc-blog.git
```
Hemen hemen resimdeki gibi bir görüntü olmalıdır.(log ve run dizinlerini ilerleyen kısımlarda oluşturucaz)
![](https://i.hizliresim.com/5gbEzl.png)
Uygulamamızın olduğu klasöre geçiyoruz ve django uygulamamız için oluşturduğumuz requirements.txt dosyasındaki paketleri pip yardımıyla kuruyoruz.
```cs
cd volkanoluc-blog
pip install -r requirements.txt
```
Gerekli paketleri pip aracılığıylada kurduktan sonra settings.py dosyamızda gerekli ayarlamaları yapıyoruz.
```cs
DATABASES = { 'default':
{ 'ENGINE': 'django.db.backends.postgresql_psycopg2',
'NAME': 'volkandb_prod',
'USER': 'volkan',
'PASSWORD': '123',
'HOST': 'localhost',
'PORT': '', } }
```
Django projenizde default olarak sqlite tanımlıdır ama djangonun bize sağladığı güzelliklerden biri de postgresql in de ön tanımlı olmasıdır.Ben projemde postgresql kullanıcağım için settings.py dosyasını bu şekilde düzenliyorum.Database için gerekli ayarlamalarıda yaptıktan sonra migrate ediyoruz.

```cs
python manage.py migrate
```
Collectstatic komutuyla bütün static dosyalarımızı toparlıyoruz.
```cs
python manage.py collectstatic
```
Buraya kadar bir sıkıntı çıkmadıysa development serverda  uygulamamızı ayaklandırabiliriz.
```cs
python manage.py runserver 0.0.0.0:8000
```
 Uygulamanız bu şekilde bir sorun çıkmadan çalıştıysa bir sıkıntı yok diyerek CONTROL-C yaparak development serverımızı durduruyoruz ve Gunicorn ve Nginx kurarak uygulamamızı ayaklandırıyoruz.
<h3>Gunicorn</h3>
İlk önce gunicornu pip yardımıyla kuruyoruz.
```cs
pip install gunicorn
```
Gunicornu kurduktan sonra virtualenv da ki bin dizinimizin altında bin/gunicorn_start dosyamızı oluşturuyoruz.
```cs
vim bin/gunicorn_start
```
Oluşturduğumuz dosyanın içine aşağıdaki ayarları ekliyoruz.
```cs
#!/bin/bash
NAME="appimizin adını yazıyoruz"
DIR=/home/volkan/volkanoluc-blog -->uygulamamizin bulundugu dizin
USER=volkan
GROUP=volkan
WORKERS=3
BIND=unix:/home/volkan/run/gunicorn.sock /burasi asagida detayli aciklanicak
DJANGO_SETTINGS_MODULE=NewBlog.settings
DJANGO_WSGI_MODULE=NewBlog.wsgi
LOG_LEVEL=error
cd $DIR
source ../bin/activate
export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
export PYTHONPATH=$DIR:$PYTHONPATH
exec ../bin/gunicorn ${DJANGO_WSGI_MODULE}:application \
--name $NAME \
--workers $WORKERS \
--user=$USER \
--group=$GROUP \
--bind=$BIND \
--log-level=$LOG_LEVEL \
--log-file=- :
```
BIND kısmında gunicorn çalıştığı zaman otomatik olarak run klasörünün alrında gunicorn.sock isimli bir socket dosyası oluşturmaktadır.

Şimdi bu gunicorn_start dosyamıza çalıştıralabilir hale getiriyoruz.

```cs
chmod u+x bin/gunicorn_start
```
Az önce bahsettiğimiz socket dosyamızın oluştuğu run klasörünü oluşturuyoruz.
```cs
mkdir run
```
Buralarda eğer bir hata alırsanız dosya izinlerini kontrol etmenizi önerim :)
<h3>SUPERVISOR KONFİGURASYONLARI</h3>
Şimdide supervisor'ı gunicornu otomatik olarak çalıştırması için gerekli ayarları yapıcaz.
İlk olarak logları tutucağımız bir dizin oluşturuyoruz.
```cs
mkdir logs
```
Dizini oluşturduktan sonra gunicorn da alınabilcek hataları kaydediceğimiz bir log dosyası oluşturuyoruz.
```cs
touch logs/gunicorn-error.log
```
Şimdi de supervısor için yeni bir konfigürasyon dosyası yaratıyoruz.
```cs
sudo vim /etc/supervisor/conf.d/NewBlog.conf
```
Ve konfigürasyon dosyamızı aşağıda ki gibi oluşturuyoruz. 
```cs
[program:NewBlog]
command=/home/volkan/bin/gunicorn_start
user=volkan
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/home/volkan/logs/gunicorn-error.log
```
Bu arada görüldüğü üzere supervısor kullanarak otomatik olarak gunicor_start scriptini tetikleyerek gunicornu çalıştırmaya başlatıyoruz.
```cs
sudo supervisorctl reread
sudo supervisorctl update
```
Yukarı da ki komutlarla supervisorı projemiz için güncelledikten sonra  aşağıdaki komutla duruma bakıyoruz.Burda sorun yaşıyorsanız hemen açıp loglara bakmalısınız.
```cs
sudo supervisorctl status NewBlog
NewBlog                          RUNNING   pid 1454, uptime 7 days, 23:59:11
```
Hata almadığınızı düşünerek devam ediyorum. Supervisorı gunicorn'a göre ayarladıktan sonra şimdide nginx'in konfigürasyonlarını yapalım

Nginx Konfigürasyonları

Şimdi de nginx konfigürasyonlarımızı yapalım.Aşağıdaki komutla yeni bir konfigürasyon dosyası oluşturuyoruz.
```cs
sudo vim /etc/nginx/sites-available/NewBlog
```

```cs
upstream app_server {
    server unix:/home/volkan/run/gunicorn.sock fail_timeout=0;
}

server {
    listen 80;

   #Buraya ip addresinizi de yazabilirsiniz veya yonlendirdiginiz domaini de yazabilirsiniz.
    server_name volkanoluc.com;

    keepalive_timeout 5;
    client_max_body_size 4G;

    access_log /home/volkan/logs/nginx-access.log;
    error_log /home/volkan/logs/nginx-error.log;

    location /static/ {
        alias /home/volkan/static/;
    }

    # checks for static file, if not found proxy to app
    location / {
        try_files $uri @proxy_to_app;
    }

    location @proxy_to_app {

      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
      #proxy_redirect off;
      proxy_pass http://app_server;
      add_header P3P 'CP="ALL DSP COR PSAa PSDa OUR NOR ONL UNI COM NAV"';
   }
}
```
Şimdi de sites-enabled a bir sembolik link oluşturuyoruz.
```cs
sudo ln -s /etc/nginx/sites-available/NewBlog /etc/nginx/sites-enabled/NewBlog
```
Nginx in bize verdiği default web sitesini siliyoruz.
```cs
sudo rm /etc/nginx/sites-enabled/default
```
Nginx ayarlamalarımızda bitti.Nginx'i sorunsuz bir şekilde yeniden başlatabiliyorsak bir sıkıntı yok demektir.
```cs
sudo service nginx restart
```
Nginx konfigürasyonlarımızı da tamamladık.Uygulamamız artık yayına hazır.Son olarak yönlendirdiğimiz domainimizi kullanabilmemiz için setting.py dosyamızı açıyoruz.Allowed host kısmını aşağıdaki gibi boş bıraktıktan sonra uwsgi yi tekrar başlatıyoruz.
```cs
ALLOWED_HOSTS = "*"
~~~~~~~~~~~~~~~~~~
sudo service uwsgi restart
```
Bunları da yaptıktan sonra sitemizi sorunsuz bir şekilde yayına almış oluyoruz.Umarım faydalı bir yazı olmuştur.İyi günler :)
