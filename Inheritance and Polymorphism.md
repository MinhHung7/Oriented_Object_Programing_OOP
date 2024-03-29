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
![](https://github.com/MinhHung7/Oriented_Object_Programing_OOP/blob/main/Inheritance%20Table.png)
<br>Nếu lớp cha có các thuộc tính **protected** và lớp con kế thừa theo kiểu **private** thì các thuộc tính **protected** của cha trở thành các thuộc tính **private** của lớp con
## Phương thức thiết lập trong kế thừa
Mặc dù một đối tượng của lớp con được thừa hưởng các thuộc tính từ lớp cha, nó không
nên trực tiếp khởi tạo dữ liệu cho các thuộc tính đó (trong vài trường hợp thì là không thể
luôn). Ở các ví dụ trên, lớp BulkQuote kế thừa 2 thuộc tính là bookNo và price từ Quote,
tuy nhiên bookNo là thành phần private của Quote, kể cả lớp con cũng không truy cập
được thuộc tính này, dẫn đến việc BulkQuote không thể trực tiếp gán dữ liệu cho bookNo.
Cho dù các thuộc tính này đều là protected và lớp con có thể truy cập được đi chăng nữa,
lớp con cũng không nên khởi tạo dữ liệu trực tiếp cho chúng (bởi vì lớp cha có cung cấp các
giao diện để tương tác với các thuộc tính của nó, lớp con nên tôn trọng và sử dụng giao diện
này).

Tóm lại, lớp con nên sử dụng phương thức thiết lập của lớp cha để khởi tạo dữ liệu cho
các thuộc tính chung mà nó được thừa kế. Cách sử dụng như sau (lấy ví dụ là phương thức
thiết lập cho lớp BulkQuote):
```cpp
//Phương thức thiết lập của Quote
Quote::Quote(string id, double price) : bookNo(id), price(price) {}
//Phương thức thiết lập của Bulk_quote
BulkQuote::BulkQuote(string id, double price, double disc, int n)
				: Quote(id,price), discount(disc), minQty(n) {}
```
```cpp
	BulkQuote derived("22120123", 150000, 0.2, 3);
```
**Constructor mặc định**
Khi một đối tượng của lớp con được khởi tạo mặc định, thứ tự như trên cũng được thực
hiện, tức là **constructor mặc định của lớp cha được gọi trước** để khởi tạo dữ liệu mặc định
cho các thuộc tính chung, sau đó constructor của lớp con mới bắt đầu thực hiện việc gán dữ
liệu cho các thuộc tính riêng.
## Phép gán và con trỏ trong kế thừa
Thông thường, một biến con trỏ chỉ có thể giữ địa chỉ của các đối tượng có cùng kiểu với nó, tuy nhiên trong kế thừa có một ngoại lệ: **một con trỏ đối tượng lớp cơ sở có thể giữ địa chỉ của một đối tượng thuộc lớp dẫn xuất**. Dẫu vậy, một con trỏ đối tượng thuộc lớp dẫn xuất không thể giữ địa chỉ của một đối tượng thuộc lớp cơ sở, vd:
```cpp
	Quote base;
	BulkQuote derived;
	Quote* basePtr = &derived; // Đúng
	BulkQuote* derivedPtr = &base; // Sai
```
Việc có thể gán địa chỉ của một đối tượng thuộc lớp dẫn xuất cho một biến con trỏ đối tượng
thuộc lớp cơ sở dẫn đến một kết quả quan trọng: Khi sử dụng một con trỏ đối tượng thuộc
lớp cơ sở, chúng ta không biết chắc được đối tượng mà con trỏ đó sẽ giữ có kiểu dữ liệu gì,
nó có thể là một đối tượng thuộc lớp cơ sở hoặc lớp dẫn xuất. Điều này góp phần tạo nên
tính đa hình trong OOP sẽ được tìm hiểu ở chương tới.<br>
**Phép gán trực tiếp giữa các đối tượng**
Ta cũng có thể gán trực tiếp một đối tượng thuộc lớp con cho một đối tượng thuộc lớp
cha. Ngược lại, không thể gán một đối tượng của lớp cha cho một đối tượng thuộc lớp con.
Tuy nhiên có một vài điểm cần lưu ý: Khi dùng một biến có kiểu lớp con khởi tạo cho một
đối tượng thuộc lớp cha, chương trình sẽ chỉ sao chép những thuộc tính chung giữa 2 lớp
mà không sao chép các thuộc tính riêng của lớp con. Đơn giản là vì lớp cha thì không thể
biết được các lớp con của nó có các thuộc tính mới nào, nó chỉ biết được những thuộc tính
đã được định nghĩa sẵn bên trong mình mà thôi.
```cpp
Quote item1;
BulkQuote item2("13hd", 50000, 0.2, 3);
item1 = item2;
```
Sau dòng lệnh trên, item1 lúc này chỉ chứa 2 thuộc tính là bookNo = 13hd và price =
50000, 2 thuộc tính discount = 0.2 và minQty = 3 trong item2 đã bị lược bỏ.
## Phương thức ảo (virtual function) và đa hình (Polymorphism)
Lớp dẫn xuất được kế thừa từ các phương thức đã có ở lớp cơ sở, tuy nhiên hành vi của chúng có thể được tinh chỉnh để tương thích hơn với lớp dẫn xuất. Để làm vậy, lớp dẫn xuất cần phải được định nghĩa lại **một phiên bản khác** cho các phương thức đó.

Trong lớp cơ sở, ta thêm từ khóa **virtual** vào trước phần khai báo của những phương thức mà lớp dẫn có thể **ghi đè** lại (**override**), những phương thức này sẽ được gọi là **phương thức ảo**. Khi gọi các phương thức ảo thông qua một con trỏ đối tượng, lời gọi sẽ được thực hiện theo cơ chế **đa hình**, cho phép xác định đúng hành vi (phương thức) sẽ được thực thi. Tùy thuộc vào kiểu dữ liệu của đối tượng mà con trỏ giữ địa chỉ, phiên bản của phương thức ảo nằm trong lớp cơ sở hoặc lớp dẫn xuất sẽ được thực hiện (nhớ lại rằng một con trỏ thuộc lớp cơ sở có thể giữ địa chỉ của một đối tượng thuộc lớp dẫn xuất).

Ngoại trừ các phương thức tĩnh và phương thức thiết lập, các phương thức khác đều có thể được khai báo là phương thức ảo. Những phương thức được khai báo là **virtual** trong lớp cơ sở thì những phương thức **cùng tên** và **cùng danh sách tham số** đầu vào trong lớp dẫn xuất cũng sẽ là phương thức ảo.
## Lớp cơ sở trừu tượng (Abstract base class)
## Phương thức phá hủy trong kế thừa
Như đã nói ở phần phương thức thiết lập trong kế thừa, khi một đối tượng được khởi tạo,
các thuộc tính chung sẽ được khởi tạo trước rồi mới đến các thuộc tính riêng. Phương thức
phá hủy thì ngược lại, khi một destructor của lớp con được gọi, nó sẽ thu hồi các tài nguyên
đã cấp phát cho các thuộc tính riêng trước, rồi sau đó destructor của lớp cha mới được gọi
để dọn dẹp các thuộc tính chung (rác của ai người đó dọn:v)
