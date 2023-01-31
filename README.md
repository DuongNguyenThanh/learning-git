# learning-git

## Git
Git là một hệ thống quản lý phiên bản phân tán.

## Git Config
```
git config --global user.name 'Duong'
git config --global user.email 'duong@gmail.com'
```

## Repository
Repository (kho chứa) là nơi sẽ ghi lại trạng thái của thư mục và file. Trạng thái được lưu lại đang được chứa như là lịch sử thay đổi của nội dung. Một người khác có thể sao chép (clone) lại mã nguồn đó nhằm làm việc.

Repository có hai loại là Local Repository (Kho chứa trên máy cá nhân) và Remote Repository (Kho chứa trên một máy chủ từ xa).

## Git status
```
git status
```
Cho biết được trạng thái của các file trong thư mục

## Staging Area
Staging Area nghĩa là một khu vực mà nó sẽ được chuẩn bị cho quá trình commit. Trước hết, ta cần phải hiểu rằng trong các hệ thống quản lý phiên bản (Version Control System) thì các dữ liệu sẽ được lưu trữ ở hai nơi, một là thư mục ta đang làm việc trên máy tính (working tree) và một là kho chứa mã nguồn (repository) sau khi ta đã thực hiện thay đổi (ví dụ như kho chứa trên Github).

Nhưng với Git thì nó có thêm một lựa chọn nữa đó là có thêm một khu vực trung gian gọi là Staging Area và đây chính là một lợi thế lớn của Git. Staging Area nghĩa là khu vực sẽ lưu trữ những thay đổi của ta trên tập tin để nó có thể được commit, vì muốn commit tập tin nào thì tập tin đó phải nằm trong Staging Area. Một tập tin khi nằm trong Staging Area sẽ có trạng thái là Stagged.

<img src="images/staging_area.png">

Và để đưa một tập tin vào Staging Area thì ta sẽ cần phải sử dụng lệnh git add tên_file.

## Git log
```
git log
```
Xem lại các commit mà chúng ta đã tạo.

## Commit là gì và nó hoạt động ra sao?
Hiểu đơn giản hơn, commit nghĩa là một hành động để Git lưu lại một bản chụp (snapshot) của các sự thay đổi trong thư mục làm việc, và các tập tin và thư mục được thay đổi đã phải nằm trong Staging Area. Mỗi lần commit nó sẽ được lưu lại lịch sử chỉnh sửa của mã nguồn kèm theo tên và địa chỉ email của người commit. Ngoài ra trong Git bạn cũng có thể khôi phục lại tập tin trong lịch sử commit của nó để chia cho một phân nhánh (branch) khác, đây là mấu chốt của việc bạn sẽ dễ dàng khôi phục lại các thay đổi trước đó.

Lệnh commit trong Git sẽ là: 
```
git commit -m “Lời nhắn”
```

Và nếu bạn muốn đưa tập tin lên repository thì bạn phải commit nó trước rồi sau đó lệnh ```git push origin master``` sẽ có nhiệm vụ đưa toàn bộ các tập tin đã được commit lên repository.

## Điều kiện gì để commit một tập tin?
Nếu bạn muốn commit một tập tin đó, bạn sẽ cần phải đưa tập tin đó vào trạng thái tracked bằng lệnh git add tên_file. Trong git có hai loại trạng thái chính đó là Tracked và Untracked, cụ thể:

`Tracked` – Là tập tin đã được đánh dấu theo dõi trong Git để bạn làm việc với nó. Và trạng thái Tracked nó sẽ có thêm các trạng thái phụ khác là: 
- Unmodified (chưa chỉnh sửa gì).
- Modified (đã chỉnh sửa).
- Staged (đã sẵn sàng để commit). 

`Untracked` – Là tập tin còn lại mà bạn sẽ không muốn làm việc với nó trong Git.

Nhưng bạn phải nên biết rằng nếu tập tin đó đã được Tracked nhưng đang rơi vào trạng thái (Modified) thì nó vẫn sẽ không thể commit được mà bạn phải đưa nó về Staged cũng bằng lệnh git add.

