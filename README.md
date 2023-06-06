# Recipe-Sharing-Platform
a site where people can register and share recipes
Recipe Sharing Platform Dökümantasyonu
Bu dökümantasyon, Recipe Sharing Platform projesinin kullanımı ve işleyişi hakkında bilgi sağlar. Proje, kullanıcıların tarif paylaşabileceği ve keşfedebileceği bir web tabanlı uygulamadır. Kullanıcılar, hesap oluşturabilir, kendi tariflerini yükleyebilir, tarifleri gözden geçirebilir ve diğer kullanıcılarla yorumlar ve derecelendirmeler aracılığıyla etkileşimde bulunabilir.

İçindekiler
Kurulum
Kullanıcı İşlemleri
Hesap Oluşturma
Hesaba Giriş
Hesaptan Çıkış
Hesap Silme
Tarif İşlemleri
Tarif Oluşturma
Tarif Görüntüleme
Tarif Silme
API Referansı
Kurulum
Projenin çalıştırılması için aşağıdaki adımları izleyin:

Node.js'i bilgisayarınıza yükleyin.

Proje dosyalarını indirin veya klonlayın.

Terminalde proje dizinine gidin ve npm install komutunu çalıştırarak bağımlılıkları yükleyin.

Proje dizininde bir .env dosyası oluşturun ve aşağıdaki ortam değişkenlerini ayarlayın:
DATABASE_URL=<MongoDB veritabanı URL'si>
SECRET_KEY=<gizli anahtar>
  
  Terminalde proje dizininde npm start komutunu çalıştırarak uygulamayı başlatın.

Tarayıcınızda http://localhost:3000 adresine gidin ve Recipe Sharing Platform'u kullanmaya başlayın.

Kullanıcı İşlemleri
Hesap Oluşturma
URL: /register
Metod: POST
Açıklama: Kullanıcı hesabı oluşturma işlemi.
Parametreler:
username (string): Kullanıcı adı.
email (string): Kullanıcı e-posta adresi.
password (string): Kullanıcı şifresi.
  
Örnek İstek:
  {
  "username": "john",
  "email": "john@example.com",
  "password": "123456"
  }
  
Örnek Cevap:
  {
  "message": "Kayıt başarılı"
  }
  
Hesaba Giriş
URL: /login
Metod: POST
Açıklama: Kullanıcı hesabına giriş yapma işlemi.
Parametreler:
email (string): Kullanıcı e-posta adresi.
password (string): Kullanıcı şifresi.
Örnek İstek:
  {
  "email": "john@example.com",
  "password": "123456"
  }
  
Örnek Cevap:
  {
  "token": "<access token>"
  }
  
Hesaptan Çıkış
URL: /logout
Metod: POST
Açıklama: Kullanıcıyı mevcut oturumdan çıkarma işlemi.
Header: Authorization: Bearer <access token>
Örnek Cevap:
  {
  "message": "Hesap başarıyla silindi"
  }
  
Tarif İşlemleri
Tarif Oluşturma
URL: /recipes/create
Metod: POST
Açıklama: Kullanıcı tarafından bir tarifin oluşturulması işlemi.
Header: Authorization: Bearer <access token>
Parametreler:
title (string): Tarif başlığı.
ingredients (array): Tarif malzemeleri.
instructions (string): Tarif talimatları.
Örnek İstek:
  {
  "title": "Mevsim Salatası",
  "ingredients": ["Domates", "Salatalık", "Biber", "Soğan", "Zeytinyağı"],
  "instructions": "1. Sebzeleri doğrayın. 2. Tüm malzemeleri karıştırın. 3. Zeytinyağı ekleyin."
  }
  
Örnek Cevap:
  {
  "message": "Tarif oluşturuldu"
  }
  
Tarif Görüntüleme
URL: /recipes/:id
Metod: GET
Açıklama: Belirli bir tarifin ayrıntılarını görüntüleme işlemi.
Parametreler:
id (string): Tarif ID'si.
Örnek Cevap:
  {
  "id": "123456789",
  "title": "Mevsim Salatası",
  "ingredients": ["Domates", "Salatalık", "Biber", "Soğan", "Zeytinyağı"],
  "instructions": "1. Sebzeleri doğrayın. 2. Tüm malzemeleri karıştırın. 3. Zeytinyağı ekleyin.",
  "createdAt": "2023-06-01T14:30:00.000Z",
  "updatedAt": "2023-06-01T14:30:00.000Z"
  }
  
Tarif Silme
URL: /recipes/:id/delete
Metod: DELETE
Açıklama: Kullanıcı tarafından bir tarifin silinmesi işlemi.
Header: Authorization: Bearer <access token>
Parametreler:
id (string): Tarif ID'si.
Örnek Cevap:
  {
  "message": "Tarif başarıyla silindi"
  }
  
API Referansı
Kullanıcılar
URL: /users

Metod: GET

Açıklama: Tüm kullanıcıların listesini getirir.

URL: /users/:id

Metod: GET

Açıklama: Belirli bir kullanıcının ayrıntılarını getirir.

Tarifler
URL: /recipes

Metod: GET

Açıklama: Tüm tariflerin listesini getirir.

URL: /recipes/:id

Metod: GET

Açıklama: Belirli bir tarifin ayrıntılarını getirir.

URL: /recipes/:id/comments

Metod: GET

Açıklama: Belirli bir tarife ait tüm yorumları getirir.

URL: /recipes/:id/ratings

Metod: GET

Açıklama: Belirli bir tarife ait tüm derecelendirmeleri getirir.

URL: /recipes/:id/comments/create

Metod: POST

Açıklama: Belirli bir tarife yorum ekler.

Header: Authorization: Bearer <access token>

Parametreler:

text (string): Yorum metni.
URL: /recipes/:id/ratings/create

Metod: POST

Açıklama: Belirli bir tarife derecelendirme yapar.

Header: Authorization: Bearer <access token>

Parametreler:

value (number): Derecelendirme değeri (1 ile 5 arasında).
