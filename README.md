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
# **LESSON 3: POINTER**  
**A. Pointer**  
con trỏ là một biến chứa địa chỉ bộ nhớ của một biến khác. Việc sử dụng con trỏ giúp chúng ta thực hiện các thao tác trên bộ nhớ một cách linh hoạt hơn.  
khai báo  
```
int *ptr;  // a pointer to int type  
char *ptr_char;  // a pointer to char type  
float *ptr_float;  // a pointer to float type
```     
ví dụ  
```
int x = 5;
int *ptr_x = &x;  // ptr_x now contains address of x
int y = *ptr_x;  // y equals to the value of x
Kích thước của con trỏ phụ thuộc vào kiến ​​trúc máy tính và trình biên dịch.
int main() 
{
    int *ptr;
    printf("Size of pointer: %d bytes\n", sizeof(ptr));
    return 0;
}
```   
**B. Void Pointer**   
Con trỏ void thường được sử dụng để trỏ tới bất kỳ địa chỉ nào mà không cần biết kiểu dữ liệu của giá trị tại địa chỉ đó.
khai báo  
```
void *ptr_void;
```  
ví dụ  
```  
#include <stdio.h>
int main() {
    int num = 10;
    float f_num = 3.14;
    char ch = 'A';

    // Declare a void pointer
    void *ptr;

    // Assign the address of variable num to the void pointer
    ptr = &num;
    printf("Value of num: %d\n", *(int*)ptr);

    // Assign the address of variable f_num to the void pointer
    ptr = &f_num;
    printf("Value of f_num: %.2f\n", *(float*)ptr);

    // Assign the address of variable ch to the void pointer
    ptr = &ch;
    printf("Value of ch: %c\n", *(char*)ptr);

    return 0;
}
```
**C. Function Pointer**  
Con trỏ hàm là một biến mà chứa địa chỉ của một hàm. Nó trỏ tới vùng bộ nhớ chứa mã máy của hàm được định nghĩa trong chương trình.  
khai báo  
``` 
<return_type> (*<name_of_pointer>)( <data_type_of_parameters> );
``` 
ví dụ  
```  
#include <stdio.h>
// Define two functions
int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int main() {
    // Declare a function pointer variable
    int (*operation)(int, int);

    // Assign the address of the add function to the function pointer
    operation = &add;
    printf("Result of addition: %d\n", operation(5, 3)); // This will call add(5, 3)

    // Assign the address of the subtract function to the function pointer
    operation = &subtract;
    printf("Result of subtraction: %d\n", operation(5, 3)); // This will call subtract(5, 3)

    return 0;
}
```  
**D. Pointer to Constant**  
Con trỏ tới hằng số (pointer to constant) là một loại con trỏ trong ngôn ngữ lập trình C/C++ mà chỉ cho phép trỏ đến một hằng số và không thể thay đổi giá trị của hằng số đó thông qua con trỏ. Điều này có nghĩa là con trỏ chỉ có thể trỏ đến địa chỉ của một hằng số, nhưng không thể sửa đổi giá trị của hằng số đó thông qua con trỏ.  
Trong trường hợp này, khi con trỏ được khai báo là một con trỏ tới hằng số, bạn không thể sử dụng con trỏ đó để thay đổi giá trị của hằng số mà nó trỏ đến, tuy nhiên, giá trị của hằng số đó vẫn có thể thay đổi thông qua các phương thức khác.  
khai báo  
```  
int const *ptr_const; 
const int *ptr_const;
```  
ví dụ  
```  
#include <stdio.h>
int main() {
    // Define a constant variable
    const int num = 10;

    // Declare a pointer to a constant integer
    const int *ptr;

    // Assign the address of the constant variable to the pointer
    ptr = &num;

    // Try to change the value through the pointer (This will result in a compilation error)
    // *ptr = 20; // This line will cause a compilation error

    // Print the value of the constant variable using the pointer
    printf("Value of num: %d\n", *ptr);

    return 0;
}
```  
**E. Constant Pointer**  
Một con trỏ hằng (constant pointer) là một con trỏ trong ngôn ngữ lập trình C/C++ mà không thể thay đổi địa chỉ mà nó trỏ đến sau khi đã được khởi tạo. Điều này có nghĩa là một khi con trỏ đã được gán một địa chỉ cụ thể, thì không thể thay đổi địa chỉ đó để trỏ đến một vùng nhớ khác.  
khai báo  
```  
int *const const_ptr = &value;
```  
ví dụ  
```  
#include <stdio.h>

int main() {
    int num1 = 10, num2 = 20;
    int *const ptr = &num1;  // Constant pointer to integer

    printf("Value of num1: %d\n", *ptr); // Output: 10

    // Attempt to change the address pointed by the constant pointer
    // ptr = &num2; // This line will result in a compilation error

    // Change the value at the address pointed by the constant pointer
    *ptr = 30;
    printf("Value of num1 after modification: %d\n", *ptr); // Output: 30

    return 0;
}
```  
**F. Pointer to Pointer**  
Con trỏ tới con trỏ là một loại dữ liệu trong ngôn ngữ lập trình cho phép bạn lưu trữ địa chỉ của một con trỏ. Con trỏ tới con trỏ cung cấp một cấp độ trỏ mới, cho phép bạn thay đổi giá trị của con trỏ gốc. Cấp độ này có thể hữu ích trong nhiều tình huống, đặc biệt là khi bạn làm việc với các hàm cần thay đổi giá trị của con trỏ.  
ví dụ  
```  
#include <stdio.h>

int main() {
    int num = 10;
    int *ptr1 = &num;  // Pointer to integer
    int **ptr2 = &ptr1;  // Pointer to pointer

    printf("Value of num: %d\n", **ptr2); // Output: 10

    // Change the value of num through pointer to pointer
    **ptr2 = 20;
    printf("Value of num after modification: %d\n", **ptr2); // Output: 20

    return 0;
}
```  
**G. NULL Pointer**  
Một con trỏ null là một con trỏ không trỏ tới bất kỳ đối tượng hoặc khu vực bộ nhớ cụ thể nào. Trong ngôn ngữ lập trình C, một con trỏ có thể được gán giá trị NULL để biểu diễn trạng thái null.  
Việc sử dụng một con trỏ null thường hữu ích để kiểm tra xem một con trỏ đã được khởi tạo và trỏ tới một khu vực bộ nhớ hợp lệ hay không. Tránh việc giải tham chiếu (sử dụng giá trị mà con trỏ trỏ tới) một con trỏ null là quan trọng để tránh lỗi trong chương trình.  
ví dụ  
```  
#include <stdio.h>

int main() {
    int *ptr = NULL; // Initialize a pointer to NULL

    // Attempt to dereference the null pointer (This will result in a segmentation fault)
    // int value = *ptr; // Uncommenting this line will result in a segmentation fault

    // Check if the pointer is null before dereferencing
    if (ptr != NULL) {
        int value = *ptr;
        printf("Value: %d\n", value);
    } else {
        printf("Pointer is null, cannot dereference.\n");
    }

    return 0;
}
```
# **LESSON 4: MEMORY LAYOUT**  
**A. Introduction and Concept**  
Bộ nhớ chương trình được chia thành 5 phần chính: (thứ tự từ địa chỉ thấp đến địa chỉ cao):  
-Text: Khu vực mã và hằng số. Khu vực nhớ Text được quản lý bởi hệ điều hành, các đơn vị khác không thể can thiệp trực tiếp vào phân vùng này (chỉ đọc).  
-BSS: Khu vực phân bổ cục bộ, bao gồm các biến: được khai báo dưới dạng tĩnh, biến toàn cục nhưng không có giá trị khởi tạo.  
-Data: Tương tự như khu vực BSS, nhưng được sử dụng để lưu trữ các biến có giá trị khởi tạo ban đầu.  
-HEAP: Khu vực cấp phát động. Được sử dụng để cấp phát bộ nhớ thông qua các kỹ thuật cấp phát bộ nhớ động (ví dụ: sử dụng các hàm malloc, calloc trong C hoặc sử dụng new trong C++).  
-STACK: Khu vực ngăn xếp. (chứa các đối tượng cục bộ).  
Lưu ý: các khu vực BSS và Data trong khu vực TEXT có kích thước cố định trong quá trình hoạt động của chương trình. Các khu vực HEAP và STACK có kích thước biến đổi, có thể mở rộng trong quá trình hoạt động của chương trình.  
![image](https://github.com/vinh1802/ADVANCED-C/assets/168539077/640a0387-3db7-4b87-9a81-3f77f142a6eb)  

# **LESSON 7: BITMASKING**  
**A. Introduction**  
Bitmasking là một kỹ thuật trong lập trình máy tính, liên quan đến việc thực hiện các phép toán bitwise trên các bit của các số nguyên. Kỹ thuật này thường được sử dụng để kiểm tra, thiết lập hoặc xóa các bit cụ thể trong một số nguyên, đồng thời giữ nguyên các bit khác.  
Một bitmask là một chuỗi các bit, trong đó mỗi bit đại diện cho một trạng thái hoặc một cờ. Bằng cách sử dụng bitmask, chúng ta có thể áp dụng các phép toán bitwise để kiểm tra hoặc thiết lập các bit cụ thể trong một số nguyên mà không ảnh hưởng đến các bit khác. Điều này thường được sử dụng để thao tác với các cờ, hoặc kiểm tra và thiết lập các thuộc tính hoặc tùy chọn trong các biến nguyên.  
6 toán tử bitwise trong C  
& (Bitwise AND Operator)  
| (Bitwise OR Operator)  
^ (Bitwise XOR Operator)  
~ (Bitwise NOT Operator)  
<< (Left Shift Operator)  
(Right Shift Operator) >>     
**B. Bitmask Techniques**  
**1.Đảo ngược một bit bằng phép NOT bitwise**  
Sử dụng để thực hiện phép NOT bitwise trên mỗi bit của một số. Kết quả là số ngược của số đó.  
cú pháp
```
number = ~ number
```  
ví dụ  
```  
#include <stdio.h> 
int main() 
{ 

    int x = 1; 

    printf("Ans: %d", ~x); 

    return 0; 
}
```  
Output  
```  
Ans: -2
```  
**2.Set bit**  
Chúng ta lấy số nguyên 1 và sử dụng toán tử dịch trái, dịch biểu diễn nhị phân của 1 đi n vị trí, trong đó (n+1) là vị trí của bit mà chúng ta muốn thiết lập. Sau đó, sử dụng toán tử OR bitwise, chúng ta biến bit thứ (n+1) của số đã cho thành 1.  
cú pháp  
```  
number | (1 << bit_position_to_set)
```  
ví dụ  
```  
#include <stdio.h> 
int main() 
{ 

    int x = 13; 

    printf("Ans: %d", 13 | (1 << 5)); 

    return 0; 
}
```  
output  
```  
Ans: 45
```  
**3.Xoá bit**  
Chúng ta lại lấy số nguyên 1 và dịch nó đến vị trí đã chỉ định. Sau đó, chúng ta thực hiện phép NOT trên điều này để chuyển đổi nó thành 0 và các bit khác của giá trị (1 << n) thành 1. Sau đó, chúng ta thực hiện phép AND để xóa bit đã chỉ định và thu được kết quả.  
cú pháp  
```  
number & ~(1 << bit_position_to_clear)
```  
ví dụ  
```  
#include<stdio.h> 
int main() 
{ 
    int x = 13; 
    
    printf("Ans: %d", 13 & ~(1 << 2) ); 
    
    return 0; 
}
```  
output  
```  
Ans: 9
```  
**4.Lật bit**  
Lật một bit cụ thể, nghĩa là nếu bit đó là 0 thì chuyển nó thành 1 và ngược lại. Hoạt động này yêu cầu sử dụng toán tử XOR bitwise (^) cùng với toán tử dịch trái (<<).  
cú pháp  
```  
number ^ (1 << bit_position_to_flip)
```  
ví dụ  
```  
#include<stdio.h>

int main() 
{ 
    int x = 13; 
    
    printf("Ans: %d", 13 ^ (1 << 3) ); 
    
    return 0; 
}
```  
output  
```  
Ans: 5
```  



