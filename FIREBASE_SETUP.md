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
    },
    "password": {
      ".read": true,
      ".write": false
    },
    "maxNumber": {
      ".read": true,
      ".write": true
    }
  }
}
```

3. Click **Publish**

⚠️ **LƯU Ý**: 
- `gameHistory`: Cho phép mọi người đọc/ghi để chơi game
- `password`: Chỉ cho phép đọc, không cho phép ghi từ client (bảo vệ mật khẩu admin)
- `maxNumber`: Cho phép đọc/ghi (Admin sẽ xác thực bằng mật khẩu trong code trước khi ghi)
- `password`: Chỉ cho phép đọc, không cho phép ghi từ client (bảo vệ mật khẩu admin)
- `maxNumber`: Chỉ cho phép đọc, không cho phép ghi từ client (bảo vệ cấu hình số lượng)

## Bước 4.5: Thêm Cấu hình Game trong Firebase

1. Vào tab **Data** trong Realtime Database
2. Click vào **root** (dấu + đầu tiên)
3. Thêm các key sau:

### 3.1. Thêm Mật Khẩu Admin:
   - **Name**: `password`
   - **Value**: `11August` (hoặc mật khẩu bạn muốn)
   - Click **Add**

### 3.2. Thêm Số Lượng Số:
   - **Name**: `maxNumber`
   - **Value**: `10` (hoặc 30, 50, 100 tùy bạn muốn)
   - Click **Add**

🎲 **Lưu ý về maxNumber:**
- Giá trị `10` → Game sẽ quay số từ 1-10
- Giá trị `30` → Game sẽ quay số từ 1-30
- Giá trị `100` → Game sẽ quay số từ 1-100
- Bạn có thể thay đổi giá trị này bất cứ lúc nào trên Firebase, game sẽ tự động cập nhật!

🔒 **Mật khẩu sẽ được dùng để reset game và chỉ Admin biết!**

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
