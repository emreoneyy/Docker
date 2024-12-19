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