## Conventional Commits
### Chuẩn cấu trúc conventional commits
```
# [] là phần tùy chọn, có thể có hoặc không, <> là phần bắt buộc 
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

`type`:
- **fix**: pull request này thực hiện fix bug của dự án.
- **feat(feature)**: pull request này thực hiện một chức năng mới của dự án.
- **refactor**: pull request này thực hiện refactor lại code hiện tại của dự án (refactor hiểu đơn giản là việc "làm sạch" code, loại bỏ code smells, mà không làm thay đổi chức năng hiện có).
- **docs**: pull request này thực hiện thêm/sửa đổi document của dự án.
- **style**: pull request này thực hiện thay đổi UI của dự án mà không ảnh hưởng đến logic.
- **perf**: pull request này thực hiện cải thiện hiệu năng của dự án (VD: loại bỏ duplicate query, ...).
- **vendor**: pull request này thực hiện cập nhật phiên bản cho các packages, dependencies mà dự án đang sử dụng.
- **chore**: pull request này để chỉ những thay đổi không đáng kể trong code (thay đổi lặt vặt - ví dụ như thay đổi text).

`scope`:
- **KHÔNG BẮT BUỘC**
- Thay đổi code trong pull request này sẽ có phạm vi ảnh hưởng đến đâu (là danh từ)
- Đứng ngay sau `<type>` và được đặt trong dấu ngoặc đơn.

```
# scope ở đây là lang (language)
feat(lang): add polish language
```
(ví dụ nếu thực hiện sửa đổi phần xác thực người dùng thì scope là (authentication) )

`description`: mô tả khá quát, ngắn gọn về những thay đổi được thực hiện trong pull request.

```
# mô tả ngắn gọn pull request này sửa lỗi chính tả trong CHANGELOG
docs: correct spelling of CHANGELOG
```

`body`:
- **KHÔNG BẮT BUỘC**
- NẾU CÓ, bắt buộc phải cách phần `description` 1 dòng trắng (blank line)
- Mô tả chi tiết bổ sung cho phần description phía trên về những thay đổi được thực hiện trong pull request.
- Không giới hạn về số dòng và không nhất thiết phải theo 1 format nhất định (free-form).

`footer(s)`:
- KHÔNG BẮT BUỘC
- Nằm ở phía sau body (nếu có body) và phân cách bằng một dòng trắng (blank line)
- Chứa các thông tin mở rộng của pull request ví dụ như là danh sách người review, link/id của các pull request có liên quan.
- Nếu có nhiều footer thì mỗi footer phải chứa một word token là :<space> hoặc <space>#
- Để phân biệt với phần body thì các từ ghép dùng làm token (ngoại trừ BREAKING CHANGE) sẽ ngăn cách nhau bằng dấu - thay vì <space> (Reviewed by => Reviewed-by)

```
# 1 commit message gồm body(gồm nhiều đoạn) và nhiều footer 
fix: correct minor typos in code #type: description

see the issue for details #body paragraph 1

on typos fixed. #body paragraph 2

Reviewed-by: Z #footer 1 sử dụng :<space>
Refs #133 #footer 2 sử dụng <space>#
```

`BREAKING CHANGE` (quan trọng nên cần viết IN HOA và **bôi đậm**):
- Nếu sự thay đổi code trong pull request của bạn làm thay đổi lớn khiến cho nó không còn tương thích với phiên bản trước nữa thì bạn sẽ phải đánh dấu pull request này là BREAKING CHANGE.
- Có 2 cách để đánh dấu 1 pull request là BREAKING CHANGE: đó là đặt từ khóa BREAKING CHANGE: vào đầu footer hoặc là ! liền sau type/scope hoặc sử dụng cả 2.

```
# sử dụng từ khóa `BREAKING CHANGE`
feat: allow provided config object to extend other configs
<blank line>
BREAKING CHANGE:<space>`extends` key in config file is now used for extending other config files

# sử dụng ! liền sau type trong commit
refactor!: drop support for Node 6

# sử dụng kết hợp cả 2 
refactor!: drop support for Node 6
<blank line>
BREAKING CHANGE:<space>refactor to use JavaScript features not available in Node 6.
```