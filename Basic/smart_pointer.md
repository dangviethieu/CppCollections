* Smart Pointer là 1 class template, được định nghĩa để xử lý các vấn đề liên quan đến xử lý bộ nhớ tự động.
* Cần thiết khi gặp vấn đề: *1 tài nguyên được sử dụng bởi nhiều đối tượng, ở nhiều nơi trong chương trình thì thực hiện huỷ tài nguyên ở đâu?*
* xác định đối tượng có quyền gì đối với tài nguyên: ***quyền sở hữu, quyền sử dụng, quyền thu hồi***
* có 3 loại smart pointer:
	* **unique_pointer: quyền sở hữu duy nhất**, tài nguyên mà nó quản lý chỉ có thể được sở hữu bởi duy nhất 1 đối tượng.
	* **shared_pointer: quyền sở hữu chia sẻ**, tài nguyên mà nó quản lý có thể được sở hữu bởi nhiều đối tượng.
	* **weak_pointer: quyền sở hữu yếu**, đối tượng nắm trong tay weak_pointer trỏ tới 1 tài nguyên chỉ có quyền sử dụng tài nguyên đó, ko có quyền huỷ
	### 1. unique_pointer
	* giới hạn phạm vi của tai nguyên, quản lý dễ dàng hơn, performance tốt hơn
	* ko thể thực hiện gán thông thường (bằng copy constructor, hoặc copy assignment) -> dùng move constructor, move assignment.
	* chi phí sử dựng tương đương vs pointer thông thường
	```
	std::unique_pointer<Test> test = std::make_unique<Test>();
	std::unique_pointer<Test> test = std::unique_pointer<Test>(new Test());
	std::unique_pointer<Test> test_another = std::move(test);
	```
	### 2. shared_pointer
	* sử dụng cơ chế **reference counting** để đảm bảo khi ko còn shared pointer nào trỏ tới tài nguyên đó nữa thì tài nguyên sẽ bị thu hồi, và sử dụng biến **atomic** để đảm bảo **thread-safe** khi tài nguyên được sử dụng ở nhiều thread khác nhau.
	```
	std::shared_pointer<Test> test = std::make_shared<Test>();
	std::shared_pointer<Test> test_(test);
	std::shared_pointer<Test> test__ = test;
	```
	### 3. weak_pointer
	* cơ chế **reference counting** chỉ dựa vào số lượng shared_ptr đang trỏ tới tài nguyên, chứ không quan tâm tới tài nguyên đó đang được trỏ tới bởi bao nhiêu weak_ptr, dù đang có 5 weak_ptr đang trỏ tới tài nguyên đó, nhưng không còn shared_ptr nào trỏ tới nữa thì tài nguyên đó vẫn bị thu hồi.
