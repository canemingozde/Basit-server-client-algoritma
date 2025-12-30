
# 🧠 Server–Client İletişim Algoritması

> Server–client ilişkisi içinde emir–komuta akışını gösteren basit bir yapı.

Bu proje, Python ile socket programlama kullanılarak **Server** ve **Client** arasında mesajlaşma akışını gösterir.  

---

## 🖥️ Server.py Algoritması

1. Socket oluşturulur:
   - `AF_INET` ve `SOCK_STREAM` ile TCP bağlantısı kurulur.
2. Host ve port tanımlanır:
   - Örn: `127.0.0.1`, `45647`
3. Socket bind edilir:
   - Belirtilen IP ve port’a bağlanılır.
4. Dinleme başlatılır:
   - `listen(1)` ile sadece bir client kabul edilir.
5. Client bağlantısı kabul edilir:
   - `accept()` ile bağlantı kurulur, adres bilgisi alınır.
6. Mesaj alma fonksiyonu tanımlanır:
   - `msj_get()`: client’dan gelen mesajları sürekli dinler.
7. Ana döngü başlatılır:
   - Kullanıcıdan input alınır.
   - Eğer mesaj `"close"` ise:
     - Client’a gönderilir ve bağlantı kapatılır.
   - Değilse:
     - Mesaj gönderilir.
     - `msj_get()` fonksiyonu ayrı bir thread ile başlatılır.

---

## 💻 Client.py Algoritması

1. Socket oluşturulur:
   - `AF_INET` ve `SOCK_STREAM` ile TCP bağlantısı kurulur.
2. Host ve port tanımlanır:
   - Server ile aynı IP ve port kullanılır.
3. Server’a bağlanılır:
   - `connect()` ile bağlantı kurulur.
4. Mesaj gönderme fonksiyonu tanımlanır:
   - `msj_put()`: kullanıcıdan input alır ve server’a gönderir.
5. Ana döngü başlatılır:
   - Server’dan gelen mesajlar dinlenir.
   - Eğer mesaj `"close"` ise:
     - Döngü kırılır ve bağlantı kapatılır.
   - Değilse:
     - Mesaj ekrana yazdırılır.
     - `msj_put()` fonksiyonu ayrı bir thread ile başlatılır.

---

## 🔄 Genel Akış

- Server başlatılır → Client bağlanır.  
- İki taraf arasında mesaj alışverişi yapılır.  
- `"close"` komutu gönderildiğinde bağlantı sonlandırılır.
