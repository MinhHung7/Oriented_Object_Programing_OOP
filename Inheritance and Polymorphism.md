# Inheritance (kế thừa) và Polymorphism (đa hình)
## Mối quan hệ đặc biệt, tổng quát hóa
- Hai đối tượng được gọi là quan hệ đặc biệt hóa - tổng quát hóa nhau khi, lớp đối tượng này là trường hợp đặc biệt của lớp đối tượng kia và lớp đối tượng kia là trường hợp tổng quát của đối tượng này.
- Kí hiệu:<br>
![](https://github.com/MinhHung7/Oriented_Object_Programing_OOP/blob/main/Inheritance%20Ex.png)
<br>**Cây kế thừa**
- Cây kế thừa là một cây đa nhánh thể hiện mối quan hệ đặc biệt hóa - tổng quát hóa giữa các lớp trong hệ thống, trong chương trình
- Vd:<br>
![image](https://github.com/MinhHung7/Oriented_Object_Programing_OOP/assets/118424791/99ad2cb4-5ef0-4ca5-ba46-48fcfb02f10d)
## Kế thừa
- Lớp kế thừa từ một lớp khác được gọi là **lớp con (child class, subclass)** hay **lớp dẫn xuất (derived class)**. Lớp được các lớp khác kế thừa được gọi là **lớp cha (parent class, superclass, base class)**
**Lợi ích của kế thừa**
  - Kế thừa cho phép xấy dựng lớp mới từ lớp đã có
  - Kế thừa cho phép tổ chức các lớp chia sẽ mã chương trình dùng chung, nhờ vậy mà có thể dễ dàng sửa chữa, nâng cấp hệ thống
  - Định nghĩa sự tương thích giữa các lớp, nhờ đó ta có thể chuyển kiểu tự động
## Định nghĩa lớp cơ sở và lớp dẫn xuất trong C++
### Bài toán quản lý cửa hàng danh sách
Lấy ví dụ về bài toán quản lí hóa đơn trong một hiệu sách, chủ cửa hàng muốn áp dụng
các phương thức tính tiền khác nhau cho các loại sách khác nhau. Một vài quyển sách chỉ
được bán ở một mức giá cố định, trong khi một vài quyển khác sẽ được giảm giá khi mua
với số lượng lớn.

Để giải quyết vấn đề, ta sẽ tạo một lớp cơ sở có tên là Quote đại diện cho những quyển
sách không được giảm giá và lớp BulkQuote được kế thừa từ lớp Quote, tượng trưng cho
những loại sách sẽ được áp mã giảm giá khi mua trên một số lượng nhất định. Hai lớp sẽ có
chung các thuộc tính là mã số sách và giá tiền, cùng với một phương thức đặc biệt dùng để
tính tiền. Trước tiên hãy cùng xem sơ qua định nghĩa của hai lớp này
### Định nghĩa lớp cơ sở
```cpp
class Quote
{
private:
	string bookNo; // mã số sách
protected:
	double price; // giá của một quyển sách
public:
	Quote ();
	Quote (const string& book, double salePrice);
	string getBookNo ()
	{
		return bookNo;
	}
	virtual double netPrice (int n)
	{
		return price * n;
	}
};
```
### Phạm vi truy xuất protected trong kế thừa
Trong trường hợp ta muốn một vài thành viên của lớp cơ sở **có thể truy cập ở lớp dẫn xuất** trong khi vẫn **giới hạn quyền truy cập từ người dùng**. Những thành viên như vậy được chỉ định là các thành viên **protected**.<br>
Phạm vi truy xuất **protected** có thể được xem như là một sự kết hợp giữa **public** và **private**
- Giống với **private**, các thành viên **protected** không thể truy cập bởi người dùng bên ngoài
- Giống với **public**, các thành viên **protected** của lớp cơ sở có thể được truy cập bởi bạn và các lớp dẫn xuất của nó

Trong ví dụ về lớp cơ sở Quote, thuộc tính price được chỉ định là protected nên các
hàm thành viên của các lớp kế thừa từ Quote có thể truy cập trực tiếp vào nó trong khi người
dùng thì không. Thuộc tính bookNo được chỉ định là private nên không thể được truy cập
trực tiếp từ bên ngoài lớp, kể cả là các lớp con hay người dùng. Còn lại các thành viên public
thì có thể được truy cập ở bất cứ đâu
### Định nghĩa lớp dẫn xuất
```cpp
class BulkQuote : public Quote
{
private:
	double discount;  // tỉ lệ phần trăm được giảm
	int minQty;  // số lượng mua tối thiểu để được áp mã
public:
	BulkQuote ();
	BulkQuote (const string& book, double salePrice, double disc, int cnt);
	double NetPrice (int n);
};
```
## Các kiểu kế thừa
