# 📚 Hướng Dẫn Sử Dụng Git cho Dự Án TPS5430

![Git Guide](https://img.shields.io/badge/Git-Hướng%20dẫn%20cơ%20bản-red)
![Vietnamese](https://img.shields.io/badge/Language-Tiếng%20Việt-blue)

## 📖 Mục Lục
1. [Git là gì?](#git-là-gì)
2. [Cài đặt Git](#cài-đặt-git)
3. [Cấu hình ban đầu](#cấu-hình-ban-đầu)
4. [Các khái niệm cơ bản](#các-khái-niệm-cơ-bản)
5. [Quy trình làm việc (Gitflow)](#quy-trình-làm-việc-gitflow)
6. [Các lệnh Git thường dùng](#các-lệnh-git-thường-dùng)
7. [Hướng dẫn chi tiết từng bước](#hướng-dẫn-chi-tiết-từng-bước)
8. [Xử lý Conflict](#xử-lý-conflict)
9. [Lưu ý quan trọng](#lưu-ý-quan-trọng)
10. [Câu hỏi thường gặp](#câu-hỏi-thường-gặp)

---

## 🤔 Git là gì?

**Git** là một hệ thống quản lý phiên bản phân tán (Version Control System) giúp:
- 📝 Lưu trữ lịch sử thay đổi của dự án
- 👥 Nhiều người cùng làm việc trên một dự án
- 🔄 Quay lại phiên bản cũ khi cần
- 🌿 Phát triển nhiều tính năng song song
- 🔍 Theo dõi ai đã thay đổi gì và khi nào

**Ví dụ thực tế:** Giống như Google Docs có lịch sử chỉnh sửa, nhưng mạnh mẽ hơn nhiều!

---

## 💻 Cài đặt Git

### Windows
1. Tải Git từ: https://git-scm.com/download/win
2. Chạy file cài đặt (`.exe`)
3. Sử dụng các tùy chọn mặc định (nhấn Next liên tục)
4. Khuyến nghị: Chọn "Git Bash" làm terminal

### macOS
```bash
# Sử dụng Homebrew (khuyến nghị)
brew install git

# Hoặc tải từ website
# https://git-scm.com/download/mac
```

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### Kiểm tra cài đặt
```bash
git --version
# Kết quả mong đợi: git version 2.x.x
```

---

## ⚙️ Cấu hình ban đầu

Sau khi cài đặt Git, bạn cần cấu hình tên và email (chỉ làm 1 lần):

```bash
# Thiết lập tên của bạn
git config --global user.name "Nguyen Van A"

# Thiết lập email của bạn
git config --global user.email "nguyenvana@example.com"

# Kiểm tra cấu hình
git config --list
```

> **💡 Lưu ý:** Tên và email này sẽ xuất hiện trong lịch sử commit. Nên dùng tên thật để mọi người biết ai đã thay đổi code.

---

## 📚 Các khái niệm cơ bản

### 1. Repository (Repo)
**Là gì?** Kho lưu trữ dự án, chứa tất cả file và lịch sử thay đổi.
- **Remote Repository:** Kho trên GitHub/GitLab (kho trung tâm)
- **Local Repository:** Kho trên máy tính của bạn

### 2. Commit
**Là gì?** Một "bản chụp" (snapshot) của dự án tại một thời điểm.
- Mỗi commit có một thông điệp (message) mô tả thay đổi
- Ví dụ: "Thêm sơ đồ mạch cho Buck Converter"

### 3. Branch (Nhánh)
**Là gì?** Một "nhánh" phát triển riêng biệt.
- `main`: Nhánh chính, chứa code ổn định
- `develop`: Nhánh phát triển chung
- `feature/xxx`: Nhánh cho tính năng mới

**Ví dụ:** 
- Bạn A làm sơ đồ mạch trên nhánh `feature/Schematic`
- Bạn B làm PCB trên nhánh `feature/PCB-Layout`
- Sau đó merge (gộp) vào `develop`

### 4. Merge
**Là gì?** Gộp các thay đổi từ nhánh này sang nhánh khác.

### 5. Pull Request (PR)
**Là gì?** Đề xuất merge code của bạn vào nhánh chung.
- Cho phép team review code trước khi merge
- Tránh lỗi và học hỏi lẫn nhau

### 6. Conflict
**Là gì?** Xung đột xảy ra khi 2 người sửa cùng một dòng code.
- Git không biết nên giữ thay đổi của ai
- Bạn cần chọn thủ công

---

## 🌊 Quy trình làm việc (Gitflow)

Dự án của chúng ta sử dụng **Gitflow Workflow**:

```
main (sản phẩm hoàn chỉnh)
  ↑
develop (phát triển chung)
  ↑
feature/Schematic (bạn đang làm)
feature/PCB-Layout (bạn khác đang làm)
```

### Quy tắc làm việc:

1. ⛔ **KHÔNG BAO GIỜ** commit trực tiếp vào `main`
2. ⚠️ **CẨN THẬN** khi commit vào `develop`
3. ✅ **NÊN** tạo nhánh `feature/` cho công việc của mình
4. 🔄 Thường xuyên pull từ `develop` để cập nhật
5. 📝 Viết commit message rõ ràng

---

## 🛠️ Các lệnh Git thường dùng

### Bảng tóm tắt nhanh

| Lệnh | Chức năng |
|------|-----------|
| `git clone <url>` | Tải dự án về máy |
| `git status` | Xem trạng thái hiện tại |
| `git branch` | Xem danh sách nhánh |
| `git checkout <branch>` | Chuyển sang nhánh khác |
| `git pull` | Cập nhật code mới nhất |
| `git add <file>` | Thêm file vào staging |
| `git commit -m "message"` | Lưu thay đổi |
| `git push` | Đẩy code lên GitHub |
| `git merge <branch>` | Gộp nhánh |

---

## 📋 Hướng dẫn chi tiết từng bước

### 🚀 Bước 1: Clone dự án lần đầu

```bash
# Di chuyển đến thư mục làm việc
cd Desktop

# Clone dự án về máy
git clone https://github.com/nhq441/design_TPS5430_regulator.git

# Vào thư mục dự án
cd design_TPS5430_regulator
```

**Kết quả:** Bạn có một bản sao dự án trên máy.

---

### 🌿 Bước 2: Tạo nhánh feature mới

```bash
# Đảm bảo bạn đang ở nhánh develop
git checkout develop

# Cập nhật develop về mới nhất
git pull origin develop

# Tạo nhánh mới cho công việc của bạn
git checkout -b feature/Ten-Tinh-Nang

# Ví dụ thực tế:
git checkout -b feature/Schematic-Design
# hoặc
git checkout -b feature/PCB-Layout
# hoặc
git checkout -b feature/Add-Documentation
```

**Giải thích:**
- `checkout -b`: Tạo và chuyển sang nhánh mới
- `feature/`: Tiền tố bắt buộc theo Gitflow
- `Ten-Tinh-Nang`: Mô tả ngắn gọn công việc

---

### ✏️ Bước 3: Làm việc và commit

```bash
# 1. Xem file nào đã thay đổi
git status

# 2. Thêm file vào staging (chuẩn bị commit)
# Thêm 1 file cụ thể
git add Kicad/Buck_TPS5430_Project/Buck_TPS5430_Project.kicad_sch

# Hoặc thêm tất cả file thay đổi
git add .

# 3. Commit với message rõ ràng
git commit -m "Thêm sơ đồ mạch Buck Converter TPS5430"

# Ví dụ commit message tốt:
git commit -m "Thêm feedback resistors R1, R2 cho VSENSE"
git commit -m "Sửa lỗi kết nối enable pin"
git commit -m "Cập nhật layout PCB 2 layer"
git commit -m "Thêm tài liệu hướng dẫn tính toán feedback"
```

**❌ Ví dụ commit message XẤU:**
```bash
git commit -m "update"
git commit -m "fix"
git commit -m "abc"
git commit -m "ok"
```

---

### 🔄 Bước 4: Đẩy code lên GitHub

```bash
# Lần đầu push nhánh mới
git push -u origin feature/Ten-Tinh-Nang

# Các lần sau chỉ cần
git push
```

**Giải thích:**
- `-u origin feature/...`: Liên kết nhánh local với remote
- Sau lần đầu, chỉ cần `git push`

---

### 🔀 Bước 5: Tạo Pull Request (trên GitHub)

1. Vào https://github.com/nhq441/design_TPS5430_regulator
2. Bạn sẽ thấy thông báo: "Compare & pull request"
3. Click vào nút đó
4. Điền thông tin:
   - **Title:** Mô tả ngắn gọn (VD: "Thêm sơ đồ mạch Buck Converter")
   - **Description:** Mô tả chi tiết những gì bạn đã làm
   - **Base branch:** Chọn `develop`
   - **Compare branch:** Nhánh feature của bạn
5. Click "Create Pull Request"
6. Đợi team leader review và merge

---

### 🔄 Bước 6: Cập nhật code mới nhất

**Tình huống:** Đồng đội đã merge code mới vào `develop`, bạn cần cập nhật.

```bash
# Chuyển sang nhánh develop
git checkout develop

# Kéo code mới nhất về
git pull origin develop

# Quay lại nhánh feature của bạn
git checkout feature/Ten-Tinh-Nang

# Merge code mới từ develop vào nhánh của bạn
git merge develop
```

**💡 Lưu ý:** Nên làm việc này hàng ngày để tránh conflict lớn!

---

### 🔄 Bước 7: Cập nhật nhánh feature đang làm

**Tình huống:** Bạn đang làm việc, có code mới trên nhánh feature của bạn (do bạn làm trên máy khác hoặc đồng đội làm).

```bash
# Kéo code mới nhất về nhánh hiện tại
git pull
```

---

## ⚔️ Xử lý Conflict

### Conflict xảy ra khi nào?
- 2 người sửa cùng một dòng code
- Một người xóa file, người khác sửa file đó

### Ví dụ conflict:

Giả sử file `README.md` bị conflict:

```
<<<<<<< HEAD
**Output Voltage 1** | **5.0V** | Regulated via TPS5430
=======
**Output Voltage 1** | **5.0V/12V** | Regulated via TPS5430
>>>>>>> develop
```

**Giải thích:**
- `<<<<<<< HEAD`: Phần code của bạn
- `=======`: Dấu phân cách
- `>>>>>>> develop`: Phần code từ develop

### Cách xử lý:

**Cách 1: Dùng editor thủ công**
```bash
# 1. Mở file conflict bằng text editor
# 2. Xóa các dấu conflict (<<<, ===, >>>)
# 3. Chọn code muốn giữ hoặc gộp cả 2
# 4. Lưu file
# 5. Add và commit

git add README.md
git commit -m "Giải quyết conflict trong README.md"
```

**Cách 2: Dùng VS Code (khuyến nghị)**
- VS Code tự động highlight conflict
- Có nút "Accept Current Change", "Accept Incoming Change", "Accept Both"

**Cách 3: Dùng merge tool**
```bash
# KDiff3, Meld, P4Merge...
git mergetool
```

---

## 🎯 Workflow hoàn chỉnh - Ví dụ thực tế

### Ví dụ: Bạn được giao nhiệm vụ thiết kế sơ đồ mạch

```bash
# 1️⃣ Bắt đầu từ develop
git checkout develop
git pull origin develop

# 2️⃣ Tạo nhánh feature
git checkout -b feature/Schematic-Design

# 3️⃣ Mở KiCad, thiết kế sơ đồ
# ... làm việc ...

# 4️⃣ Lưu và commit (làm nhiều lần trong ngày)
git add .
git commit -m "Thêm TPS5430 IC vào schematic"

# Tiếp tục làm việc...
git add .
git commit -m "Thêm input capacitor 100uF"

# Tiếp tục làm việc...
git add .
git commit -m "Thêm feedback resistor network"

# 5️⃣ Push lên GitHub (cuối ngày hoặc khi cần backup)
git push -u origin feature/Schematic-Design

# 6️⃣ Ngày hôm sau, cập nhật develop
git checkout develop
git pull origin develop
git checkout feature/Schematic-Design
git merge develop

# 7️⃣ Tiếp tục làm việc...
git add .
git commit -m "Hoàn thành schematic design"
git push

# 8️⃣ Tạo Pull Request trên GitHub
# Vào GitHub → Compare & Pull Request → Create

# 9️⃣ Sau khi được merge, xóa nhánh feature (tùy chọn)
git checkout develop
git pull origin develop
git branch -d feature/Schematic-Design
```

---

## ⚠️ Lưu ý quan trọng

### ✅ NÊN:
- ✅ Commit thường xuyên (nhiều commit nhỏ > 1 commit lớn)
- ✅ Viết commit message rõ ràng, bằng tiếng Việt hoặc tiếng Anh
- ✅ Pull code mới từ `develop` mỗi ngày
- ✅ Push code lên GitHub thường xuyên (để backup)
- ✅ Tạo nhánh feature riêng cho mỗi tính năng
- ✅ Kiểm tra kỹ trước khi commit (dùng `git status`)

### ❌ KHÔNG NÊN:
- ❌ Commit file không liên quan (file temp, cache, build...)
- ❌ Commit trực tiếp vào `main`
- ❌ Commit code chưa test
- ❌ Dùng `git push -f` (force push) trừ khi biết rõ mình làm gì
- ❌ Commit thông tin nhạy cảm (password, API key)
- ❌ Viết commit message mơ hồ

---

## 🆘 Các tình huống cứu cánh

### 😱 "Tôi commit nhầm file!"

```bash
# Nếu chưa push
git reset HEAD~1  # Hủy commit gần nhất, giữ lại thay đổi
git reset --hard HEAD~1  # Hủy commit và xóa luôn thay đổi
```

### 😱 "Tôi làm sai nhánh!"

```bash
# Bạn đang ở develop nhưng cần ở feature
git stash  # Cất thay đổi tạm thời
git checkout feature/Ten-Nhanh
git stash pop  # Lấy thay đổi ra
```

### 😱 "Tôi muốn hủy tất cả thay đổi chưa commit"

```bash
# Hủy thay đổi của 1 file
git checkout -- ten_file.txt

# Hủy TẤT CẢ thay đổi (⚠️ NGUY HIỂM!)
git reset --hard HEAD
```

### 😱 "Tôi muốn xem ai đã sửa dòng này"

```bash
git blame ten_file.txt
```

### 😱 "Tôi push nhầm, muốn quay lại"

```bash
# ⚠️ CHỈ LÀM NẾU CHƯA AI PULL CODE CỦA BẠN!
git reset --hard HEAD~1
git push -f origin feature/Ten-Nhanh
```

---

## ❓ Câu hỏi thường gặp

### Q: Git khác GitHub như thế nào?
**A:** 
- **Git:** Phần mềm quản lý version (cài trên máy)
- **GitHub:** Website lưu trữ code online (như Google Drive cho code)

### Q: Khi nào nên commit?
**A:** Sau mỗi thay đổi logic hoàn chỉnh. Ví dụ:
- ✅ "Thêm R1, R2 cho feedback network"
- ✅ "Sửa lỗi connection ENA pin"
- ❌ Không nên: Sau mỗi lần nhấn Ctrl+S

### Q: Tôi có thể xóa file commit cũ không?
**A:** Không nên! Git được thiết kế để lưu lịch sử. Nếu thực sự cần, dùng `git rebase` (nâng cao).

### Q: File nào không nên commit?
**A:** 
- File build: `.o`, `.exe`, `.bin`
- File temp: `~`, `.swp`, `.tmp`
- File IDE: `.vscode/`, `.idea/`
- File lớn: video, zip (dùng Git LFS)
- **Đã có `.gitignore` giúp bạn!**

### Q: Pull Request và Merge khác nhau?
**A:**
- **Pull Request:** Đề xuất merge trên GitHub (có review)
- **Merge:** Lệnh Git gộp nhánh (không có review)

### Q: Tôi nên đặt tên nhánh như thế nào?
**A:** 
- Format: `feature/ten-tinh-nang`
- Ví dụ tốt: `feature/add-ldo-circuit`, `feature/pcb-routing`
- Ví dụ xấu: `test`, `my-branch`, `abc`

---

## 📖 Tài liệu tham khảo

### Học thêm về Git
- **Git Book (Tiếng Việt):** https://git-scm.com/book/vi/v2
- **Git Cheat Sheet:** https://education.github.com/git-cheat-sheet-education.pdf
- **Interactive Git Tutorial:** https://learngitbranching.js.org/

### Video hướng dẫn
- Cơ bản: https://www.youtube.com/watch?v=DVRQoVRzMIY (tiếng Việt)
- Nâng cao: https://www.youtube.com/watch?v=Uszj_k0DGsg (tiếng Anh)

---

## 🎓 Bài tập thực hành

### Bài 1: Clone và khám phá
```bash
git clone https://github.com/nhq441/design_TPS5430_regulator.git
cd design_TPS5430_regulator
git log --oneline  # Xem lịch sử commit
git branch -a      # Xem tất cả nhánh
```

### Bài 2: Tạo nhánh và commit
```bash
git checkout -b feature/Practice
echo "Tôi đang học Git" > test.txt
git add test.txt
git commit -m "Thêm file test"
git push -u origin feature/Practice
```

### Bài 3: Merge và xử lý conflict

**Mục tiêu:** Học cách merge nhánh và xử lý conflict cơ bản

#### Bước 1: Tạo 2 nhánh để thực hành
```bash
# Tạo file test chung
git checkout develop
echo "Line 1: Original content" > conflict_test.txt
git add conflict_test.txt
git commit -m "Add conflict test file"
git push

# Tạo nhánh A và sửa file
git checkout -b feature/test-A
echo "Line 1: Modified by Person A" > conflict_test.txt
git add conflict_test.txt
git commit -m "Person A changes"
git push -u origin feature/test-A

# Quay lại develop và tạo nhánh B
git checkout develop
git checkout -b feature/test-B
echo "Line 1: Modified by Person B" > conflict_test.txt
git add conflict_test.txt
git commit -m "Person B changes"
git push -u origin feature/test-B
```

#### Bước 2: Thử merge (sẽ gặp conflict)
```bash
# Ở nhánh feature/test-B, merge nhánh feature/test-A
git checkout feature/test-B
git merge feature/test-A
# Kết quả: CONFLICT! 🔥
```

#### Bước 3: Xử lý conflict
```bash
# Xem file bị conflict
cat conflict_test.txt
# Sẽ thấy:
# <<<<<<< HEAD
# Line 1: Modified by Person B
# =======
# Line 1: Modified by Person A
# >>>>>>> feature/test-A

# Mở file bằng editor và sửa thành:
# Line 1: Modified by Person A and B

# Sau khi sửa xong:
git add conflict_test.txt
git commit -m "Resolve conflict between A and B"
git push
```

#### Bước 4: Dọn dẹp
```bash
# Xóa các nhánh test
git checkout develop
git branch -d feature/test-A
git branch -d feature/test-B
git push origin --delete feature/test-A
git push origin --delete feature/test-B
```

**💡 Mẹo:** 
- Dùng VS Code để xử lý conflict dễ hơn (có nút Accept Current/Incoming Change)
- Nếu conflict phức tạp, hỏi người gây conflict để quyết định giữ code nào
- **Nếu gặp lỗi hoặc không biết xử lý, liên hệ hỗ trợ ngay!**

---

## 📞 Liên hệ hỗ trợ

Nếu gặp vấn đề:
1. 🔍 Google lỗi (90% đã có người gặp)
2. 💬 Hỏi team trên Zalo/Slack
3. 📧 Email team leader
4. 🌐 Đọc tài liệu Git Book

---

## 🎉 Kết luận

Git nghe có vẻ phức tạp nhưng bạn chỉ cần nhớ:

```
1. git pull      → Lấy code mới
2. (làm việc)
3. git add .     → Chuẩn bị commit
4. git commit    → Lưu thay đổi
5. git push      → Đẩy lên GitHub
```

**Thực hành nhiều là thành thạo!** 💪

---

*Tài liệu được tạo cho dự án TPS5430 Buck Converter*  
*Cập nhật lần cuối: Tháng 2, 2026*🚀
