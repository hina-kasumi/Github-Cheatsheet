# Hướng Dẫn Sử Dụng Gitflow Trong Dự Án

Gitflow là một chiến lược quản lý branch trong Git, được thiết kế để tổ chức quy trình phát triển phần mềm một cách hiệu quả, đặc biệt phù hợp với các dự án có chu kỳ phát hành phiên bản rõ ràng. Gitflow định nghĩa các loại branch cụ thể với mục đích riêng, giúp đội nhóm phát triển dễ dàng quản lý code, tính năng, sửa lỗi, và các bản phát hành.

## 1. Gitflow Là Gì?

Gitflow là một mô hình quản lý branch được Vincent Driessen giới thiệu vào năm 2010. Nó sử dụng các branch chính và phụ để quản lý vòng đời phát triển phần mềm, từ phát triển tính năng, sửa lỗi, đến phát hành và bảo trì. Gitflow đặc biệt hữu ích trong các dự án có nhiều nhà phát triển và yêu cầu phát hành phiên bản định kỳ.

## 2. Các Loại Branch Trong Gitflow

Gitflow sử dụng các loại branch sau, mỗi loại có vai trò và quy tắc riêng:

### 2.1. Branch Chính (Main Branches)
- **`main`**: Lưu trữ lịch sử chính thức của dự án, chỉ chứa code đã sẵn sàng cho production. Mỗi commit trên `main` thường đại diện cho một phiên bản phát hành.
- **`develop`**: Chứa code mới nhất đã được tích hợp từ các tính năng hoặc sửa lỗi, nhưng chưa sẵn sàng cho production. Đây là branch tích hợp chính cho các nhà phát triển.

