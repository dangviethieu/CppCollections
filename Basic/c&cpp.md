## Sự khác nhau giữa C và C++?  
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