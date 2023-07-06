# CLass and Object
- Class là đơn vị đóng gói cơ bản của C++, cung cấp cơ chế tạo đối tượng
- Class là một mô tả trừu tượng của một nhóm các đối tượng có cùng bản chất
- Mỗi đối tượng là một thể hiện cụ thể cho những mô tả trừu tượng đó
- Class gồm 2 thành phần chính:
  - **Thành phần dữ liệu (data member)**: hay còn gọi là **thuộc tính (attribute)**
  - **Hàm thành phần (member function)**: hay còn gọi là **phương thức (method)**
# Khai báo và định nghĩa một Lớp đối tượng mới
```cpp
class HocSinh{
private:
  int mssv;  //attribute
  string hoten;  //attribute
  double diemToan;  //attribute
  double diemVan;  //attribute
  double diemTB; //attribute
  void xuLy();  //method
public:
  void nhap();  // methoa
  void xuat();  // method
};
```
Khai bao

Vd: HocSinh hs1, hs2, hs3;
# Member function - Method
## Khái niệm:  
- Là các khả năng, hành động mà một đối tượng thuộc về lớp có thể thực hiện
## Method Calling
- Để gọi một phương thức, ta có thể sử dụng **toán tử chấm (dot operator)** trên một đối tượng của lớp hoặc **toán tử mũi tên (arrow operator)** lên một con trỏ giữ địa chỉ của đối tượng thuộc lớp đó
```cpp
HocSinh hs;
hs.nhap();
HocSinh* pHs = &hs;
pHs->nhap();
```
## Định nghĩa phương thức
- Việc định nghĩa các phương thức có thể được thực hiện bên trong hoặc bên ngoài Class
- Khi định nghĩa phương thức ở ngoài lớp, ta sử dụng **toán tử phạm vi (scope operator - dấu ::)**
```cpp
void HocSinh::nhap(){
  // Thân phương thức
}
```
## Giới thiệu về con trỏ this
- Con trỏ hằng (const pointer) là con trỏ mà địa chỉ ns đang giữ không thể bị thay đổi
```cpp
HocSinh* const p = &hs;
```
- Con trỏ **this** là một con trỏ hằng được chương trình **tự định nghĩa** bên trong một phương thức, nó sẽ giữ và chỉ có thể giữ **địa chỉ của đối tượng đang gọi thực hiện phương thức đó**. Vì thế con trỏ **this** luôn có kiểu trùng với kiểu của Class mà nó trỏ tới
```cpp
hs.nhap(); // đối tượng học sinh gọi thực hiện phương thức nhập
```


