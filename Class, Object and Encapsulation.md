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
- Khi dòng lệnh trên được thực hiện, chương trình sẽ tự động gán địa chỉ của đối tượng hs vào
biến con trỏ this (được định nghĩa ngầm bên trong phương thức Nhap). Sau đó, ta có thể
dùng con trỏ này để truy cập đến các thuộc tính của đối tượng hs, cũng như dùng nó để gọi
các phương thức khác, ví dụ
```cpp
void HocSinh::nhap(){
  cin>>this->mssv;
  this->xuLy();
}
```
- Tuy nhiên để cho gọn, chương trình cho phép ta truy cập trực tiếp đến các thành viên của
đối tượng đang gọi thực hiện phương thức. Bất kì tên của thành viên nào được ghi ra mà
không nói gì thêm thì thành viên đó sẽ xem như là được truy cập thông qua con trỏ this.
# Trừu tượng hóa dữ liệu (Data abstraction) và đóng gói (Encapsulation)
- Một trong những ý tưởng cơ bản đằng sau việc xây dựng và thiết kế một Lớp đối tượng
chính là Trừu tượng hóa dữ liệu (Data abstraction) và Đóng gói (Encapsulation).
- Trừu tượng hóa dữ liệu là một kỹ thuật lập trình và thiết kế dựa trên sự tách biệt của Giao
diện (Interface) và Thực thi (Implementation). Giao diện của một Lớp đối tượng là các
hoạt động mà người dùng của một Lớp có thể thao tác trên các đối tượng của Lớp đó. Phần
Thực thi bao gồm các dữ liệu thành viên (thuộc tính), phần định nghĩa của các phương thức.
- Đóng gói chính là quá trình ẩn đi phần Thực thi khỏi người dùng bên ngoài và giới hạn
quyền truy cập vào nó. Người dùng của một Lớp chỉ có thể sử dụng Giao diện mà không có
quyền truy cập vào phần Thực thi.
- Một Lớp đối tượng được áp dụng đặc tính Trừu tượng hóa dữ liệu và Đóng gói sẽ tạo
thành một kiểu dữ liệu trừu tượng mô phỏng lại một khái niệm bên ngoài thế giới thực.
Những lập trình viên sử dụng Lớp chỉ cần biết một cách trừu tượng rằng đối tượng của Lớp
có thể thực hiện các hoạt động gì mà không cần hiểu cách thức thực hiện bên trong.
# Phạm vi truy xuất (access specifiers)
- Trong C++, chúng ta thực hiện việc đóng gói bằng cách chỉ định phạm vi truy xuất
  - Những thành phần được khai báo sau từ khóa **public** có thể được truy cập ở **tất cả
các phần của chương trình**. Các thành phần **public** tạo nên giao diện của một Lớp.
  - Những thành phần được khai báo sau từ khóa **private** chỉ có thể được truy cập **bên
trong phạm vi của lớp**, bởi các hàm thành viên (phương thức) của một lớp và không
thể được truy cập từ bên ngoài lớp. Phần **private** ẩn đi (đóng gói) phần thực thi.
- Ngoài ra còn phạm vi truy xuất nữa là **protected**

**Lưu ý: Sự khác biệt giữa từ khóa struct và class:**
- Trong một lớp có thể không có hoặc có nhiều nhãn **private** và **public**, mỗi nhãn này
có phạm vi ảnh hưởng cho đến khi gặp một nhãn kế tiếp hoặc hết khai báo lớp.
Nếu khai báo một Lớp sử dụng từ khóa **struct**, những thành phần được khai báo trước
nhãn truy cập đầu tiên sẽ được mặc định là **public**, nếu sử dụng từ khóa **class**, những
thành phần đó sẽ mặc định là **private**:

**Lưu ý: Các lợi ích khi áp dụng đặc tính Đóng gói:**
- Giúp **bảo vệ dữ liệu** bên trong tránh khỏi các sai sót không đáng có từ người dùng (như
ví dụ về phương thức cập nhật ở trên).
- Giúp **thay đổi phần thực thi** của lớp một cách **linh hoạt** (tức là thay đổi cách tổ chức dữ
liệu, chi tiết thực hiện các phương thức). Miễn là phần giao diện không bị thay đổi thì
những đoạn code sử dụng lớp sẽ không bị ảnh hưởng, do đó không làm đổ vỡ kiến trúc
hệ thống.
# Phương thức thiết lập (Constructor)
## Mục tiêu:
- Các phương thức thiết lập của một lớp đối tượng có nhiệm vụ thiết lập thông tin ban
đầu cho các đối tượng thuộc về lớp sau khi đối tượng được khai báo.
## Đặc điểm
- Phương thức thiết lập là một hàm thành viên đặc biệt có tên trùng với tên lớp.
- Không có giá trị trả về.
- Được tự động gọi thực hiện ngay khi đối tượng được khai báo.
- Có thể có nhiều phương thức thiết lập trong 1 lớp.
- Trong một quá trình sống của đối tượng thì chỉ có 1 lần duy nhất một phương thức
thiết lập được gọi thực hiện mà thôi đó là khi đối tượng ra đời.
## Phân loại phương thức thiết lập
- Phương thức thiết lập mặc định (default constructor).
- Phương thức thiết lập nhận tham số đầu vào (parameterized constructor).
- Phương thức thiết lập sao chép (copy constructor).
### Phương thức thiết lập mặc định (default constructor).
**Lưu ý**
- Nếu chúng ta có định nghĩa các phương thức thiết lập khác thì chương trình sẽ không
tự định nghĩa phương thức thiết lập mặc định cho chúng ta, do đó ta phải tự định nghĩa
một phiên bản của riêng mình
- Phương thức thiết lập mặc định còn được chương trình tự gọi khi ta khai báo một mảng
các đối tượng của một lớp như các cách sau:
```cpp
HocSinh arr[5];
HocSinh* arr = new HocSinh[5];
```
### Phương thức thiết lập nhận tham số đầu vào (parameterized constructor).


