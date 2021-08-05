**Kế thừa (inheritance) là một tính chất đặc trưng của lập trình hướng đối tượng. Nó có nghĩa là một class thừa hưởng lại tất cả các thuộc tính, phương thức của class mà nó kế thừa.**

## Các loại kế thừa
* Kế thừa đơn (single inheritance): là một class con kế thừa duy nhất từ một class cha.
* Kế thừa đa cấp (multilevel inheritance): là một class con kế thừa từ một class cha, class cha đó lại kết thừa từ một lớp khác.
* Kế thừa phân cấp (hierarchical inheritance): là khi có nhiều hơn một class con kế thừa từ class cha.

## Cú pháp
```
class <tên_class_con> : <phạm_vi_truy_cập> <tên_class_cha>
{
    // code goes here
};
```