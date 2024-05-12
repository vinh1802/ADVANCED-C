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

Ví dụ mã:  
```
#include <stdio.h>      
typedef enum
{
    GPIOA,
    GPIOB,
    GPIOC
} Ports;

typedef enum{
    PIN1,
    PIN2,
    PIN3,
    PIN4,
    PIN5,
    PIN6,
    PIN7,
} Pins;

typedef enum
{
    HIGH,
    LOW
} Status;

#define STM32 0
#define ATMEGA 
#define PIC 2

#define MCU STM32

#if MCU == STM32
void daoTrangThaiDen(Ports port, Pins pin, Status status)
{
    if (status == HIGH)
    {
        HAL_GPIO_WritePin(port, pin, LOW);
    }
    else
    {
        HAL_GPIO_WritePin(port, pin, HIGH);
    }  
}

#elif MCU == ATMEGA 
void daoTrangThaiDen(Pins pin, Status status)
{
    if (status == HIGH)
    {
        digitalWrite(pin, LOW);
    }
    else
    {
        digitalWrite(pin, HIGH);
    }  
}

#endif
void delay(int ms){}

int main()
{
    while(1)
    {
        daoTrangThaiDen(GPIOA,13,HIGH);
        delay(1000);
    }

return 0;
} 
```

