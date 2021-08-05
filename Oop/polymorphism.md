**Đa hình (polymorphism) là hiện tượng mà các đối tượng thuộc các class khác nhau có thể biểu diễn cùng một thông thiệp theo các cách khác nhau.**

![Screenshot](../imgs/polymorhism.png)

Các loại đa hình
* Compile time Polymorphism: 
    * cách mà đối tượng thực hiện thông điệp được xác định ngay lúc biên dịch chương trình
    * **overriding** (phương thức ở class cơ sở bị override ở class dẫn xuất, điều đó làm cho tuy cùng một phương thức nhưng đối tượng thuộc class cơ sở sẽ thực hiện khác đối tượng thuộc class dẫn xuất)
    * **overloading** (cùng là một hàm nhưng với các đối tượng là các tham số khác nhau thì hành động thực hiện cũng sẽ khác nhau)
* Runtime Polymorphism
    * cách mà đối tượng thực hiện thông điệp không được xác định lúc biên dịch mà nó chỉ được xác định khi chương trình được thực thi

## Phương thức ảo
Phương thức ảo (virtual method) trong C++ là cách thể hiện tính đa hình trong lập trình hướng đối tượng của C++, các phương thức ở class cơ sở có tính đa hình phải được định nghĩa là một phương thức ảo.
```
class <ClassName>
{
protected:
    virtual <returnType> <methodName>([<params>]) {}
};
```
tính đa hình được thể hiện thông qua tham chiếu và con trỏ
```
NhanVienVanPhong nvvp;  
NhanVien &nv = nv; // biến nv tham chiếu đến biến nvvp  
nv.nhap(); // Phương thức được gọi là sẽ phương thức nhập của class NhanVienVanPhong
```
Do để tham chiếu đến một biến, bắt buộc biến kia phải tồn tại trước, do đó cách tham chiếu rất ít khi được sử dụng mà thay vào đó, người ta sẽ dùng con trỏ.

```
NhanVien *nv = new NhanVienVanPhong; // con trỏ nv trỏ tới biến động kiểu NhanVienVanPhong
nv->nhap(); // Phương thức được gọi là sẽ phương thức nhập của class NhanVienVanPhong
```

## Phương thức thuần ảo
Phương thức thuần ảo (pure virtual method) là phương thức ảo không có phần định nghĩa và bắt buộc phải được override ở class dẫn xuất  
```
class <ClassName>
{
public:
    virtual <returnType> <methodName>([<params>]) = 0;
};
```
Ví dụ: đối với class nhân viên thì phương thức tính lương không có bởi vì ta không thể tính lương cho một nhân viên mà không biết là nhân viên gì. Các class dẫn xuất của nó là một cụ thể hóa của class cơ sở nhân viên, nên ta có thể tính lương được, ta biết cách tính cho từng loại nhân viên như thế nào.

## Lớp trừu tượng
Lớp trừu tượng (abstract class) là một class chứa phương thức thuần ảo, không thể tạo một đối tượng thuộc lớp trừu tượng. Điều này hiển nhiên, bởi vì nếu class chứa một hoặc nhiều phương thức ảo, khi đối tượng được tạo thì phương thức đó sẽ không có định nghĩa và sẽ gây lỗi.

## Interface
Interface có thể được hiểu là một class trừu tượng hoàn toàn, nghĩa là mọi phương thức của interface đều là phương thức thuần ảo và bạn sẽ cần phải override lại tất cả các phương thức của interface ở class dẫn xuất.

    Một interface là một bản mô tả hành vi hoặc khả năng của một class mà không đưa ra cách thực hiện cụ thể của class đó như thế nào.
