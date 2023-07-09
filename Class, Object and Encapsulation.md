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
Là các phương thức thiết lập sử dụng các đối số được truyền vào nó để khởi tạo dữ liệu cho các thuộc tính của đối tượng.
```cpp
HocSinh (int id, string name, int toan, int van)
{
  mssv = id;
  hoTen = name;
  diemToan = toan;
  diemVan = van;
  XuLy ();
}
```
Để gọi phương thức thiết lập vừa định nghĩa ở trên, ta sẽ khai báo đối tượng hs như sau:
```cpp
  HocSinh hs(22120123, "Minh Hung", 9, 8);
```
Ta có thể định nghĩa nhiều phương thức thiết lập khác miễn là chúng có danh sách tham số đầu vào khác nhau
```cpp
HocSinh (int id, string name)
{
  mssv = id;
  hoTen = name;
  diemToan = 0;
  diemVan = 0
  XuLy ();
}
```
### Phương thức thiết lập sao chép (copy constructor)
**Nhắc lại kiến thức**
- Tham chiếu trong C++:
  - Tham chiếu là một **cái tên khác** cho đối tượng
  - Tham chiếu được khai báo bằng cách thêm kí tự '&' vào trước tên biến
    - Ví dụ:
        ```cpp
        HocSinh &r = hs;
        ```
    -  Khi khái báo một tham chiếu r như trên, chương trình sẽ **không sao chép** giá trị của **hs** vào **r** mà chỉ xem r như một **cái tên khác** của đối tượng hs.
  - Tham chiếu hằng: một tham chiếu mà không thể dùng để thay đổi giá trị của đối tượng mà nó gắn vào
    - Ví dụ:
      ```cpp
      const HocSinh &r = hs;
      ```
  - Một tham chiếu bình thường không thể được gắn với một biến hằng, một tham chiếu hằng có thể được gắn với một biến hằng lẫn biến thường
    - Ví dụ
      ```cpp
      #include <iostream>

      int main() {
          int x = 5; // biến thường
          const int y = 10; // biến hằng
      
          const int& ref1 = x; // tham chiếu hằng gắn với biến thường
          const int& ref2 = y; // tham chiếu hằng gắn với biến hằng
      
          std::cout << "ref1: " << ref1 << std::endl;
          std::cout << "ref2: " << ref2 << std::endl;
      
          x = 7; // thay đổi giá trị của biến thường
          // y = 15; // Lỗi! Không thể thay đổi giá trị của biến hằng
      
          std::cout << "ref1 sau khi thay doi x: " << ref1 << std::endl;
          std::cout << "ref2 sau khi thay doi y: " << ref2 << std::endl;
      
          return 0;
      }
      ```
      ```cpp
      ref1: 5
      ref2: 10
      ref1 sau khi thay doi x: 7
      ref2 sau khi thay doi y: 10
      ```
