# Phần 1: Phân tích lỗ hổng

### 1. Xác định dòng log gây rò rỉ dữ liệu

-   Dòng 1: File `campuspay_beta_users.xlsx` cấp quyền Editor + Anyone with the link. Đây là nguyên nhân trực tiếp gây rò rỉ vì bất kỳ ai có link đều có thể xem, sửa và chia sẻ tiếp dữ liệu sinh viên.
    
-   Dòng 2: File `campuspay_api_keys.txt` cấp quyền Viewer + Restricted. Cấu hình này tương đối an toàn vì chỉ người được cấp quyền mới truy cập được.
    
-   Dòng 3: File `slide_pitch_v8.pptx` cấp quyền Commenter + Anyone with the link. Người có link vẫn xem được nội dung nên có nguy cơ lộ thông tin.
    
-   Dòng 4: File `campuspay_beta_users.xlsx` cấp quyền Editor + Restricted cho Email C. Cấu hình này phù hợp nếu Email C cần chỉnh sửa file.
    
-   Dòng 5: Email người lạ truy cập file API keys là dấu hiệu bất thường, cần kiểm tra thêm để xác định nguyên nhân.
    

### 2. Ba giả thuyết người lạ truy cập file API keys

-   Giả thuyết 1: File từng được chia sẻ công khai trước khi chuyển sang Restricted.
    
-   Giả thuyết 2: Người lạ được cấp quyền trực tiếp hoặc thông qua một nhóm có quyền truy cập.
    
-   Giả thuyết 3: Tài khoản của người được cấp quyền bị lộ hoặc bị người khác sử dụng.
    

# Phần 2: Sửa lỗi và nghiệm thu

### 3. Bảng cấu hình quyền chia sẻ đúng chuẩn

 Câu 3: Bảng phân quyền đúng

| Tên file | Quyền phù hợp | Phạm vi |
|---|---|---|
| `campuspay_beta_users.xlsx` | Editor | Restricted |
| `campuspay_api_keys.txt` | Viewer | Restricted |
| `slide_pitch_v8.pptx` | Commenter | Restricted |

Giải thích: Các file chứa dữ liệu quan trọng không nên để chế độ Anyone with the link. Chỉ cấp quyền cho những người thực sự cần sử dụng.

### 4. Thu hồi link cũ và sử dụng Set Expiration Date

-   Vào Google Drive, chọn file → Share → đổi quyền truy cập chung thành Restricted.
    
-   Xóa những người không còn cần quyền truy cập để hạn chế việc tiếp tục xem file.
    
-   Sử dụng Set Expiration Date để tự động hết hạn quyền của cộng tác viên tạm thời, ví dụ sau khi kết thúc đợt thử nghiệm Beta.
