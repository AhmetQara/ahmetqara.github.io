 ## Reverse Shell
 
  Reverse shell yani tersten shell açmak, komut çalıştırabildiğimiz bir sunucudan kendi cihazımıza bir bağlantı açmamıza olanak sağlar. Backdoor mantığına benzerdir ama tam olarak aynı değil. Backdoor da karşıda bir kullanıcının bir .exe veya bir dosya çalıştırması, bir siteye vs. girmesi bi şeylere tıklaması gerekirken, reverse shell de biz kendimiz kod çalıştırabileceğimiz bir açık bulduğumuzda o zaafiyetten faydalanıp kendimize bağlantı yaptırarak içeriye daha kolay sızabilmek için açık bir kapı bırakmış oluyoruz. 
 
  Şimdi komutumuzu yani reverse shell komutunu girmeden önce netcad ile bir port açıp dinlemeye başlayalım.
 
 ![resim](https://user-images.githubusercontent.com/18248422/179301637-3076384b-b372-4f9a-a389-c0ea4c9f4de6.png)

  bu şekilde netcad çalıştırarak “5050” portunu dinlemeye başlıyoruz.
 
  Ardından mesela php için yazılmış olan reverse shell komutunu siteye girelim;
  
  ![resim](https://user-images.githubusercontent.com/18248422/179301653-43e32e81-e92f-4e91-ba45-4fdb6041dfec.png)
 
  tabi bu komutta olan ip adresine kendi ip adresimizi ve port kısmına ise netcad ile dinlemeye başladığımız “5050” portunu giriyoruz. 
  
  ![resim](https://user-images.githubusercontent.com/18248422/179301673-e5b1f11b-db47-4db0-ad96-7d7b66e1255a.png)
 
  Gerekli düzenlemeleri yapınca komut bu hale geldi. Artık bu komutu gidip site üzerinde ki form da çalıştırmak üzere submit edebiliriz. 
  
  ![resim](https://user-images.githubusercontent.com/18248422/179301689-37004051-d8fa-4a66-a7c4-20f0f02319d4.png)
 
  bu şekilde yazıp submit ediyoruz.
  
 ![resim](https://user-images.githubusercontent.com/18248422/179301711-f826e3a9-2fa3-4354-8c14-aed7745921b6.png)

  komutumuzu yazıp submit edince, terminalimizde nc ile açıp dinlemeye başladığımız 5050 portuna bağlantı geldi. Gördüğünüz gibi bu komut sayesinde bu siteden kendimize bir shell açıp içeriye girmeyi başardık artık websitesinin bazı dosyalarına erişebiliyoruz. Reverse shell işlemi başarılı olmuş oldu.
 
  NOT: Bir sitede reverse shell denemeden önce python için version kontrolü yapmak çok işe yarayacaktır. Bir şekilde eğer komut çalıştırabiliyorsak bu kontrolü “<which python3> veya <which python>” şeklinde yapabiliriz;
 
 ![resim](https://user-images.githubusercontent.com/18248422/179301770-a64fca42-43af-4794-8b9e-e2c75ef1feea.png)

## created by [@ahmetkara](https://github.com/ahmetQara)
