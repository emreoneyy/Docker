# Docker

## Docker Katmanlı Dosya Sistemi:

Union File System
![image](https://github.com/user-attachments/assets/8aa23a1f-a13b-423d-aa3f-61372069ade1)

Docker, image’lardan bir container oluşturulduğu zaman, yeni bir katman oluşturur (Container Yazılabilir Katman) ve sizin containerlar üzerinde yaptığınız değişiklikler bu katmanda yapılır. Yukarıdaki resimde bulunan üç katman ise containerlarda read only olarak oluşturulur. Bu sayede yapılan değişiklikler sadece o container’ı etkiler.

![image](https://github.com/user-attachments/assets/80453d27-50d1-4c09-a9b4-723e1b1f9567)



## Komutlar:

### **help (—help):**

Bu komut sayesinde kullanmak istediğimiz şeyi, nasıl kullanabileceğimizi öğreniriz.
![image](https://github.com/user-attachments/assets/45dc4b69-d3f0-4da8-8c7c-77c58018c6be)

### Container oluşturma komutu:
`docker container run {image}`

Her container imajında o imajdan bir container yarattığımız zaman varsayılan olarak çalışması için ayarlanmış bir uygulama vardır ve bu uygulama çalıştığı sürece container ayakta kalır. Uygulama çalışmayı bıraktığında da container da kapatılır.

### Container loglarını görme komutu:

`docker container logs {container_id}`

### Container silme komutu:

`docker container rm {container_id}`

`docker container rm -f {container_id}`

`docker container prune` → Bütün containerları siler.

### Containeri arkaplanda (detech modda) çalıştırmak:

`docker container run -d -p 80:80 {image_name}`

## Container’ın içerisine girmek:

`docker container exec -it {container_name} sh`

Buradaki exec komutu container’a bağlanmamızı sağlar. -it komutu o container’ın terminalinde işlem yapabilmemizi sağlar. sh ‘da container shell’inin açılmasını sağlar.


## Volume:
Container'larda veri depolamayı sağlar ve bunu container'ın yaşam süresinden bağımsız bir şekilde yapılmasını sağlar.

### Volume oluşturma komutu:

`docker volume create {volume_name}`

### Volume ve container’ı bağlama komutu:

`docker container run -v {volume_name}:/{folder_name} {image_name}`


# Docker Network Driver:

Bridge Network Driver: Varsayılan olarak kullanılan network driver’ıdır. Bir container oluşturulduğu zaman, arkada bir bridge network ağı da oluşturulur. Container bu ağa bağlanır.

Host Driver: Üstünde çalıştığı sistem ile container arasında bir network izolasyonu bulunmaz. Üzerinde çalıştığı host’un network bilgilerini aynen alır.

MacVlan:

None: Container’ın ağ bağlantısı olmasını istemezsek bu driver ile oluşturabiliriz.

Overlay: Aynı cluster’ın içerisindeki container’ları aynı ağda göstermek istersek kullanıyoruz.

### Default Bridge Network ile User Defined Bridge Network Farkları Nelerdir?
- Default Bridge Network'e bağlı containerlar birbirleri ile isimleri üzerinden iletişime geçemezler. IP adresleri üzerinden iletişime geçebilirler. DNS hizmeti yoktur diyebiliriz yani.
  ![image](https://github.com/user-attachments/assets/f52648b6-690d-4ae1-95de-eef139663216)

- User Defined Bridge Network'e bağlı containerlar birbirleri ile isimleri üzerinden iletişime geçebilirler.
  ![image](https://github.com/user-attachments/assets/46eedf2f-2173-4b8f-8f1e-7c54b3ade89c)

- Default Bridge Network'e bağlı containerlar birden fazla ağa bağlanamazlar.
- User Defined Bridge Networklar istenilmesi durumunda birden çok ağa bağlanabilirler.


# Port Publish:

 Dışarıdan container’a bağlanmak istediğimizde kullanılan yöntemdir. Container’ın portu ile bağlı olduğu host’un portlarının birbirlerine eşlenmesi gibi düşünebiliriz. Bu sayede dışarıdan gelen istekler host’a daha sonrada container’a aktarılır.

`docker container run -p {host_port}:{container_port} {image}`


# Docker Logs:

Container Loglarını İnceleme Komutu:

`docker logs {container_name}`

Container Loglarını Detaylı İnceleme Komutu:

`docker logs —details {container_name}`

Container loglarını zaman bazlı inceleme:

`docker logs -t {container_name}`

Belirli bir saate kadar logları inceleme komutu:

`docker logs —until {time} {container_name}`

`docker logs --until 2024-06-07T14:50:03.998817254Z con1`

**Timestamp ile beraber logları yazma komutu:**

`docker logs -t {container_name}`

Belirli bir saatten sonraki logları inceleme komutu:

`docker logs —since {time} {container_name}`

Son n tane log satırını alma komutu:

`docker logs —tail {number_of_line} {container_name}`

`docker logs —tail 3 con1`

Logları canlı olarak takip etme komutu:

`docker logs -f {container_name}`


# Docker Stats ve Top:

 `docker top {container_name}` bu komut sayesinde container’ın içine girmeden, o container içinde nelerin çalıştığını görebiliriz.

`docker stats` bu komut sayesinde o sistemdeki tüm containerların CPU,RAM,I/O kullandığını görebiliriz.

`docker stats {container_name}` bu komut sayesinde, containerların ne kadar CPU, RAM I/O kullandığını görebiliriz.


# Container CPU ve Memory Limitleri:

Gerçek dünyada en çok karşılaşılan problemlerden bir tanesi, ilgili container’ın kurulu olduğu host üzerinde fazla CPU ve Memory kullanması sonucunda diğer container’lara CPU ve Memory yetmemesidir. Container oluştururken bu sınırlamayı veren bir komut kullanmazsak bu tarz problemler ile karşılaşabiliriz.

İlk olarak bir sınırlama yapmadan container oluşturup limitini inceleyelim.

![image](https://github.com/user-attachments/assets/5c569861-4f1c-4a38-8e45-5627493aeea8)


`docker container run -d —-memory={LIMIT} {image}` bu komut sayesinde 100mb bir sınır koyup container oluşturuyorum. Daha sonra `docker stats` komutu ile limiti inceliyorum.

![image](https://github.com/user-attachments/assets/7730e3aa-beb6-4f37-a163-5c0560725b72)


Eğer ki container’ın kullandığı memory tamamen kullanılırsa, o durumlarda sistemin çökmemesi adına swap alanı açabiliriz. Bu şekilde diskten ekstra container’a yer açılır.

`docker container run -d —-memory=100m —-memory-swap=200m {image}`

—cpus kullanımı core kullanımı açısından sınırlandırmayı sağlar.

`docker container run -d —-cpus=”1.5” {image}`

`docker container run -d —-cpuset-cpus=”0,3” {image}`


# Docker Environment Variables:

`printenv` environment değişkenleri listeler

`export {variable_name}=”{variable_value}”` yeni bir değişken tanımlamızı sağlar.

`echo {$variable_name}` belirli bir değişkenin değerini gösterir.

Container oluştururken env variable oluşturmak:

`docker container run —-env VAR1=deneme1 —-env VAR2=deneme2 {image}`

Bütün değişkenleri bu şekilde tek tek vermek zor olacağı için bunları bir dosyada tutup container’a da aktarabiliriz. Bunun için önce env.list adında bir txt dosyası oluşturuyorum.

![image](https://github.com/user-attachments/assets/45cf1028-fb8f-4fdc-b975-92ea0e8ab696)

Daha sonra terminalde bu dosyanın olduğu dizine gidip komutumu yazıyorum.

`docker container run —-env-file ./env.list ubuntu`

# **Docker Image Oluşturma:**

**FROM imaj:tag**  

Oluşturulacak imajın hangi imajdan oluşturulacağını belirten talimat:

Örnek: FROM ubuntu:18.04

**RUN**

Image oluşturulurken, shellde bir komut çalıştırmak istersek bu talimat kullanılır. 

**WORKDIR klasor_path**

Normalde terminalde cd ile belirli bir path’e gitme işlemimizi yapmaya yarar. cd’den farklı olarak eğer o path yoksa oluşturur.

Örnek: WORKDIR /usr/src/app   

**COPY kaynak hedef**

Imaj içine dosya veya klasor kopyalamak için kullanılır.

Örnek: COPY /source /user/src/app 

**CMD** 

İmajdan container yaratıldığı zaman varsayılan olarak çalıştırmasını istediğimiz komutu CMD ile belirleriz.

Örnek: CMD java merhaba

**EXPOSE**

İmajdan oluşturulucak containerların hangi portlar üzerinden erişilebileceğini yani hangi portlar üzerinden yayınlanacağını belirtiriz.

Örnek: EXPOSE 80/tcp

### **Örnek Image:**
![image](https://github.com/user-attachments/assets/8eedd1cc-99a0-4ddc-86cc-4e386fdfa387)

![image](https://github.com/user-attachments/assets/c6126d59-f352-459a-b7bd-8781bb00fc17)

![image](https://github.com/user-attachments/assets/a3946f93-5855-40f6-b3be-acb9487665e4)

