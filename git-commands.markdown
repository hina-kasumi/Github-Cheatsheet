# Các Câu Lệnh Git Phổ Biến

Dưới đây là danh sách các câu lệnh Git phổ biến, được sử dụng rộng rãi trong các dự án.

## 1. Thiết Lập và Cấu Hình
- `git init`: Khởi tạo một repository Git mới trong thư mục hiện tại.
- `git clone <repository-url>`: Sao chép một repository từ remote về máy cục bộ.
- `git config --global user.name "<tên>"`: Thiết lập tên người dùng cho Git.
- `git config --global user.email "<email>"`: Thiết lập email người dùng cho Git.
- `git config --list`: Hiển thị tất cả cấu hình Git hiện tại.

## 2. Làm Việc Với Branch
- `git branch`: Liệt kê tất cả các branch trong repository.
- `git branch <branch-name>`: Tạo một branch mới.
- `git checkout <branch-name>`: Chuyển sang branch được chỉ định.
- `git checkout -b <branch-name>`: Tạo và chuyển sang branch mới.
- `git merge <branch-name>`: Hợp nhất branch được chỉ định vào branch hiện tại.
- `git branch -d <branch-name>`: Xóa branch đã được hợp nhất.
- `git branch -D <branch-name>`: Xóa branch ngay cả khi chưa được hợp nhất.

## 3. Làm Việc Với Commit
- `git status`: Kiểm tra trạng thái của working directory và staging area.
- `git add <file>`: Thêm file vào staging area.
- `git add .`: Thêm tất cả các file thay đổi vào staging area.
- `git commit -m "<message>"`: Tạo commit với thông điệp mô tả.
- `git commit --amend`: Sửa đổi commit gần nhất (thêm file hoặc chỉnh sửa message).
- `git log`: Xem lịch sử commit.
- `git log --oneline`: Xem lịch sử commit dưới dạng ngắn gọn.

## 4. Làm Việc Với Remote Repository
- `git remote add origin <repository-url>`: Liên kết repository cục bộ với remote repository.
- `git push origin <branch-name>`: Đẩy branch lên remote repository.
- `git pull origin <branch-name>`: Kéo code từ remote repository về và hợp nhất.
- `git fetch origin`: Lấy dữ liệu từ remote repository nhưng không hợp nhất.
- `git remote -v`: Xem danh sách các remote repository được cấu hình.

## 5. Xử Lý Xung Đột và Hoàn Tác
- `git revert <commit-id>`: Tạo commit mới để hoàn tác một commit cụ thể.
- `git reset --soft <commit-id>`: Hoàn tác commit nhưng giữ lại các thay đổi trong staging area.
- `git reset --hard <commit-id>`: Hoàn tác commit và xóa luôn các thay đổi.
- `git restore <file>`: Khôi phục file trong working directory về trạng thái của commit gần nhất.
- `git restore --staged <file>`: Loại bỏ file khỏi staging area nhưng giữ nguyên thay đổi trong working directory.
- `git stash`: Lưu trữ tạm thời các thay đổi chưa commit vào stash.
- `git stash pop`: Khôi phục các thay đổi gần nhất từ stash và xóa nó khỏi danh sách stash.
- `git stash apply`: Áp dụng các thay đổi từ stash nhưng không xóa nó khỏi danh sách stash.
- `git stash list`: Hiển thị danh sách các stash hiện có.
- `git stash drop <stash-id>`: Xóa một stash cụ thể (ví dụ: `stash@{0}`).
- `git stash clear`: Xóa toàn bộ danh sách stash.
- `git mergetool`: Sử dụng công cụ để giải quyết xung đột merge.

## 6. Kiểm Tra và So Sánh
- `git diff`: Xem sự khác biệt giữa working directory và staging area.
- `git diff --staged`: Xem sự khác biệt giữa staging area và commit gần nhất.
- `git blame <file>`: Xem thông tin chi tiết về người thay đổi từng dòng trong file.
- `git show <commit-id>`: Xem chi tiết một commit cụ thể.

## 7. Rebase và Quản Lý Lịch Sử Nâng Cao
- `git rebase <branch-name>`: Di chuyển hoặc hợp nhất các commit từ branch hiện tại lên branch được chỉ định, tạo lịch sử commit tuyến tính hơn.
- `git rebase -i <commit-id>`: Thực hiện rebase tương tác để chỉnh sửa, gộp, hoặc xóa các commit (bắt đầu từ commit sau `<commit-id>`).
- `git rebase --continue`: Tiếp tục quá trình rebase sau khi giải quyết xung đột.
- `git rebase --abort`: Hủy bỏ quá trình rebase và quay lại trạng thái trước khi rebase.
- `git cherry-pick <commit-id>`: Áp dụng một commit cụ thể từ branch khác vào branch hiện tại.
- `git tag <tag-name>`: Tạo một tag để đánh dấu một commit cụ thể (thường dùng cho phiên bản release).
- `git push origin <tag-name>`: Đẩy tag lên remote repository.
- `git submodule add <repository-url>`: Thêm một submodule vào repository.

## 8. Quản Lý Lịch Sử và Dọn Dẹp
- `git clean -fd`: Xóa các file và thư mục không được theo dõi bởi Git.
- `git gc`: Dọn dẹp và tối ưu hóa repository.
- `git reflog`: Xem lịch sử các thao tác trên HEAD (hữu ích để khôi phục commit bị xóa).

## Lưu Ý
- **Backup thường xuyên**: Trước khi thực hiện các lệnh như `reset`, `rebase`, hoặc `merge`, hãy đảm bảo bạn đã sao lưu hoặc đẩy code lên remote.
- **Thông điệp commit rõ ràng**: Viết thông điệp commit ngắn gọn, mô tả chính xác những gì đã thay đổi.
- **Kiểm tra trước khi merge hoặc rebase**: Luôn kiểm tra code và giải quyết xung đột cẩn thận để tránh lỗi.
- **Sử dụng stash hợp lý**: Sử dụng `stash` khi cần tạm thời lưu trữ thay đổi để chuyển branch hoặc làm việc khác.
- **Sử dụng branch hợp lý**: Tạo branch riêng cho từng tính năng hoặc lỗi để dễ quản lý.
