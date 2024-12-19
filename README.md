# Docker

## Docker Katmanlı Dosya Sistemi:

Union File System
![image](https://github.com/user-attachments/assets/8aa23a1f-a13b-423d-aa3f-61372069ade1)

Docker, image’lardan bir container oluşturulduğu zaman, yeni bir katman oluşturur (Container Yazılabilir Katman) ve sizin containerlar üzerinde yaptığınız değişiklikler bu katmanda yapılır. Yukarıdaki resimde bulunan üç katman ise containerlarda read only olarak oluşturulur. Bu sayede yapılan değişiklikler sadece o container’ı etkiler.

![image](https://github.com/user-attachments/assets/80453d27-50d1-4c09-a9b4-723e1b1f9567)
