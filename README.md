📘 AWS Serverless Book API – QA Testing Project

Bu proje, AWS üzerinde çalışan sunucusuz (serverless) bir kitap yönetim sisteminin uçtan uca test edilmesi için hazırlanmış profesyonel bir QA portföy projesidir.

Proje kapsamında; Lambda, API Gateway, DynamoDB, S3 ve CloudWatch gibi AWS servislerinin entegrasyonunu test etmek için fonksiyonel, entegrasyon, negatif ve otomasyon testleri tasarlanmıştır.


🚀 Proje Amacı

Gerçek hayattaki AWS tabanlı mikroservis yapısını simüle ederek:
	•	API testi
	•	Entegrasyon testi
	•	IAM/permission testleri
	•	S3 upload senaryoları
	•	CloudWatch log incelemeleri
	•	Java + RestAssured ile API otomasyonu

gibi Cloud QA süreçlerini eksiksiz olarak göstermek.

Bu proje, Cloud QA / API QA pozisyonlarında güçlü bir örnek çalışma sunmak için hazırlanmıştır.

⸻

🧩 Kullanılan AWS Servisleri (Simüle Edilmiş)

Bu projede aşağıdaki AWS servisleri kullanılmıştır (gerçek ortam simüle edilmiştir):
	•	AWS Lambda → CRUD işlemlerini gerçekleştiren fonksiyonlar
	•	API Gateway → Lambda fonksiyonlarını tetikleyen REST endpoint’leri
	•	DynamoDB → Kitap kayıtlarının tutulduğu NoSQL veritabanı
	•	S3 → Kitap kapak resimlerini yüklemek için storage servisi
	•	CloudWatch Logs → Lambda fonksiyon logları

⸻

📁 Proje Yapısı
aws-serverless-book-api-qa/
├── README.md
├── postman_collection/
│     └── BookAPI.postman_collection.json
├── test-cases/
│     ├── functional-tests.xlsx
│     ├── integration-tests.xlsx
│     └── negative-tests.xlsx
├── automation/
│     ├── pom.xml
│     └── src/test/java/api/
│           ├── AddBookTest.java
│           ├── GetBookTest.java
│           ├── UpdateBookTest.java
│           └── DeleteBookTest.java
└── cloudwatch-logs/
      └── sample-log.txt

      🧪 Test Kapsamı

✔ 1. Fonksiyonel Testler (CRUD)
	•	POST /books → Kitap ekleme
	•	GET /books/{id} → Kitap detaylarını getirme
	•	PUT /books/{id} → Kitap güncelleme
	•	DELETE /books/{id} → Kitap silme

Her bir API çağrısı için pozitif ve negatif senaryolar hazırlanmıştır.

⸻

✔ 2. Entegrasyon Testleri
	•	API Gateway → Lambda → DynamoDB veri akışının doğrulanması
	•	DynamoDB’ye eklenen kaydın kontrolü
	•	Update sonrası değişen verilerin doğrulanması
	•	Silme işlemi sonrası verinin kaybolduğunun teyidi
	•	İşlem loglarının CloudWatch’a düşüp düşmediğinin incelenmesi

⸻

✔ 3. Permission / IAM Testleri

Gerçek AWS ortamında sık yaşanan izin problemleri simüle edilmiştir.

Aşağıdaki durumlar test edilmiştir:
	•	Eksik IAM rolü → 403 Forbidden
	•	Yanlış permission → 500 Internal Error
	•	API Key olmadan istek → 401 Unauthorized

⸻

✔ 4. S3 Upload Testleri

S3 bucket’ına resim yükleme senaryoları hazırlanmıştır:
	•	Geçerli PNG/JPEG dosyası → 200 OK
	•	5MB üstü dosya → 413 Payload Too Large
	•	Yanlış uzantı (.exe, .txt) → 400 Bad Request

⸻

🤖 Otomasyon Testleri (Java + RestAssured)

Proje içinde örnek API otomasyon testleri bulunmaktadır.

Örnek test sınıfı:
@Test
public void addBookTest() {
    given()
        .contentType("application/json")
        .body("{\"bookId\":\"1\", \"title\":\"API Testing\", \"author\":\"Gulcan\"}")
    .when()
        .post(baseUrl + "/books")
    .then()
        .statusCode(200)
        .body("message", equalTo("Book added successfully"));
}

🔍 CloudWatch Log Örneği

cloudwatch-logs/sample-log.txt içinde Lambda fonksiyonları için örnek loglar yer almaktadır.

START RequestId: 12345 Version: $LATEST
Book added: API Testing (ID: 1)
END RequestId: 12345
REPORT Duration: 56 ms  Billed Duration: 100 ms  Memory Size: 128 MB 

🛠️ Kullanım

1. Postman Koleksiyonu

postman_collection/ klasöründeki dosyayı Postman’e import ederek tüm API’lere otomatik erişebilirsiniz.

2. Test Case Dokümanları

test-cases/ klasörü fonksiyonel, entegrasyon ve negatif testlerin tamamını içerir.

3. Otomasyon Testleri

Aşağıdaki komut ile otomasyonları çalıştırabilirsiniz:

mvn test


⸻

👤 QA Sorumlusu

Tester: Gülcan Çelik
Role: QA Engineer / Cloud QA
GitHub: https://github.com/gulcannce

⭐ Sonuç
Bu proje, AWS altyapısı üzerinde çalışan serverless bir API’nin uçtan uca test edilmesi için hazırlanmıştır.
Gerçek iş ortamında karşılaşılan Cloud QA senaryolarının büyük bir kısmını simüle eder.
