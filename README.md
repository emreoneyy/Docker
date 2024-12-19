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
docker container run {image}

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

