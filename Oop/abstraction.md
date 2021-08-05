**Tính trừu tượng (Abstraction) là một trong 4 tính chất đặc trưng quan trọng của các ngôn ngữ lập trình hướng đối tượng (OOP – object-oriented programming). Mục tiêu chính của nó là làm giảm sự phức tạp bằng cách ẩn các chi tiết không liên quan trực tiếp tới người dùng (người dùng ở đây không phải người dùng cuối mà là lập trình viên). Điều đó cho phép người dùng vẫn thực hiện được các công việc cần thiết dựa trên một thực thể trừu tượng được cung cấp mà không cần hiểu hoặc thậm chí không nghĩ về tất cả sự phức tạp ẩn giấu bên trong.**

Trong OOP thì Abstraction có thể chia thành 2 level (2 cảnh giới)
## Cảnh giới thứ nhất
Dữ liệu (data) và một số hàm (methods) không cần thiết đưa ra bên ngoài sẽ được đưa vào trong class và chỉ định đặc tả truy cập là private (hoặc protected). Các data hoặc methods đó sẽ không thể truy cập từ bên ngoài của class đó. Ở cảnh giới này trừu tượng giúp cho code dễ hiểu hơn vì nó tập trung vào các tính năng / hành động cốt lõi và không tập trung vào các chi tiết nhỏ nhặt. Ngoài ra nó còn giúp chương trình dễ bảo trì, hạn chế lỗi do truy cập data bừa bãi, sai cách. Ở level này có thể coi Abstraction = Encapsulation + Data Hiding.

## Cảnh giới thứ hai
Ở cảnh giới này chúng ta thực hiện trừu tượng hoá từ giai đoạn design cho đến coding. Ở giai đoạn design – thiết kế chúng ta sẽ tập trung vào việc đưa ra “what” – cái mà một module hoặc 1 class sẽ làm chứ không tập trung vào “how” – các việc đó được thực hiện như thế nào. Kết quả của bước thiết kế này sẽ là một cái gọi là interface. Các class (hoặc module) sẽ làm việc với nhau thông qua interface chứ không cần biết cụ thể về nhau.

    Một interface là một bản mô tả hành vi hoặc khả năng của một class mà không đưa ra cách thực hiện cụ thể của class đó như thế nào.
Trong C++ thì interface là một class mà chỉ chứa khai báo của hàm huỷ ảo (virtual destructor) và các hàm thuần ảo (poor virtual methods) khác. Ở giai đoạn coding thì các interface sẽ được xây dựng cụ thể bằng các class cụ thể khác, các class này bắt buộc phải kết thừa interface class và định nghĩa cụ thể các hàm thuần ảo đã được khai báo trong interface đó. Bằng cách này thì các module (hoặc class) sẽ không phụ thuộc vào nhau mà chỉ phụ thuộc vào interface, việc sửa code của các module (hoặc class) sẽ không kéo theo việc phải sửa code ở các module (hoặc class) khác.
```
class IShape  // class này đóng vai trò là interface vì tất cả các hàm của nó đều là hàm thuần ảo
{
public:
    virtual ~IShape();
    virtual void move_x(int x) = 0;
    virtual void move_y(int y) = 0;
    virtual void draw() = 0;
};
 
class Line : public IShape
{
public:
    virtual ~Line();
    virtual void move_x(int x); // class Line sẽ phải có code cụ thể của hàm move_x
    virtual void move_y(int y); // class Line sẽ phải có code cụ thể của hàm move_y
    virtual void draw(); // class Line sẽ phải có code cụ thể của hàm draw
private:
    point end_point_1, end_point_2;
//...
};
 
int main (void)
{
    IShape* shape = new Line();
    // Gọi một số hàm setup cho shape
    //...
    // Vẽ shape
    shape->move_x(10);
    shape->move_y(20);
    shape->draw();
    //...
}
```
Trong ví dụ trên thì IShape được gọi là interface còn Line là class implement cụ thể interface đó. IShape chỉ đưa ra danh sách các hàm mà một class kế thừa nó cần phải định nghĩa, bản thân class IShape không định nghĩa các hàm đó. Line 28~30 trong hàm main thực hiện vẽ đối tượng trỏ bởi con trỏ shape mà không quan tâm đến đối tượng cụ thể trong đó là đối tượng của class nào, nó chỉ làm việc đó thông qua interface IShape mà không cần biết đến sự tồn tại của Line.