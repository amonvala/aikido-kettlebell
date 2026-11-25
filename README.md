# aikido-kettlebell

Metabolik Güç & Aikido kettlebell koçu. Tek dosyalık web uygulaması (`index.html`).

## Kayıtlar nerede tutulur?

- **Firebase ayarı yoksa:** Günlük ve profiller o cihazın tarayıcısında saklanır.
  Başka cihaza geçmek için Günlük sekmesinden JSON yedeği alınıp diğer cihazda yüklenir.
- **Firebase ayarı varsa:** Aile Google hesabıyla giriş yapılan her cihaz aynı günlüğü ve
  profilleri görür. İnternet yokken alınan kayıtlar bağlantı gelince gönderilir.

## Aile bulutu kurulumu (ücretsiz)

Firebase'in **Spark** planı ücretsizdir ve kredi kartı istemez. Ücretli plana (Blaze) geçilmediği
sürece fatura çıkmaz; kota aşılırsa o gün yalnızca bulut durur. Bir ailenin kullanımı kotanın
çok altındadır (günde 50.000 okuma / 20.000 yazma).

1. <https://console.firebase.google.com> adresinde aile hesabıyla yeni proje oluşturun.
   Google Analytics gerekmez. Plan olarak Spark (ücretsiz) kalsın.
2. **Build > Authentication > Get started > Sign-in method > Google**'ı etkinleştirin.
3. **Authentication > Settings > Authorized domains** listesine uygulamanın açılacağı adresi
   ekleyin (ör. `kullaniciadi.github.io`). `localhost` zaten eklidir.
4. **Build > Firestore Database > Create database**: konum olarak `eur3 (europe-west)` seçin,
   "production mode" ile başlatın.
5. **Firestore > Rules** sekmesine `firestore.rules` dosyasının içeriğini yapıştırın,
   `AILE_HESABI@gmail.com` yerine aile hesabının adresini yazıp **Publish** deyin.
   (Gerçek adresi bu depoya yazmayın.)
6. **Project settings > General > Your apps > Web (`</>`)** ile bir web uygulaması ekleyin.
   Hosting kutusunu işaretlemeyin. Verilen `firebaseConfig` nesnesini `index.html` içindeki
   `const FIREBASE_CONFIG = null;` satırında `null` yerine yapıştırın.
7. Uygulamayı açın, **Günlük** sekmesinde **Aile Hesabıyla Giriş** deyin. Daha önce o cihazda
   tutulan kayıtlar varsa "Bu cihazdaki N kaydı aktar" düğmesiyle aile günlüğüne taşıyın.

`firebaseConfig` değerleri gizli değildir; GitHub'da durabilir. Verilere erişimi 5. adımdaki
kurallar korur: yalnızca aile hesabıyla giriş yapan okuyup yazabilir.
