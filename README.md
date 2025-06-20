# 💬 ChatApp

**ChatApp**, Flask + WebSocket + WebRTC + MySQL ile geliştirilmiş gerçek zamanlı bir sohbet ve sesli arama uygulamasıdır.

## 🚀 Özellikler

- 🔐 Kullanıcı kayıt ve giriş (JWT tabanlı kimlik doğrulama)
- ✅ Oturum yönetimi (sessionStorage ile kullanıcı takibi)
- 👤 Aktif kullanıcı listesi
- 💬 Gerçek zamanlı özel & grup mesajlaşma
- 📞 WebRTC ile tarayıcı tabanlı sesli arama
- 🕓 Görüşme süresi ve çağrı geçmişi kaydı
- 📋 Okundu bilgisi (tek ✓ - çift ✓✓)
- 🎨 Responsive modern arayüz

---

## 📁 Proje Yapısı

```
chatapp/
├── app.py
├── auth.py
├── config.py
├── static/
│   ├── main.js
│   ├── style.css
│   └── poster.png
├── templates/
│   ├── login.html
│   ├── register.html
│   └── home.html
├── .env
├── .gitignore
└── README.md
```

---

## ⚙️ Kurulum

1. Depoyu klonla:

```bash
git clone https://github.com/kullaniciadi/chatapp.git
cd chatapp
```

2. Sanal ortam oluştur ve bağımlılıkları yükle:

```bash
python -m venv venv
source venv/bin/activate  # (Windows: venv\Scripts\activate)
pip install -r requirements.txt
```

3. `.env` dosyasını oluştur:

```env
SECRET_KEY=senin-secret-keyin
MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=
MYSQL_DB=chatapp
```

4. MySQL içinde `chatapp` veritabanını oluştur ve aşağıdaki tabloları yükle:

---

## 🗃️ Veritabanı Tabloları

### 📄 `users`

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  uuid VARCHAR(36) UNIQUE,
  username VARCHAR(255) UNIQUE,
  password VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### 💬 `messages`

```sql
CREATE TABLE messages (
  id INT AUTO_INCREMENT PRIMARY KEY,
  room VARCHAR(100),
  sender VARCHAR(100),
  message TEXT,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  is_read TINYINT(1) DEFAULT 0
);
```

---

### 👥 `groups`

```sql
CREATE TABLE groups (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) UNIQUE,
  owner_uuid VARCHAR(36),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (owner_uuid) REFERENCES users(uuid)
);
```

---

### 👤 `group_members`

```sql
CREATE TABLE group_members (
  group_id INT,
  user_uuid VARCHAR(36),
  joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (group_id, user_uuid),
  FOREIGN KEY (group_id) REFERENCES groups(id) ON DELETE CASCADE,
  FOREIGN KEY (user_uuid) REFERENCES users(uuid) ON DELETE CASCADE
);
```

---

### 📞 `call_logs`

```sql
CREATE TABLE call_logs (
  id INT AUTO_INCREMENT PRIMARY KEY,
  caller VARCHAR(50),
  callee VARCHAR(50),
  start_time DATETIME,
  end_time DATETIME,
  duration_seconds INT
);
```

---

## 🖥️ Uygulamayı Başlat

```bash
python app.py
```

Uygulama [http://localhost:5000](http://localhost:5000) adresinde çalışacaktır.

---

## 🧑‍💻 Katkıda Bulunmak

Pull request'ler ve öneriler her zaman memnuniyetle karşılanır!

---

## 👨‍🎓 Geliştirici

Bu proje **[@rasitcanbulat](https://github.com/rasitcanbulat)** tarafından geliştirilmiştir.