Trở lại vấn đề chính, **phương thức thiết lập sao chép** của một lớp đối tượng là phương thức thiết lập có 1 **tham số đầu vào là tham chiếu** tới một đối tượng của lớp đó. Mục đích của phương thức này là để sao chép dữ liệu của một đối tượng vào một đối tượng khác vừa được khai báo
```cpp
HocSinh (const HocSinh& temp)
{
  cout << "Copy constructor of HocSinh has been called!\n";
  mssv = temp.mssv;
  hoTen = temp.hoTen;
  diemToan = temp.diemToan;
  diemVan = temp.diemVan;
  diemTB = temp.diemTB;
}
```
Trong chương trình ta gọi thực hiện phương thức sao chép bằng cách khai báo:
```cpp
HocSinh hs2(hs);
```
Hoặc:
```cpp
HocSinh hs2 = hs;
```
Chương trình tới đây sẽ **không sao chép dữ liệu** của hs vào temp mà chỉ xem temp như là **một cái tên khác** của hs<br>
**Lưu ý!**<br>
Chúng ta thấy rằng nếu **temp** không được khai báo là tham chiếu mà chỉ là một biến bình thường thì chương trình sẽ ngầm thực hiện dòng lệnh:
```cpp
 const HocSinh temp = hs;
```
Lúc này trong quá trình thực hiện phương thức thiết lập sao chép để sao chép hs và hs2, chương trình phải gọi thêm một phương thức thiết lập sao chép khác để sao chép **hs** vào **temp**. Cứ như vậy tạo thành một **vòng lặp vô hạn**<br>
Trong phương thức trên, ta khai báo tham chiếu temp là hằng để đảm bảo đối số truyền vào
**không thể bị sửa đổi** một cách vô ý, cũng như đảm bảo rằng có thể truyền vào phương thức
một **đối số hằng**.<br>
**Một số trường hợp khác mà phương thức thiết lập sao chép được gọi thực hiện:**
- Khi truyền một đối số vào lời gọi hàm của môt hàm có tham số tương ứng không phải là tham chiếu (vd trên)
- Khi kết thúc lời gọi hàm, hàm trả về đối tượng mà kiểu dữ liệu của hàm không phải tham chiếu
- Khi khởi tạo các phần tử của một mảng sử dụng dấu ngoặc nhọn. Ví dụ:
  ```cpp
    HocSinh arr[2] = {hs};
  ```
  Lúc này chương trình gọi phương thức thiết lập sao chép để sao chép **hs** vào phần tử đầu tiên của mảng, và gọi thực hiện phương thức thiết lập mặc định để khởi tạo giá trị cho phần tử thứ 2
## Phương thức phá hủy (Destructor)
- Mục đích:
 - Thông thường, phương thức phá hủy có nhiệm vụ thu hồi lại tất cả các tài nguyên đã cấp phát cho đối tượng khi đối tượng hết phạm vi hoạt động (scope)
- Đặc điểm:
  - Tên phương thức trùng với tên lớp nhưng có dấu ngã ở đằng trước
  - Không có giá trị trả về
  - Không có tham số đầu vào
  - Được tự động gọi thực hiện trước khi đối tượng bị hủy
  - Có và chỉ có duy nhất một phương thức phá hủy trong một lớp
  - Trong quá trình sống của đối tượng có và chỉ có một lần phương thức phá hủy được gọi thực hiện
- Ý nghĩa:
Một cách dùng của phương thức phá hủy là để giải phóng bộ nhớ của các thuộc tính
được cấp phát động trong một đối tượng. Nếu chúng ta không giải phóng các vùng
nhớ này, nó sẽ bị tồn đọng lại và chiếm không gian không cần thiết<br>
### Phương thức phá hủy và cấp phát động
```cpp
class LopHoc
{
private:
	HocSinh* arr;
	int size;
public:
	LopHoc (int size)
	{
		this->size = size;
		arr = new HocSinh[size];
	}
};
```
Trong hàm main
```cpp
int main(){
    LopHoc lop(70);
    return 0;
}
```
Khi chương trình kết thúc, đối tượng **lóp** bị phá hủy, kéo theo các dữ liệu thành phần là **arr** và **size** bị phá hủy theo, tuy nhiên vùng nhớ được cấp phát cho biến con trỏ arr vẫn còn đó mà chưa được thu hồi.<br>
Để giải quyết vấn đề này, ta sẽ định nghĩa cho lớp LopHoc một phương thức phá hủy như
sau:
```cpp
~LopHoc(){
	cout << "Destructor has been called" << endl;
	delete[] arr;
}
```
Nếu chúng ta không tự định nghĩa một phương thức phá hủy, chương trình cũng sẽ tự
định cho ta một phiên bản như đây:
```cpp
	~LopHoc() { }
```
Phương thức phá hủy này không thực hiện bất cứ thao tác gì nên có thân hàm rỗng. Đối với
những lớp đối tượng có thành phần được khai báo tĩnh thì có thể sử dụng phiên bản do
chương trình tự định nghĩa mà không cần phải tự định nghĩa một phiên bản riêng<br>
**Một số trường hợp khác mà phương thức phá hủy được gọi:**
- Đối tượng bị phá hủy khi ra khỏi phạm vi hoạt động
- Đối tượng được cấp phát động bị hủy khi sử dụng toán tử **delete** lên biến con trỏ trỏ tới nó
```cpp
 HocSinh* hsPtr = new HocSinh();
 delete hsPtr;   // Phương thức phá hủy của biến học sinh được gọi
```
- Các dữ liệu thành viên bị hủy và đối tượng chúng thuộc về bị hủy
### Phương thức phá hủy và phương thức thiết lập sao chép
Khi thiết kế các lớp đối tượng, có một nguyên tắc là nếu một lớp cần phải tự định nghĩa phương thức phá hủy, thì lớp đó cũng cần tự định nghĩa một phương thức thiết lập sao chép của riêng mình

