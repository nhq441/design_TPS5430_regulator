📘 GIT_GUIDE.md
Hướng dẫn Git cho Team (Dự án Buck Converter)

Tài liệu này dành cho thành viên chưa quen sử dụng Git.
Mục tiêu: Làm việc an toàn – không làm hỏng nhánh chính – không gây xung đột file KiCad.

1️⃣ Hiểu đúng trước khi thao tác

Hãy nắm 3 khái niệm quan trọng nhất:

🔹 Repository (Repo)

Kho lưu trữ toàn bộ dự án trên GitHub.

🔹 Clone

Tải toàn bộ repo về máy tính của bạn.

🔹 Branch (Nhánh) — QUAN TRỌNG NHẤT

Dự án sử dụng mô hình Gitflow:

main → phiên bản ổn định cuối cùng
❌ Tuyệt đối không sửa trực tiếp

develop → nơi tổng hợp code để test

feature/... → nhánh cá nhân để làm việc
✔ Làm sai có thể xoá và làm lại
✔ Không ảnh hưởng người khác

Ví dụ tên nhánh:

feature/mach-nguon
feature/schematic-mcu
feature/tai-lieu

2️⃣ Cài đặt môi trường

Cài Git SCM
https://git-scm.com/downloads

→ Cài mặc định (Next liên tục)

Nên dùng một trong hai:

GitHub Desktop (dễ dùng)

VS Code (có tích hợp Git)

Tạo tài khoản GitHub và gửi email cho trưởng nhóm để được thêm vào repo.

3️⃣ Quy trình làm việc chuẩn (BẮT BUỘC TUÂN THỦ)
🔰 Lần đầu tiên

Mở Terminal (hoặc Git Bash) tại thư mục muốn lưu project:

git clone https://github.com/nhq441/design_TPS5430_regulator.git


Sau đó vào thư mục dự án:

cd design_TPS5430_regulator

🔄 Quy trình làm việc mỗi ngày
Bước 1 — Cập nhật nhánh develop
git checkout develop
git pull origin develop


Luôn đảm bảo bạn đang làm việc trên phiên bản mới nhất.

Bước 2 — Tạo nhánh riêng để làm việc
git checkout -b feature/ten-cong-viec


Ví dụ:

git checkout -b feature/thiet-ke-mcu


Từ đây trở đi, mọi thay đổi chỉ nằm trong nhánh của bạn.

Bước 3 — Commit và Push

Sau khi hoàn thành công việc:

Lưu file bình thường trong KiCad

Đóng KiCad hoàn toàn (tránh lỗi file lock)

Thực hiện:

git add .
git commit -m "Hoàn thiện schematic khối MCU"
git push origin feature/thiet-ke-mcu

Bước 4 — Tạo Pull Request

Vào GitHub

Nhấn Compare & pull request

Chọn:

Base: develop

Compare: feature/...

Viết mô tả rõ ràng bạn đã làm gì

Nhấn Create pull request

Báo trưởng nhóm review

⚠️ Lưu ý cực kỳ quan trọng khi dùng KiCad với Git
❌ Không bao giờ force push nếu không hiểu rõ
git push --force


Lệnh này có thể ghi đè công việc của người khác.

⚠ Conflict với file KiCad

File:

.kicad_pcb

.kicad_sch

rất khó merge tự động.

👉 Quy tắc an toàn:

Không sửa cùng một file PCB cùng lúc

Phân chia module rõ ràng

Thông báo khi bắt đầu sửa PCB

🚨 Nếu xảy ra lỗi

Không tự ý thử lệnh lung tung

Chụp màn hình

Báo trưởng nhóm ngay

4️⃣ Quy định quản lý Repo (Dành cho Leader)

Nếu bạn là người quản lý repo, nên thực hiện:

🔒 1. Bảo vệ nhánh

Vào:

GitHub → Settings → Branches


Thiết lập cho main và develop:

✅ Require a pull request before merging

Việc này ngăn push trực tiếp lên nhánh chính.

🧹 2. Cấu hình .gitignore cho KiCad

Đảm bảo đã loại bỏ:

*.lck
*.bkp
fp-info-cache


Tránh commit file rác.

🧩 3. Sử dụng Hierarchical Sheets (KiCad 6+)

Nên chia:

Nguồn

MCU

IO

Communication

thành các sheet riêng biệt.

Lợi ích:

Giảm conflict

Nhiều người làm song song

Dễ bảo trì

🎯 Nguyên tắc làm việc của Team

Không sửa trực tiếp main

Không merge khi chưa review

Không sửa file PCB của người khác khi chưa trao đổi

Luôn commit với message rõ ràng

Chúc team hoàn thành đồ án suôn sẻ và không gặp conflict 🔧🚀