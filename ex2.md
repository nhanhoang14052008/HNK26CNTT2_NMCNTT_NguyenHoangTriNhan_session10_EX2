## Phần 1. Phân tích lỗi

Bảng Excel quản lý thiết bị IoT đang vi phạm ít nhất 4 quy tắc vàng trong tư duy Database:

1.  Không gộp ô (Merge Cell): Ô tiêu đề bị gộp khiến Excel khó xác định cấu trúc cột và vùng dữ liệu cần lọc.
    
2.  Không để hàng trống trong vùng dữ liệu: Hàng trống khiến AutoFilter có thể chỉ nhận diện một phần bảng.
    
3.  Dữ liệu phải thống nhất: Cột Trạng thái có giá trị `hỏng` và `hỏng` (thừa dấu cách), khiến Excel hiểu là hai giá trị khác nhau.
    
4.  Mỗi cột chỉ chứa một loại thông tin: Cột phải có tiêu đề rõ ràng và dữ liệu cùng loại, không trộn nhiều thông tin trong một ô.
    

## Phần 2. Hoàn thiện bảng dữ liệu

### Bước 1. Gỡ Merge Cell

-   Chọn vùng tiêu đề đang gộp ô.
    
-   Vào Home → Merge & Center → Unmerge Cells.
    
-   Đảm bảo mỗi cột có một tiêu đề riêng, không để trống tiêu đề.
    

### Bước 2. Làm sạch cột Trạng thái bằng TRIM()

Giả sử cột Trạng thái nằm ở cột D, dữ liệu bắt đầu từ ô D2.

1.  Tạo một cột phụ, đặt tên `Trạng thái sạch`.
    
2.  Tại ô E2, nhập công thức:
    

`=TRIM(D2)`

3.  Nhấn Enter, kéo công thức xuống hết các dòng dữ liệu.
    
4.  Sao chép cột kết quả, chọn cột D và dùng Paste Special → Values để thay thế dữ liệu cũ.
    
5.  Xóa cột phụ nếu không còn cần thiết.
    

Lưu ý: TRIM loại bỏ khoảng trắng thừa thông thường. Nếu dữ liệu chứa khoảng trắng đặc biệt như dấu cách không ngắt dòng (CHAR(160)), có thể dùng:

`=TRIM(SUBSTITUTE(D2,CHAR(160)," "))`

### Bước 3. Xóa hàng trống

-   Chọn vùng dữ liệu.
    
-   Vào Home → Find & Select → Go To Special → Blanks.
    
-   Kiểm tra các ô trống được chọn; xóa các hàng trống hoàn toàn bằng Delete Sheet Rows.
    
-   Không xóa những ô trống hợp lệ trong các hàng vẫn có dữ liệu.
    

### Bước 4. Bật AutoFilter

1.  Chọn một ô trong vùng dữ liệu liên tục.
    
2.  Nhấn Ctrl + Shift + L để bật Filter.
    
3.  Mở bộ lọc tại cột Trạng thái.
    
4.  Chọn giá trị `hỏng` để lọc các thiết bị bị hỏng.
    

Nếu đã làm sạch dữ liệu đúng cách, các giá trị chỉ khác nhau do khoảng trắng sẽ được chuẩn hóa và không còn xuất hiện thành hai nhóm riêng biệt.
