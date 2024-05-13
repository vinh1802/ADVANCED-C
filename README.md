# **LESSON 1: COMPILER AND MACRO**
**A. COMPILER**  
Làm thế nào để tạo một chương trình cho máy tính?  
-Bước 1: Viết mã nguồn (.c) và tệp tiêu đề (.h).  
-Bước 2: Tiền xử lý mã nguồn theo các chỉ thị tiền xử lý. Các chỉ thị tiền xử lý bắt đầu bằng dấu thăng (#), như #include và #define. Chúng chỉ ra rằng một số thao tác (như bao gồm một tệp khác hoặc thay thế các ký hiệu) sẽ được thực hiện TRƯỚC khi biên dịch.  
-Bước 3: Biên dịch mã nguồn đã được tiền xử lý thành mã đối tượng (.obj, .o).  
-Bước 4: Liên kết mã đối tượng đã biên dịch với các mã đối tượng khác và các mã thư viện (.lib, .a) để tạo ra mã thực thi (.exe).  
-Bước 5: Tải mã thực thi vào bộ nhớ máy tính.  
-Bước 6: Chạy mã thực thi.  
![image](https://github.com/vinh1802/ADVANCED-C/assets/168539077/2880ac29-e544-4598-906d-165c19d306c9)

**B. MACRO**  
MACRO là một từ được sử dụng để chỉ thông tin được xử lý trong trình tiền xử lý. Chia thành 3 nhóm chính:  
-Tệp tiêu đề hoặc Thư viện: #include  
-Thay thế macro_name bằng macro_value trước khi biên dịch thành tệp .bin: #define, #undef  
-Chỉ thị biên dịch có điều kiện: #if, #elif, #else, #ifdef, #ifndef  

Ví dụ 1:  
#if condition_1  
TODO 1;  
#elif condition_1  
TODO 2;  
#else  
TODO 3;  
#endif  
=>giải thích: Nếu "điều_kiện_1" là đúng, thì LÀM_1 được xây dựng. Nếu điều_kiện_2 là đúng, thì LÀM_2 được chọn để xây dựng. Nếu cả điều_kiện_1 và 2 đều sai, thì LÀM_3 được chọn để xây dựng.  

Ví dụ 2:
#ifdef macro  
TODO 1;  
#else  
TODO 2;  
#endif  
=>giải thích: Nếu macro đã được xác định trước bằng #define macro, thì LÀM_1 được chọn để xây dựng. Nếu không được xác định, LÀM_2 được chọn để xây dựng.

Ví dụ 3:
#ifndef macro  
TODO 1;  
#else  
TODO 2;  
#endif  
=>giải thích: Ngược lại so với #ifdef. Nếu macro chưa được xác định, thì LÀM_1 được chọn để xây dựng. Nếu đã được xác định, thì LÀM_2 được chọn để xây dựng.  

# **LESSON 2: STDARG AND ASSERT**  
**A. STDARG**  
Stdarg.h trong ngôn ngữ lập trình C cho phép các hàm chấp nhận một số lượng biến số không cố định. Nó cung cấp các macro và một loại (va_list) để truy cập và điều chỉnh các đối số này.  
Các Tính Năng Chính của stdarg.h  
-va_list: Một loại dữ liệu đại diện cho một danh sách các đối số.  
-va_start(ap, last_named_arg): Khởi tạo một đối tượng va_list để trỏ tới đối số không có tên đầu tiên sau last_named_arg.  
-va_arg(ap, type): Lấy đối số tiếp theo từ va_list và chuyển đổi nó thành kiểu đã chỉ định.  
-va_end(ap): Dọn dẹp đối tượng va_list.  
**B. ASSERT**  
-Các lệnh assert được sử dụng trong các chương trình nếu nhà phát triển muốn khẳng định hoặc đưa ra giả định.  
-Nó lấy một biểu thức làm tham số trong hàm. Biểu thức được đánh giá.  
-Nếu giá trị trả về sau khi đánh giá biểu thức là 0 hoặc FALSE, nó trả về biểu thức cùng với tên tệp và dòng thực thi như một lỗi.  
-Nếu có lỗi xảy ra, chương trình gọi hàm abort(). Hàm assert không làm gì nếu biểu thức được đánh giá là TRUE.  
