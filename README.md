# CppCollections
## 1. Sự khác nhau giữa C và C++?  
Ngôn ngữ C++ có tất cả những gì mà ngôn ngữ C có.  
Về cơ bản, có 1 số sự khác nhau chính:
* C là ngôn ngữ lập trình hướng thủ tục, C++ là ngôn ngữ lập trình hướng đối tượng.
* C chỉ hỗ trợ con trỏ, C++ hỗ trợ cả con trỏ và tham chiếu.
* C không có nạp chông toán hàm (function overloading), C++ có hỗ trợ. 
So sánh sự khác trên các khía cạnh:  

| Khía cạnh  | C | C++ |
| ------------- | ------------- | ------------- |
| Kiểu ngôn ngữ	  | Ngôn ngữ lập trình hướng thủ tục	  | Ngôn ngữ lập trình hướng đối tượng |
| Cách tiếp cận	  | C tiếp cận theo hướng top-down (tập trung vào việc chia nhỏ một vấn đề lớn thành các phần nhỏ hơn)	  | C++ tiếp cận theo hướng bottom-up (trước tiên tập trung vào giải quyết các vấn đề nhỏ hơn ở cấp độ cơ bản và sau đó tích hợp chúng thành một giải pháp toàn diện và hoàn chỉnh) |   
| Cách tổ chức chương trình	| C chia chương trình lớn được thành các phần nhỏ và được gọi là các hàm (function)	| C++ lại chia các chương trình lớn thành các lớp (Class) và đối tượng (Object)
| inline function	| Không hỗ trợ	| Có hỗ trợ
| Con trỏ	| C chỉ hỗ trợ tham trị & con trỏ	| C++ hỗ trợ cả tham trị, tham chiếu và con trỏ
Nạp chồng hàm	| Không hỗ trợ	| Có hỗ trợ
Quản lý ngoại lệ	 | Không có. Tuy nhiên vẫn có một số giải pháp	 | Có hỗ trợ, bạn có thể sử dụng try catch để bắt lỗi
Hàm | Không cho phép giá trị mặc định của tham số.	| Cho phép giá trị mặc định của tham số
Namespace	| Không có	| Có
Quan hệ	| C không thể chạy code C++	| C++ có thể chạy code C
Quản lý bộ nhớ	| C có malloc() và calloc() cho cấp phát động	| C++ có toán tử new cho cấp phát động
Hàm ảo	| Không tồn tại trong C	| Có trong C++
Lập trình giao diện	| Sử dụng công cụ GTK	| Có Qt hỗ trợ lập trình GUI

## 2. Memory Allocation
C++ hỗ trợ 3 loại cấp phát bộ nhớ:  
### 2.1 Cấp phát bộ nhớ tĩnh (Static memory allocation)  
* dùng cho **biến static, biến global**
* vùng nhớ được **cấp phát 1 lần** khi ctrinh bắt đầu chạy và **tồn tại trong suốt thời gian tồn tại của ctrinh**
* kích thước của biến/mảng phải được khai báo tại thời điểm biên dịch ctrinh
### 2.2 Cấp phát bộ nhớ tự động (Automactic memory allocation)
* dùng cho các **tham số hàm, biến local**
* vùng nhớ dc cấp phát khi ctrinh đi vào khối lệnh và dc giải phóng khi khối lệnh bị thoát
* kích thước của biến/mảng phải được khai báo tại thời điểm biên dịch ctrinh  

**Nhược điểm của 2 loại trên:**  
* Gây **lãng phí bộ nhớ** nếu các biến không thực sự sử dụng hết kích thước khi khai báo.
* Hầu hết các biến thông thường (bao gồm mảng tĩnh) được cấp phát trong một phần bộ nhớ gọi là **ngăn xếp (stack)**. Kích thước bộ nhớ stack cho một chương trình khá nhỏ (khoảng 1Mb với Visual Studio), nếu yêu cầu cấp phát vùng nhớ vượt quá con số này, chương trình sẽ bị đóng bởi hệ điều hành với lỗi stack overflow.
* Chương trình sẽ bị giới hạn bởi kích thước được khai báo ban đầu.
### 2.3 Cấp phát bộ nhớ động (Dynamically memory allocation)  
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
## 3. Smart Pointer
* Smart Pointer là 1 class template, được định nghĩa để xử lý các vấn đề liên quan đến xử lý bộ nhớ tự động.
* Cần thiết khi gặp vấn đề: *1 tài nguyên được sử dụng bởi nhiều đối tượng, ở nhiều nơi trong chương trình thì thực hiện huỷ tài nguyên ở đâu?*
* xác định đối tượng có quyền gì đối với tài nguyên: ***quyền sở hữu, quyền sử dụng, quyền thu hồi***
* có 3 loại smart pointer:
	* **unique_pointer: quyền sở hữu duy nhất**, tài nguyên mà nó quản lý chỉ có thể được sở hữu bởi duy nhất 1 đối tượng.
	* **shared_pointer: quyền sở hữu chia sẻ**, tài nguyên mà nó quản lý có thể được sở hữu bởi nhiều đối tượng.
	* **weak_pointer: quyền sở hữu yếu**, đối tượng nắm trong tay weak_pointer trỏ tới 1 tài nguyên chỉ có quyền sử dụng tài nguyên đó, ko có quyền huỷ
	### 3.1. unique_pointer
	* giới hạn phạm vi của tai nguyên, quản lý dễ dàng hơn, performance tốt hơn
	* ko thể thực hiện gán thông thường (bằng copy constructor, hoặc copy assignment) -> dùng move constructor, move assignment.
	* chi phí sử dựng tương đương vs pointer thông thường
	```
	std::unique_pointer<Test> test = std::make_unique<Test>();
	std::unique_pointer<Test> test = std::unique_pointer<Test>(new Test());
	std::unique_pointer<Test> test_another = std::move(test);
	```
	### 3.2. shared_pointer
	* sử dụng cơ chế **reference counting** để đảm bảo khi ko còn shared pointer nào trỏ tới tài nguyên đó nữa thì tài nguyên sẽ bị thu hồi, và sử dụng biến **atomic** để đảm bảo **thread-safe** khi tài nguyên được sử dụng ở nhiều thread khác nhau.
	```
	std::shared_pointer<Test> test = std::make_shared<Test>();
	std::shared_pointer<Test> test_(test);
	std::shared_pointer<Test> test__ = test;
	```
	### 3.3. weak_pointer
	* cơ chế **reference counting** chỉ dựa vào số lượng shared_ptr đang trỏ tới tài nguyên, chứ không quan tâm tới tài nguyên đó đang được trỏ tới bởi bao nhiêu weak_ptr, dù đang có 5 weak_ptr đang trỏ tới tài nguyên đó, nhưng không còn shared_ptr nào trỏ tới nữa thì tài nguyên đó vẫn bị thu hồi.










