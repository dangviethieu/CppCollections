C++ hỗ trợ 3 loại cấp phát bộ nhớ:  
### 1 Cấp phát bộ nhớ tĩnh (Static memory allocation)  
* dùng cho **biến static, biến global**
* vùng nhớ được **cấp phát 1 lần** khi ctrinh bắt đầu chạy và **tồn tại trong suốt thời gian tồn tại của ctrinh**
* kích thước của biến/mảng phải được khai báo tại thời điểm biên dịch ctrinh
### 2 Cấp phát bộ nhớ tự động (Automactic memory allocation)
* dùng cho các **tham số hàm, biến local**
* vùng nhớ dc cấp phát khi ctrinh đi vào khối lệnh và dc giải phóng khi khối lệnh bị thoát
* kích thước của biến/mảng phải được khai báo tại thời điểm biên dịch ctrinh  

**Nhược điểm của 2 loại trên:**  
* Gây **lãng phí bộ nhớ** nếu các biến không thực sự sử dụng hết kích thước khi khai báo.
* Hầu hết các biến thông thường (bao gồm mảng tĩnh) được cấp phát trong một phần bộ nhớ gọi là **ngăn xếp (stack)**. Kích thước bộ nhớ stack cho một chương trình khá nhỏ (khoảng 1Mb với Visual Studio), nếu yêu cầu cấp phát vùng nhớ vượt quá con số này, chương trình sẽ bị đóng bởi hệ điều hành với lỗi stack overflow.
* Chương trình sẽ bị giới hạn bởi kích thước được khai báo ban đầu.
### 3 Cấp phát bộ nhớ động (Dynamically memory allocation)  
Sử dụng toán tử **new**:  
>// cấp phát động một số nguyên và gán địa chỉ cho con trỏ ptr nắm giữ  
int *ptr = new int;  
*ptr = 10; // gán 10 cho vùng nhớ vừa được cấp phát  
// Khi cấp phát động cho một biến, bạn có thể cùng lúc khởi tạo giá trị cho nó:  
int *ptr1 = new int(10);  
int *ptr2 = new int{ 20 };  

Khi chúng ta không còn sử dụng một biến được cấp phát động, chúng ta cần trao quyền quản lý vùng nhớ đó lại cho hệ điều hành. Đối với các biến đơn (không phải mảng), điều này được thực hiện thông qua toán tử **delete**:  
>int *ptr = new int;  
delete ptr; // trả lại vùng nhớ ptr đang trỏ đến cho hệ điều hành  
ptr = nullptr; // gán ptr thành con trỏ null  

*Toán tử **delete không thực sự xóa bất cứ điều gì**. Nó chỉ đơn giản là trao lại quyền sử dụng vùng nhớ được cấp phát cho hệ điều hành. Sau đó, hệ điều hành được tự do gán lại vùng nhớ đó cho một ứng dụng khác (hoặc ứng dụng này).*

### Con trỏ lơ lửng (Dangling pointers)
Thông thường, khi delete một con trỏ, vùng nhớ được trả lại cho hệ điều hành sẽ chứa cùng giá trị mà nó có trước đó. Lúc này, con trỏ đang trỏ sang một vùng nhớ chưa được cấp phát (hệ điều hành quản lý).  
Con trỏ trỏ đến vùng nhớ chưa được cấp phát gọi là một con trỏ lơ lửng (Dangling pointers). Truy cập vào vùng nhớ (dereferencing pointer) hoặc xóa một con trỏ lơ lửng sẽ dẫn đến lỗi undefined behavior.
```
#include <iostream>  
using namespace std;  
int main()  
{  
	// cấp phát động một số nguyên và gán địa chỉ cho con trỏ ptr nắm giữ  
	int *ptr = new int;  
	*ptr = 10; // gán 10 vào vùng nhớ được cấp phát  
	// giải phóng vùng nhớ cho hệ điều hành, ptr đang là con trỏ lơ lửng  
	delete ptr;  
	// truy cập vùng nhớ ptr đang trỏ tới => lỗi undefined behavior  
	cout << *ptr;  
    // giải phóng vùng nhớ con trỏ đã được giải phóng trước đó => lỗi undefined behavior  
    delete ptr;   
	return 0;  
}
```
### Rò rỉ bộ nhớ trong C++ (Memory leaks)
*Ví dụ 1:*
```
void doSomething()
{
	int *ptr = new int;
}
```
Trong hàm doSomething() cấp phát động một số nguyên, nhưng không sử dụng toán tử delete để giải phóng vùng nhớ đó. Vì con trỏ tuân theo tất cả các quy tắc giống như các biến thông thường, khi hàm kết thúc, ptr sẽ bị hủy. Mặt khác, ptr là biến duy nhất giữ địa chỉ của số nguyên được cấp phát động. Nghĩa là chương trình đã "mất" địa chỉ của bộ nhớ được cấp phát động trong hàm doSomething(). Kết quả là chương trình không thể giải phóng vùng nhớ được cấp phát động.  
Vấn đề trên được gọi là rò rỉ bộ nhớ (memory leaks). Rò rỉ bộ nhớ xảy ra khi chương mất địa chỉ của một số vùng nhớ được cấp phát động trước khi giải phóng nó cho hệ điều hành.  
Khi rò rỉ bộ nhớ, chương trình của bạn không thể xóa bộ nhớ được cấp phát động, bởi vì chương trình không còn nắm giữ địa chỉ vùng nhớ đó. Hệ điều hành cũng không thể sử dụng vùng nhớ này, vì vùng nhớ đó vẫn nằm trong quyền sử dụng của chương trình.

Một số trường hợp khác có thể gây rò rỉ bộ nhớ trong C++:  
*Ví dụ 2:* Con trỏ giữ địa chỉ của bộ nhớ được cấp phát động được gán một giá trị khác gây rò rỉ bộ nhớ.
```
int value = 10;
int *ptr = new int; // cấp phát vùng nhớ
ptr = &value; // địa chỉ vùng nhớ cấp phát trước đó bị mất, rò rỉ bộ nhớ
```
Ví dụ 3: Cấp phát vùng nhớ liên tục nhiều lần
```
int *ptr = new int;
ptr = new int; // địa chỉ vùng nhớ cấp phát trước đó bị mất, rò rỉ bộ nhớ
```
Để khắc phục vấn đề rò rỉ bộ nhớ (memory leaks) trong C++, chúng ta cần giải phóng vùng nhớ khi ra khỏi phạm vi con trỏ (ví dụ 1), hoặc trước khi gán (ví dụ 2), cấp phát một con trỏ (ví dụ 3).