Trong ví dụ ở trên, nếu không làm gì thêm, ctrinh sẽ tự định nghĩa cho ta một phương thức thiết lập sao chép như sau:
```cpp
LopHoc (const LopHoc& temp)
{
	this->arr = temp.arr;
	this->size = temp.size;
}
```
Tại dòng số 2, địa chỉ mà biến-con-trỏ-arr-thuộc-đối-tượng-temp đang nắm giữ được sao
chép vào biến con trỏ arr của đối tượng đang thực hiện lời gọi phương thức. Lúc này hai con
trỏ có giá trị bằng nhau, tức là chúng đang cùng nắm giữ một vùng nhớ

Để tránh lỗi trên, ta cần phải định nghĩa lại phương thức sao chép cho **LopHoc**
```cpp
LopHoc(const LopHoc& temp) {
	size = temp.size;
	arr = new HocSinh[size];
	for (int i = 0; i < size; ++i) {
		arr[i] = temp.arr[i];
	}
}
```
## Thành phần tĩnh
Các thành phần tĩnh là các thành phần thuộc về một lớp chứ **không thuộc về một đối tượng** cụ thể. Điều này có nghĩa là tất cả các đối tượng của một lớp đều chia sẻ chung một thành phần tĩnh, và nó có thể được truy cập thông qua một đối tượng.

Có hai loại thành phần tĩnh:
- Các thuộc tính tĩnh
- Hàm thành viên tĩnh
### Khởi tạo thành viên tĩnh
```cpp
class HocSinh
{
private:
	static int demHs;
public:
	static int getDemHocSinh ();
};
```
### Cách gọi các thành viên tĩnh
Chúng ta có thể truy cập trực tiếp một thành viên tĩnh thông qua toán tử phạm vi, vd:
```cpp
	int dem = HocSinh::getDemHs();
```
Mặc dù các thành viên tĩnh không phải là một phần đối tượng, chúng ta vẫn có thể dùng các đối tượng của một lớp để truy cập đến các thành phần tĩnh của lớp đó
```cpp
	HocSinh h1;
 	int dem = h1.getDemHs();
```
## Hàm bạn, lớp bạn (Friends)
### Hàm bạn
Hàm bạn là hàm có thể truy cập thành phần **private** hoặc **protected** của lớp xem nó là bạn
```cpp
class MyClass1
{
private:
	int tpRiengTu;
	friend void myFunct (MyClass1 mClass);
};
void myFunct (MyClass1 mClass)
{
	cout << mClass.tpRiengTu;
}
```
### Lớp bạn
Tương tự,  lớp bạn là lớp có thể truy cập thành phần **private** hoặc **Protected** của lớp xem nó là bạn
```cpp
class MyClass2 {
public:
	void myMethod(MyClass1 mClass) {
		cout << mClass.tpRiengTu; // Không hợp lệ
	}
};
```
```cpp
class MyClass1 {
	friend class MyClass2;
	//...
};
```

