# 🔥 Hướng dẫn Setup Firebase (MIỄN PHÍ)

## Bước 1: Tạo Firebase Project

1. Truy cập: https://console.firebase.google.com/
2. Click **"Add project"** (Thêm dự án)
3. Đặt tên project: `random-number-game` (hoặc tên bất kỳ)
4. Tắt Google Analytics (không cần thiết) → **Continue**
5. Đợi Firebase tạo project → Click **Continue**

## Bước 2: Tạo Web App

1. Trong Firebase Console, click vào biểu tượng **</> (Web)**
2. Đặt tên app: `Random Game`
3. ✅ Check vào **"Also set up Firebase Hosting"**
4. Click **Register app**
5. **SAO CHÉP** đoạn config này (sẽ dùng sau):

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

## Bước 3: Bật Realtime Database

1. Ở menu bên trái, click **Build** → **Realtime Database**
2. Click **Create Database**
3. Chọn location: **United States (us-central1)**
4. Chọn **"Start in test mode"** → **Enable**

## Bước 4: Cấu hình Security Rules (Quan trọng!)

1. Vào tab **Rules** trong Realtime Database
2. Thay thế rules bằng đoạn này:

```json
{
  "rules": {
    "gameHistory": {
      ".read": true,
      ".write": true
    }
  }
}
```

3. Click **Publish**

⚠️ **LƯU Ý**: Rules này cho phép mọi người đọc/ghi. Để bảo mật hơn, nên thêm authentication sau.

## Bước 5: Cập nhật Code

1. Mở file `index.html`
2. Tìm dòng:
```javascript
const firebaseConfig = {
```

3. Thay thế toàn bộ object `firebaseConfig` bằng config bạn đã copy ở **Bước 2**

4. **LƯU FILE**

## Bước 6: Test & Deploy

### Test Local (không bắt buộc):
```bash
# Mở file index.html trực tiếp trong trình duyệt
```

### Deploy lên GitHub Pages:
```bash
git add .
git commit -m "Add Firebase integration with multiplayer support"
git push origin main
```

## Bước 7: Kiểm tra

1. Truy cập: `https://YOUR_USERNAME.github.io/random-number-game/`
2. Mở 2 tab/cửa sổ khác nhau
3. Quay số ở tab 1 → tab 2 sẽ tự động cập nhật!

---

## 🎯 Tính năng mới:

✅ **Real-time sync** - Đồng bộ giữa nhiều máy/thiết bị
✅ **Nhập tên người chơi** - Lưu lại người đã quay số nào
✅ **Lịch sử chi tiết** - Hiển thị tên + thời gian
✅ **Status badge** - Hiển thị trạng thái Online/Offline
✅ **Reset toàn cục** - Reset sẽ ảnh hưởng tất cả người chơi

---

## ⚠️ Nếu không muốn dùng Firebase:

Trang web sẽ tự động chuyển sang **Offline Mode** và lưu dữ liệu vào **localStorage** của từng máy (không đồng bộ giữa các thiết bị).

---

## 📊 Firebase Free Tier Limits:

- ✅ **1GB storage** (Realtime Database)
- ✅ **10GB/month download**
- ✅ **50,000 reads/day**
- ✅ **20,000 writes/day**

**→ ĐỦ CHO HÀNG NGHÌN LƯỢT CHƠI MỖI NGÀY!**

---

## 🔒 Bảo mật nâng cao (Tùy chọn):

Để chặn spam/abuse, có thể giới hạn:

```json
{
  "rules": {
    "gameHistory": {
      ".read": true,
      ".write": "newData.child('timestamp').val() > now - 1000",
      ".validate": "newData.hasChildren(['number', 'playerName', 'timestamp'])"
    }
  }
}
```

---

**💡 Cần hỗ trợ? Comment hoặc tạo issue!**
