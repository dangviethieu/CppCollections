**Tính đóng gói (Encapsulation) chỉ đơn giản là việc kết hợp một bộ các dữ liệu (data) liên quan đến nhau cùng với một bộ các hàm/phương thức (functions/methods) hoạt động trên các dữ liệu đó, “gói” tất cả vào trong một cái gọi là class.  Các thực thể của các class thì được gọi là các đối tượng (objects) trong khi class giống như một công thức được sử dụng để tạo ra các đối tượng đó.**

![Encapsulation](https://cppdeveloper.com/wp-content/uploads/2019/01/encapsulation_.png)

```
class Rectangle {
private:
    int mWidth;
    int mHeight;
public:
    void setValues(int w, int h);
    int getArea(void);
};

void Rectangle::setValues(int w, int h) {
    mWidth = w;
    mHeight = h;
}

int Rectangle::getArea() {
    return mWidth*mHeight;
}
```
Tính đóng gói thể hiện ở đoạn code trên là việc kết hợp các dữ liệu về hình chữ nhật gồm có chiều rộng, chiều dài cùng với các hàm xử lý (đọc/ghi/tính toán) với các dữ liệu này vào một class có tên là Rectangle. Chỉ đơn giản vậy thôi.


## Che dấu dữ liệu  (Data Hiding):
là việc một số dữ liệu (data) và hàm/phương thức (functions/methods) được class che giấu đi (ở dạng private) để đảm bảo rằng các dữ liệu đó sẽ được truy cập và sử dụng đúng mục đích, đúng cách thông qua các hàm/phương thức (functions/methods) ở dạng public mà class cung cấp. Bạn không thể truy cập đến các private data hoặc gọi đến private methods của class từ bên ngoài class đó.

Che dấu dữ liệu – Data Hiding chỉ là một phương pháp kỹ thuật mà bạn áp dụng để xây dựng nên class mà thôi, nó không phải là tính chất đặc trưng của lập trình hướng đối tượng, việc bạn có áp dụng phương pháp này hay không là hoàn toàn không bắt buộc. Tuy nhiên trong các hệ thống thật, để nâng cao tính security, giảm phụ thuộc giữa các class, tránh lỗi do đọc ghi dữ liệu sai cách, …  thì việc áp dụng phương pháp che dấu dữ liệu gần như là đương nhiên.
