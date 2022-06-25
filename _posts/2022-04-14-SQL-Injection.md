
## SQL Injection

Sql Injection'a geçmeden önce biraz sql kodları üzerinde örneklere bakalım;

![resim](https://user-images.githubusercontent.com/18248422/175047302-d3dfa2e1-83eb-432b-b1c4-fdfcf8bd986b.png)

![resim](https://user-images.githubusercontent.com/18248422/175047335-4b019e06-28fb-436a-9eb7-25147a8a83c1.png)

 Bu komut ile virtualBox da açtığımız metasploitable makinasına linux üzerinden sql database e erişiyoruz. Normalde bu komuttan sonra şifre istemesi lazım fakat bu makinada bilerek bu kısmı açık ve şifresiz bırakmışlar. 
 Bu komuttan sonra artık metasploitable makinasının data base'ine eriştik;
 
![resim](https://user-images.githubusercontent.com/18248422/175047377-5c35ec6a-2d0e-4857-ab4a-d82ada94a04f.png)

Şimdi “show databases;” komutu ile içerde olan veri tabanı tablolarını görelim;

![resim](https://user-images.githubusercontent.com/18248422/175047413-bc40d62d-67be-4b44-b64a-11d10720d61d.png)

işte bunlar bu makinada bulunan database'ler.

Bunlardan mesela “owasp10” database'ini seçelim;

![resim](https://user-images.githubusercontent.com/18248422/175047488-554430af-5ea6-4dfd-bccc-1ff003b96c66.png)

"use owasp10" komutu ile mysql database'ine geçiş yaptık. use <database_name>

owasp10 içerisinde ki tabloları görelim;

![resim](https://user-images.githubusercontent.com/18248422/175047550-f44483fe-d4ef-4429-bb7f-3a9e254adeec.png)

"show tables;" komutu ile tabloları görebildik.

Şimdi bir tablo seçip onun içine bakalım;

![resim](https://user-images.githubusercontent.com/18248422/175047608-f0db1f87-bbb9-4d2d-9375-207c4a210b0d.png)

"credit_cards" tablosunda ki bütün bilgileri “select * from credit_cards” komutunu girerek listeledik.

 Şimdi gelelim asıl önemli olan kısıma. Örneğin bir siteye giriş yaparken verilen kullanıcı adı, şifre gibi bilgileri yanlış girdiğimize bize gösterilen hata mesajına göre bir açık bulabiliriz ve bu açıktan faydalanabiliriz. 
 
 Bu duruma bir örnek olarak;
 
 ![resim](https://user-images.githubusercontent.com/18248422/175047640-2b584023-a721-4e8d-be70-2a9ab1a528b2.png)
  
  bu sitede şifre kısmına tek tırnak olan ' işaretini koydum ve site bu hatayı karşıma çıkarttı. Bu hatada özellikle kırmızı ile işaretlenen kısıma dikkat et, “select * FROM accounts..” şeklinde gösterilen yerden anlaşılacağı gibi “accounts” diye bir tablo bulunduğu bilgisini böylelikle edinmiş olduk. Şimdi bu tarz bilgiler sayesinde, bu tarz açıklardan nasıl bir şekilde faydalanıp kullanabiliriz onu görelim. 

![resim](https://user-images.githubusercontent.com/18248422/175048221-fc6565ca-378d-4a35-b300-cabc8ccde6a8.png)

  bizim ilgilendiğimiz kısım bu SQL kodu. Bunun mesela password kısmına kendi passwordumuzu ve AND 1=1#' yazıp yani AND kısmından sonra doğru olacak bir logic yazıp (resimde görülen kırmızı ile altı çizili kısım), bunu alıp kopyayalıp şifre kısmına girip bu şekilde giriş yaptığımızda eğer çalışıyorsa bu şu demek oluyor; biz şifremizle birlikte aslında SQL kodu da yazarak çalıştırabiliyoruz, işte bu ve bunun gibi form göndererek sql kodu çalıştırma yöntemine SQL Injection deniyor. SQL Injection için genelde AND ve sonrasında istediğimiz bir kod ve en sonunda da # koymamız yani # işareti ile kapatmamız gerekir. Resimde işaretli kısımda ki örnekte olduğu gibi biz bu durumda password kısmına hem şifremizi hem de çalıştıracağımız kodu yapıştırıyoruz, bu örnekte olan durumda password kısmına şunu yapıştırmamız gerek;  111111' AND 1=1#
  
  Eğer şifreyi bu şekilde “111111' AND 1=1#” girdiğimizde giriş yapılıyorsa demek ki SQL kodu çalışıyor. Şimdi bunu admin kullanıcısı olarak deneyelim;
  
  ![resim](https://user-images.githubusercontent.com/18248422/175048332-d05ed668-627e-4b02-a6fb-1725523c71a0.png)

  
  
  name için admin, şifre için bu sefer AND değil OR kullandık çünkü şifre ‘1’ ise VEYA (OR) 1=1 doğru ise giriş yap demiş olduk. E 1=1 doğru olduğuna göre bu şekilde ki bir SQL injection doğru kabul edeceği için admin şifresini bilmemize bile gerek kalmadan girmiş olduk. username için ya da bu örnekte olduğu gibi Name için admin girmeyi unutmuyoruz ki admin olarak giriş yapabilelim. Şifre kısmına tam olarak resimde de mavi şekilde seçili olan kısım  “1' OR 1=1#" (çift tırnaklar hariç) bu şekilde girdik. Yani password isimli değişkenin içini atıyoruz. 
  password='içi' →  mavi şekilde seçili kısmı yukarıda ki forma bulunan password kısmına yaz 
  
 ![resim](https://user-images.githubusercontent.com/18248422/175048446-93a3d097-4682-4db0-9890-84bb4e1d58d6.png)
  
 ![resim](https://user-images.githubusercontent.com/18248422/175048468-7eff3372-9edc-488b-b5be-a9581bd0066f.png)

  Benzer olarak birde bu yöntem var. Burda öncekinden farklı olarak sadece “admin” username yani kullanıcı adı için sonuna # işareti koyduk. Bu şu demek oluyor, # bu işaretten sonra ki kodların hiç bir önemi yok! Eğer “admin” isimli bir kullanıcı varsa şifresinin ne olduğundan bağımsız (resimde ki altı çizili ve 2 yazan kısımda ki şifrenin hiç bir önemi yok öylesine yazıldı) olarak bu SQL injection'ı admin kullanıcısı için yap ve sisteme gir!
 
 ![resim](https://user-images.githubusercontent.com/18248422/175048515-2028b9a8-8890-46c4-8176-69f02f474ce4.png)
  
  Name kısmına girip admin'# (' işaretini koymayı da unutma) yazıp şifre kısmına ne yazarsak yazalım artık admin olarak Login olabiliriz.
  
  Bu gösterilen yöntemler SQL Injection yapabildiğimizi fark ettiğimizde ilk denememiz gereken yöntemlerdendir.

  ## Get Metodu ile SQL Injection
  
  Bir örnek üzerinden gidelim;
  ![resim](https://user-images.githubusercontent.com/18248422/175048574-f28b2758-95e6-4dab-99a6-274cc451ca9f.png)

  bu sitenin kullanıcıların hesapları ile ilgili bilgi verdiği kısım. Şimdi burada bilerek yanlış bir name and password girelim;
![resim](https://user-images.githubusercontent.com/18248422/175048612-6b9e4718-f2bd-4459-a47f-141f25881e89.png)
  
  yanlış bir name and password girdiğimizde URL kısmının değiştiğini görüyoruz. O zaman biz bu URL kısmında bazı değişiklikler yaparak kendi istediğimiz bir kodu çalıştırarak SQL Injection yapabilir miyiz deneyelim;
  
  URL kısmında ki adresi şu şekilde,
  
 ![resim](https://user-images.githubusercontent.com/18248422/175048649-9ada2610-de76-47a4-a752-fc0e750bd36c.png)

  şimdi bu adreste olan username kısmında ki “aaa” diye girdiğimiz kısmın sonuna ' ve # işaretlerini koyalım (önceki örnekte olduğu gibi) ve bu şekilde Name kısmına yapıştıralım yani tam olarak şu şekilde aaa'#

 ![resim](https://user-images.githubusercontent.com/18248422/175048672-fefc9567-5069-4fc2-a7a0-4786d06e08f2.png)

 şimdi bu değişen kısmı URL yapıştırıp çalıştıralım. 

 Çalıştırdıktan sonra sayfada bir değişiklik olmadı, demek ki bu metod çalışmıyor veya bir yanlış yaptık. 
 
 Aslında burada ki yanlış şuydu;
 
  biz URL kısmına # koyduğumuzda HTML koduna çevrilmedi, biz # kısmının HTML koduna çevrilmesi için # yerine %23 yazmalıyız.
  
  ![resim](https://user-images.githubusercontent.com/18248422/175048758-0b8cac4b-ca18-456a-ba49-f90f2c3ab316.png)

  yani bu şekilde # yerine %23 yazdık. Şimdi bu haliyle çalıştırmadan önce “aaa” gibi büyük ihtimalle sistemde bulunmayan bir username yerine admin yazarak URL kısmına yapıştıracağımız linki son haline getirelim.
  
  ![resim](https://user-images.githubusercontent.com/18248422/175048786-1690a618-7e6f-4e62-8c88-7ce7f9ad7c99.png)

  şimdi kullanıcı adını da “admin” olarak değiştirdiğimize göre artık URL kısmına bunu yapıştırıp çalıştıralım.
  
  ![resim](https://user-images.githubusercontent.com/18248422/175048853-dfab5c75-8939-4b6f-a6ea-3834d80b7a16.png)
 Çalıştırdıktan sonra gördümüz gibi admin, şifresi, signature(imzası) olarak bilgilerini öğrenmiş olduk.
  
  İşte URL kısmında bir parametre görürsek, get metodu ile URL üzerinde yaptığımız değişikliklerle get metodu ile Sql Injection bu şekilde yapılıyor.
  
  Şimdi işi bir adım daha ileri götürelim. Örneğin bir siteye girmeye çalışıyoruz ve doğal olarak o sitenin veri tabanında (database) bulunan kullanıcı isimlerini bilmiyoruz hatta admin kullanıcı adını kullanarak get metodu ile sql injection gibi denemeler yaptık ama baktık ki kullanıcı adı olarak admin yok sonuçta yöneticinin kullanıcı admin olmak zorunda değil. Bu tarz durumlar için SQL dilinde bulunan “UNION” yani “birleştirme” kodunu kullanarak iki tane SQL sorgusunu birden injection edeceğiz.
  
  ![resim](https://user-images.githubusercontent.com/18248422/175048913-6f463539-c34b-48d6-8831-acbd03c3a750.png)

  burda da görüldüğü gibi UNION ile iki tane SQL sorgusunu birleştirdik. 
   
  Bunu URL kısmına şu şekilde yazıyoruz;
  ![resim](https://user-images.githubusercontent.com/18248422/175048955-d9b60bd9-9685-4977-89ab-fd10fe90fe30.png)
  
  <'union select * from accounts> yani kullanıcı adı olarak admin diye bi kullanıcı olsa da olmasa da git accounts tablosunda ki bütün kullanıcıları,şifreleri vs her şey bana göster demiş olduk.
  
  username kısmına yazdığıma dikkat et, olmayan bir kullanıcı yazdığımız halde çalışacak.
  
  Sonuç;
  
  ![resim](https://user-images.githubusercontent.com/18248422/175048986-5860e88d-11dc-469b-bc45-e1f9eedc645e.png)

  sonuç bu. Admin de dahil bütün kullanıcıların bilgilerini aldık. Hem de şifreyi bırak, login olmadan, sistemde ki tek bir kullanıcı adını bile bilmeden.
  
  Şimdi burdada şöyle bir sorun çıkıyor, kullanıcı adını bilmeden bunu yaptık fakat bu kısımda “accounts” tablosunu kullanarak bu bilgiyi edindik. Eğer biz “accounts” isimli bir tablonun olduğunu bilmeseydik o zaman nasıl yapabilirdik? Şimdi ise bu soruyu cevaplayalım.
  
  ![resim](https://user-images.githubusercontent.com/18248422/175049119-048f20c8-2b0a-4a29-b69a-26381895601c.png)

  üstte ki satırda olan “UNITON SELECT * FROM accounts...” kısmı önceden yazdığımız ve “accounts” tablo ismini bilerek yazdığımız kod.
  
  Bi alt satırda ki altı kırmızı ile işaretli olan kısımda da gösterildiği gibi “ORDER BY 1” olarak değiştirdik. ORDER BY verilen değere göre veri tabanında ki bi sütunları sıralamamıza yarayan bir keyword. Şimdi mesela ORDER BY 10 diyip bunu URL kısmında çalıştırmamız şu demek olacak; 10 tane sütun varsa onları bana sırala. Bunu deneyelim;
  ![resim](https://user-images.githubusercontent.com/18248422/175049143-9f163ec6-7d40-48d9-bff5-d76a05d3dba4.png)
  
  url kısmında işaretli şekilde çalıştırdığımızda aşağıda ki mesajda olan “böyle bir (bu kadar sayıda) sütun yok” hatasını aldık. Demek ki 10'dan daha az sütun varmış. Sayıyı azaltarak deneme yanılmayla ilerleyip doğru sütun sayısını buluyoruz.
  ![resim](https://user-images.githubusercontent.com/18248422/175049165-36f84c02-741f-46a2-8af5-25bc3378a506.png)
  
  sütun değerinin 5 olduğunu buluyoruz çünkü bir hata almadık ama şu durumda da bir bilgi veya değer de edinemedik ama en azından 5 tane sütun olduğunu anlamış olduk.
  
  Madem 5 sütun olduğunu bulduk o zaman UNION SELECT ile bu 5 sütunu seçelim;
  ![resim](https://user-images.githubusercontent.com/18248422/175049202-14120ce3-6bcf-47e4-8398-632b5d4cb388.png)

  bu şekilde seçiyoruz ve URL kısmına şu şekilde giriyoruz;
  ![resim](https://user-images.githubusercontent.com/18248422/175049266-93595a4b-61e8-4155-af32-a781fe66bb66.png)

  url kısmında kodu çalıştırınca aşağıda ki sonucu elde ediyoruz. Burda da görüldüğü gibi biz 1,2,3,4,5 girmemize rağmen bize 2,3,4 değerlerini döndürdü demek ki 2,3,4 kısmında ORDER BY kullanmamız daha mantıklı çünkü 1,5 ile ilgili mantıklı bir değer döndürmedi. O zaman biz 2,3,4 için istediğimiz bir değeri verip çalıştırırsak bu sayede istediğimiz değeri görebiliriz.
  
  Biz database i arıyoruz madem o zaman 2,3,4 değerleri yerine başka şeyler yazıp deneyelim. 
  ![resim](https://user-images.githubusercontent.com/18248422/175049311-d77b0e8c-cf66-49e1-b418-046bda1445af.png)

  2,3,4 çalıştığı için gidip 2,3,4 yerine database(),user(),version() gibi değerler yazdık ve resimde de görüldüğü gibi gerçekten de çalıştı ve bize bu değerleri gösterdi. 
  ![resim](https://user-images.githubusercontent.com/18248422/175049394-28342e47-2b31-45a8-adf7-1f3af9fb4b0d.png)

  NOT: burada ki username,password,signature kısımlarının karşısında çıkan değerler doğru eşleşmedi çünkü biz bunları değil de bizim istediğimiz database(),user(),version() değerlerini URL kısmında verdiğimiz için username,password,signature kısımlarının karşısında database(),user(),version() değerleri çıktı. Yani burda ki username,password,signature yazmasının bir önemi yok. owasp10, root@localhost gibi bilgileri edinmemiz önemliydi ve edindik, yani istesek gerçekten de username karşısına username() getirmeyi deneyebilirdik, biz durda çalışıp çalışmadığını denemek için öylesine database(),user(),version() değerlerini verdik ve karşılığında da onlar çıktı ve çalıştığını görmüş olduk.
  
  Şimdi gelelim asıl amacımız olan tablo isimlerini bulmaya.
  ![resim](https://user-images.githubusercontent.com/18248422/175049429-a4f7ec39-325b-4079-a4d7-9e7cba8ef0eb.png)

 bu şekilde bir sorgu ile her sql database dosyasında bulunan ve resimde de altı çizili gösterilen “information_schema” dosyasında ki bütün tabloları aratabiliriz. Şimdi bunu URL adresine koyup çalıştıralım. 
![resim](https://user-images.githubusercontent.com/18248422/175049449-c8b9c9d3-2d81-4f7f-84c5-9a4ee1afca6f.png)


Bütün veri tabanını tarayıp 237 tane tablo karşımıza çıkarttı. Biz aradığımız veri tabanı ismimlerinden birini “database()” yazarak "owasp10" olarak görmüştük, bunu kullanıp aramamızı daha spesifik bir hale getirebiliriz.
![resim](https://user-images.githubusercontent.com/18248422/175049491-0f36a5de-4918-4664-9d5a-66e94dddd5ee.png)

owasp10 database'inde bulunan tabloları sıralamak için bu şekilde yazabiliriz.
![resim](https://user-images.githubusercontent.com/18248422/175049750-97315c5d-85a3-4a3b-89a7-5c6ca3f402cf.png)

 İşte artık ismini öğrendiğimiz bir database de bulunan bütün tabloları da görmeyi başardık. Şimdi madem tabloları gördük şimdi bu yönteme benzer şekilde birde yapmışken bu bulduğumuz tablonun içinde ki sütunları yani column ları da görelim;
 ![resim](https://user-images.githubusercontent.com/18248422/175049776-73a9bc08-58bb-4d59-9e23-83d5e3a530ab.png)
 
 bu şekilde URL'e yazalım;
 ![resim](https://user-images.githubusercontent.com/18248422/175049806-3d8d54fb-1b5c-4b69-b1af-62d6e944e203.png)
 
 accounts tablosunda ki sütun isimlerini de ele geçirdik. 
 
 Artık hem tablo hemde sütun (column) isimlerini gördüğümüze göre buna göre bir arama yapıp bütün her şeyi görebiliriz;
 ![resim](https://user-images.githubusercontent.com/18248422/175049853-5e4fe6ae-5a5d-4686-9db5-c9ad5eb6d83a.png)
 ![resim](https://user-images.githubusercontent.com/18248422/175049915-e196298c-6061-4f23-acd6-ee36c23c3e08.png)

 böylelikle her bir bilgiyi gördük ve ele geçirdik.
  
 NOT: aşağıda ki resimde, önceki sorgularda ki farkları belirtmek için kırmızı ok ile çizip değişimlerini gösterdim.
 ![resim](https://user-images.githubusercontent.com/18248422/175049972-bf904ace-e50e-44fc-bdc6-fccf94825d56.png)

 Böylelikle SQL Injection sayesinde siteye giriş bile yapmadan bütün database i elegeçirdik.
 
 Bu kısımda öğrendiklerimizin hepsi işin arka planını anlamak içindi. Mantığını anladığımıza göre, bütün bu manuel olarak yaptığımız işleri bizim için site üzerinde (URL vererek) tarama yapıp, SQL Injection yapabileceğimiz bir açık var mı? Varsa database i görmemizi, içeriğini incelememizi vs sağlayan, bütün bunları otomatik olarak yapan bir framework var; SQL Map 
 
 ## creted by @[ahmetkara](https://github.com/ahmetQara)

