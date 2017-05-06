---
layout: post
title: HackThis Web Walkthrough Part 2
date: '2017-05-6 13:12:34 +0300'
categories: blog
---



Selamlar,
Bu yazıda, Octosec tarafından hazırlanan **Kevgir** isimli sanal makinenin bir kaç çözümünü inceleyeceğiz.
Makineyi şu linkten indirebilirsiniz : **[Vulnhub](https://www.vulnhub.com/entry/kevgir-1,137/)**


Çözüme, hedef makinenin IP adresini bularak başlıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/1.png)

Ip adresini elde ettiğimize göre bilgi toplamaya başlayabiliriz.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/2.png)

Makinede oldukça çok açık port var. Ilk gözüme çarpan port **1322 numaralı ssh portu** oldu.
Banko olarak köşede bulunsun diye hemen bir bruteforce saldırısı başlattım.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/3.png)

ve ilk shell'imizi elde etmiş olduk.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/4.png)

Madem bruteforce ile siftahı açtık, brute force ile devam edelim.Default tomcat "username, password"'u varmi öğrenmek için **tomcat_mgr_login** axuilary'si ile bir tarama yapiyorum ve bingo !

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/5.png)

Username password bilgisi elde ettiğimize göre;
**tomcat_mgr_upload** exploit'i ile siteye bir shell yükleyebiliriz.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/6.png)

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/7.png)

Ve bir meterpreter oturumu elde ediyoruz.

Ve son elde etmek istediğim shell içinse apache portunu gözüme kestiriyorum.

8081 numaralı porta bağlandığımda beni bir joomla sitesi karşılıyor.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/8.png)

Siteyi incelemeye dahi tenezzül etmeden, hızlıca **joomscan** ile taramaya başlıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/9.png)
Joomscan bir sürü exploit sonucu döndü ama en çok dikkatimi çeken 15 numaralı exploit oldu

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/10.png)
Exploit'deki talimatlari uyguluyorum ve admin passwordunu kendi istediğim herhangi bir password ile değiştirdim.
Panel üzerinde biraz dolaştıkdan sonra Templates altında beez adlı bir sayfanın index.php dosyasını değiştirebileceğim bir yer buldum.
![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/11.png)

Dosyanın içindeki kodları, php reverse shell kodlarıyla değiştirdim

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/12.png)

Ve kaydedip o sayfaya gitmeye çalıştığımda, son bir meterpreter oturumu elde etmiş oldum.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/13.png)


Son olarak, bir post exploitation yapip yetkilerimi root'a yükseltiyorum.

![]({{ AUCyberClub.github.io }}/assets/img/kevgir-1/14.png)

---
**[Engin Demirbilek](https://twitter.com/Hyal0id)**
---














