

## Man In The Middle Attack (Mitm)

![resim](https://user-images.githubusercontent.com/18248422/176667863-f5ba04f5-7334-49a9-9f17-0aaea41b265a.png)
![resim](https://user-images.githubusercontent.com/18248422/176667877-7602ba31-27c1-4079-83c5-4ba4e7447104.png)

yukardaki şekilde ki “ROUTER" ya da modeme bir response gönderebiliyoruz. Bu response içeriği olarak kendi mac adresimizi verirken ip olarak “TARGET” ip verebiliriz. Böylelikle bu ip de bu mac adresi var diyerek modemi yanlış yönlendirebiliriz. Ardından “TARGET” a gidip yine kendi adresimizi ve ip olarak ise modemin ip'sini vererek kendimizi modem gibi tanıtabiliriz.
  
Tüm bu yaptıklarımızdan sonra aşağıda da görüldüğü gibi modem(router) bizi TARGET, TARGET ise bizi modem sanacaktır. Bizde ortada ki cihaz olarak kalacağımız için bu yönteme “Man in the Middle” adı verilmiştir.

![resim](https://user-images.githubusercontent.com/18248422/176667909-67d71ed3-8ae4-4e23-9ef0-e20647e8d0a8.png)
![resim](https://user-images.githubusercontent.com/18248422/176667925-7391d160-fe01-4b06-ae87-baa8fd625413.png)

TARGET cihaz internete çıkarken tüm istekleri bizim üzerimizden geçirecek bizde bu istekleri modeme ileteceğiz ve böylece modemden gelen cevaplarıda görebileceğiz ve hedef(TARGET) cihaza iletebiliriz. Böylelikle tüm internet paketlerini okuyup hedefin hangi sitelerde gezdiğini, şifrelerini, kullanıcı adı bilgilerini vs her şeyini görebiliriz. Bütün bu man of the middle saldırısının yapılması için hedef ile aynı ağda olmak gerekir. 

Mitm(man in the middle) saldırısında başlamadan önce ip forward işlemi yapmalıyız ki hedefin internet bağlantısı kesilmesin. Bu işlemi her boot dan sonra yapmalıyız.

ip forward için terminal'e şu komutu girmeliyiz;

echo > 1 /proc/sys/net/ipv4/ip_forward

![resim](https://user-images.githubusercontent.com/18248422/176667999-79cab0e9-d92b-4b81-899e-29bee824c68e.png)

burada görülen “op” eğer “1” değerine sahipse “arp request” oluşturmak anlamına gelir eğer bunun değeri “2” olursa “arp response” oluşturmak anlamına gelir. Bizim için arp response(cevap) olması lazım o yüzden bunun değerini 2 yapmalıyız. Bunu da şu şekilde kod yazarak yaparız;

arp_response = scapy.ARP(op=2,.... gibi

aşağıda bir kod örneği bulunmaktadır

arp_response = scapy.ARP(op=2,pdst="10.0.2.15",hwdst="08:00:27:e6:e5:59",psrc="10.0.2.1")
scapy.send(arp_response)
 
## Mitm atağı başlatma (manual olarak arpspoof)

![resim](https://user-images.githubusercontent.com/18248422/176668375-43d99f65-2142-4351-8dfb-ce0f4611d47a.png)
![resim](https://user-images.githubusercontent.com/18248422/176668390-b3e28aed-248c-4ca8-b12c-cc8d38737358.png)
 
Bu kodlarla arp_posion yaptık. Bu arp_poison işlemi ile hedef ip olan “10.0.0.62” adresi artık modemin mac adresini bizim makinemiz olarak görüyor.

Aşağıda ki resimde de bunu değişikliği görebiliriz.

![resim](https://user-images.githubusercontent.com/18248422/176668503-18c89da4-b687-4369-a1f6-7c5aba50616c.png)

Böylelikle modemin ip'si olan “10.0.0.1” in mac adresini kendi mac adresimiz ile değiştirdik. 
    
Hedef cihaz modemi bizim verdiğimiz mac adresinde sanıyor, böylelikle arp saldırısı başarıya ulaştı.