### 2.2. Branch Hỗ Trợ (Supporting Branches)
- **`feature`**: Dùng để phát triển các tính năng mới. Branch này được tạo từ `develop` và sau khi hoàn thành sẽ được hợp nhất (merge) trở lại `develop`. Tên thường bắt đầu bằng `feature/` (ví dụ: `feature/login-system`).
- **`release`**: Chuẩn bị cho một bản phát hành mới. Branch này được tạo từ `develop` để sửa lỗi nhỏ, cập nhật tài liệu, hoặc điều chỉnh phiên bản. Sau khi hoàn tất, nó được merge vào cả `main` và `develop`. Tên thường bắt đầu bằng `release/` (ví dụ: `release/v1.0.0`).
- **`hotfix`**: Xử lý các lỗi khẩn cấp trên production. Branch này được tạo từ `main`, sửa lỗi xong sẽ merge vào cả `main` và `develop`. Tên thường bắt đầu bằng `hotfix/` (ví dụ: `hotfix/fix-login-bug`).
- **`bugfix`**: Dùng để sửa lỗi không khẩn cấp, thường được tạo từ `develop` và merge lại `develop`. Tên thường bắt đầu bằng `bugfix/` (ví dụ:bugfix/ui-alignment`).

## 3. Quy Trình Làm Việc Với Gitflow

Dưới đây là quy trình chi tiết khi sử dụng Gitflow, kèm theo các câu lệnh Git tương ứng cùng comment giải thích:

### 3.1. Khởi Tạo Repository Với Gitflow
1. Khởi tạo repository và tạo các branch chính:
   ```bash
   git init  # Khởi tạo một repository Git mới trong thư mục hiện tại
   git branch develop  # Tạo branch develop để lưu trữ code đang phát triển
   git push origin main  # Đẩy branch main lên remote repository
   git push origin develop  # Đẩy branch develop lên remote repository
   ```

### 3.2. Phát triển Tính Năng Mới (Feature)
1. Tạo branch `feature` từ `develop`:
   ```bash
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote branch develop
   git checkout -b feature/<tên-tính-năng>  # Tạo và chuyển sang branch feature mới
   ```
2. Làm việc, commit thay đổi:
   ```bash
   git add .  # Thêm tất cả các file thay đổi vào staging area
   git commit -m "Thêm tính năng <mô tả>"  # Tạo commit với thông điệp mô tả rõ ràng
   ```
3. Hoàn thành, merge lại `develop`:
   ```bash
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote để tránh xung đột
   git merge --no-ff feature/<tên-tính năng>  # Merge branch feature vào develop, giữ lịch sử commit riêng
   git push origin develop  # Đẩy code đã merge lên remote branch develop
   ```
4. Xóa branch `feature`:
   ```bash
   git branch -d feature/<tên-tính năng>  # Xóa branch feature cục bộ sau khi merge
   ```

### 3.3. Chuẩn bị phát hành Bán Hành (Release)
1. Tạo branch `release` từ `develop`:
   ```bash
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote
   git checkout -b release/<phiên bản>  # Tạo và chuyển sang branch release mới
   ```
2. Sửa lỗi nhỏ, cập nhật version, commit:
   ```bash
   git add .  # Thêm các thay đổi (ví dụ: sửa lỗi, cập nhật changelog) vào staging area
   git commit -m "Cập nhật phiên bản <phiên bản>"  # Tạo commit với mô tả rõ ràng
   ```
3. Merge vào `main` và `develop`:
   ```bash
   git checkout main  # Chuyển sang branch main
   git pull origin main  # Cập nhật code mới nhất từ remote main
   git merge --no-ff release/<phiên-bản>  # Merge branch release vào main, giữ lịch sử commit riêng
   git tag v<phiên-bản>  # Tạo tag để đánh dấu phiên bản phát hành
   git push origin main  # Đẩy branch main lên remote repository
   git push origin v<phiên-bản>  # Đẩy tag phiên bản lên remote repository
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote develop
   git merge --no-ff release/<phiên bản>  # Merge branch release vào develop để đồng bộ
   git push origin develop  # Đẩy code đã merge lên remote branch develop
   ```
4. Xóa branch `release`:
   ```bash
   git branch -d release/<tag-name>  # Xóa branch release cục bộ sau khi merge
   ```

### 3.4. Sửa Lỗi Khẩn Cấp (Hotfix)
1. Tạo branch `hotfix` từ `main`:
   ```bash
   git checkout main  # Chuyển sang branch main
   git pull origin main  # Cập nhật code mới nhất từ remote main
   git checkout -b hotfix/<mô-tả-lỗi>  # Tạo và chuyển sang branch hotfix mới
   ```
2. Sửa lỗi, commit:
   ```bash
   git add .  # Thêm các thay đổi sửa lỗi vào staging area
   git commit -m "Sửa lỗi <mô-tả>"  # Tạo commit với mô tả rõ ràng
   ```
3. Merge vào `main` và `develop`:
   ```bash
   git checkout main  # Chuyển sang branch main
   git pull origin main  # Cập nhật code mới nhất từ remote main
   git merge --no-ff hotfix/<mô-tả-lỗi>  # Merge branch hotfix vào main, giữ lịch sử commit riêng
   git tag v<phiên-bản-hotfix>  # Tạo tag để đánh dấu phiên bản hotfix
   git push origin main  # Đẩy branch main lên remote repository
   git push origin v<phiên-bản-hotfix>  # Đẩy tag hotfix lên remote repository
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote develop
   git merge --no-ff hotfix/<mô-tả-lỗi>  # Merge branch hotfix vào develop để đồng bộ
   git push origin develop  # Đẩy code đã merge lên remote branch develop
   ```
4. Xóa branch `hotfix`:
   ```bash
   git branch -d hotfix/<mô-tả-lỗi>  # Xóa branch hotfix cục bộ sau khi merge
   ```

### 3.5. Sửa Lỗi Không Khẩn Cấp (Bugfix)
1. Tạo branch `bugfix` từ `develop`:
   ```bash
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote develop
   git checkout -b bugfix/<mô-tả-lỗi>  # Tạo và chuyển sang branch bugfix mới
   ```
2. Sửa lỗi, commit:
   ```bash
   git add .  # Thêm các thay đổi sửa lỗi vào staging area
   git commit -m "Sửa lỗi <mô-tả>"  # Tạo commit với mô tả rõ ràng
   ```
3. Merge lại `develop`:
   ```bash
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote develop
   git merge --no-ff bugfix/<mô-tả-lỗi>  # Merge branch bugfix vào develop, giữ lịch sử commit riêng
   git push origin develop  # Đẩy code đã merge lên remote branch develop
   ```
4. Xóa branch `bugfix`:
   ```bash
   git branch -d bugfix/<mô-tả-lỗi>  # Xóa branch bugfix cục bộ sau khi merge
   ```

## 4. Sử Dụng Các Lệnh Git Nâng Cao Trong Gitflow
- **`git rebase`**:
   ```bash
   git checkout feature/<tên-tính-năng>  # Chuyển sang branch feature cần rebase
   git rebase -i <commit-id>  # Mở rebase tương tác để chỉnh sửa, gộp, hoặc xóa commit
   ```
- **`git stash`**:
   ```bash
   git stash  # Lưu tạm các thay đổi chưa commit vào stash
   git checkout develop  # Chuyển sang branch develop
   git pull origin develop  # Cập nhật code mới nhất từ remote develop
   git checkout feature/<tên-tính-năng>  # Quay lại branch feature
   git stash pop  # Khôi phục các thay đổi từ stash
   ```
- **`git restore`**:
   ```bash
   git restore <file>  # Khôi phục file về trạng thái của commit gần nhất
   ```
- **`git cherry-pick`**:
   ```bash
   git cherry-pick <commit-id>  # Áp dụng một commit cụ thể từ branch khác vào branch hiện tại
   ```

## 5. Ưu Điểm và Nhược Điểm Của Gitflow

### Ưu Điểm
- **Tổ chức rõ ràng**: Phân chia branch theo mục đích giúp quản lý dự án dễ dàng hơn.
- **Hỗ trợ phát hành phiên bản**: Phù hợp với các dự án có chu kỳ phát hành định kỳ.
- **Hỗ trợ làm việc nhóm**: Nhiều nhà phát triển có thể làm việc song song trên các tính năng khác nhau.

### Nhược Điểm
- **Phức tạp**: Nhiều branch và quy trình có thể gây khó khăn cho các dự án nhỏ hoặc đội nhóm mới.
- **Xung đột merge**: Branch `develop` có thể gặp xung đột nếu tích hợp quá nhiều thay đổi.
- **Không phù hợp với CI/CD**: Gitflow có thể chậm trong môi trường tích hợp và triển khai liên tục.

## 6. Lưu Ý Khi Sử Dụng Gitflow
- **Đặt tên branch nhất quán**: Sử dụng tiền tố (`feature/`, `release/`, `hotfix/`, `bugfix/`) để dễ nhận diện.
- **Kéo code thường xuyên**: Sử dụng `git pull` trên `main` và `develop` để tránh xung đột.
- **Kiểm tra kỹ trước khi merge**: Đảm bảo test đầy đủ trên branch `release` hoặc `hotfix` trước khi merge vào `main`.
- **Sử dụng công cụ hỗ trợ**: Các công cụ như GitLab, GitHub, hoặc SourceTree có thể hỗ trợ trực quan hóa quy trình Gitflow.
- **Backup thường xuyên**: Đẩy code lên remote trước khi thực hiện các thao tác phức tạp như merge hoặc rebase.

## 7. Kết Luận

Gitflow là một chiến lược mạnh mẽ để quản lý các dự án phần mềm phức tạp, đặc biệt trong môi trường doanh nghiệp. Tuy nhiên, đội nhóm cần thống nhất cách sử dụng và hiểu rõ quy trình để đảm bảo hiệu quả. Nếu dự án nhỏ hoặc áp dụng CI/CD, bạn có thể xem xét các mô hình đơn giản hơn như **GitHub Flow**.

File này có thể được sử dụng như tài liệu tham khảo để triển khai Gitflow trong dự án của bạn.