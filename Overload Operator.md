# Overload Operator
## Nạp chồng toán tử
Cũng như nạp chồng hàm **(overload function)**, bạn có thể định nghĩa nhiều hàm có cùng tên nhưng khác tham số truyền vào. Nạp chồng toán tử **(overload operator)** cũng tương tự, bạn **định nghĩa lại toán tử đã có** trên kiểu dữ liệu người dùng tự đinh nghĩa để dễ dàng thực hiện các câu lệnh trong chương trình
```cpp
	PhanSo ps1(1, 2);
	PhanSo ps2(2, 3);
	PhanSo ketQua;
	ketQua = ps1.Tong(ps2); // Dùng hàm
	ketQua = ps1 + ps2;    // Dùng overload operator
```
### Cơ chế hoạt động
Về bản chất, việc thực hiện các toán tử cũng tương đương với việc gọi hàm, ví dụ:
```cpp
	PhanSo a(1, 2);
	PhanSo b(2, 3);
	PhanSo ketQua = a + b;
	// Tương đương với
	PhanSo ketQua = a.operator+(b);
```
**Các toán tử có thể overload**
![](https://github.com/MinhHung7/Oriented_Object_Programing_OOP)
### Cú pháp Overload
Chúng ta sẽ overload hàm có tên **"operator@"**, với **@** là các toán tử cần overload. Có 2 loại là **hàm cục bộ** và **hàm toàn cục**
- **Cài đặt với hàm cục bộ**
  ```cpp
  class PhanSo {
	private:
		int tu;
		int mau;
	public:
		PhanSo() { tu = 0; mau = 1; }
		PhanSo(int a, int b) { tu = a; mau = b; }
		PhanSo operator+(const PhanSo& ps){ // overload toán tử +
			PhanSo kq;
			kq.tu = this->tu * ps.mau + ps.tu * this->mau;
			kq.mau = this->mau * ps.mau;
			return kq;
		}
	};
	```
- **Cài đặt hàm toàn cục**
Thông thường nếu ta sử dụng operator+(PhanSo a) thì ta sẽ có PhanSo + PhanSo
<br>Nếu ta dùng operator + (int i) thì ta có PhanSo + i
<br> Vậy để có i + PhanSo, ta **cài đặt toàn cục**
```cpp
#include<iostream>
using namespace std;

class PhanSo
{
private:
	int tu, mau;
public:
	PhanSo (int tu, int mau)
	{
		this->tu= tu;
		this->mau = mau;
	}
	PhanSo ()
	{
		tu = 0;
		mau = 0;
	}
	PhanSo operator +(const PhanSo& ps, const int& i);
	PhanSo operator +(const int& i, const PhanSo& ps);

};

PhanSo operator +(const PhanSo& ps, const int& i)
{
	PhanSo kq;
	kq.tu = ps.tu + i * ps.mau;
	return kq;
}

PhanSo operator +(const int& i, const PhanSo& ps)
{
	return ps + i;
}


int main ()
{
	PhanSo a (1, 2);
	int i = 1;
	PhanSo c = a + i;
}
```
Đoạn mã trên bị sai thì operator trong class chỉ chấp nhận 1 tham số. Do đó nếu muốn dùng 2 tham số, ta phải viết lại hàm ở ngoài. Nhưng để viết hàm ở ngoài có được biến private ta phải dùng hàm bạn
```cpp
#include<iostream>
using namespace std;

class PhanSo
{
private:
	int tu, mau;
public:
	PhanSo (int tu, int mau)
	{
		this->tu= tu;
		this->mau = mau;
	}
	PhanSo ()
	{
		tu = 0;
		mau = 0;
	}
	friend PhanSo operator +(const PhanSo& ps, const int& i);
	friend PhanSo operator +(const int& i, const PhanSo& ps);

};

PhanSo operator +(const PhanSo& ps, const int& i)
{
	PhanSo kq;
	kq.tu = ps.tu + i * ps.mau;
	return kq;
}

PhanSo operator +(const int& i, const PhanSo& ps)
{
	return ps + i;
}


int main ()
{
	PhanSo a (1, 2);
	int i = 1;
	PhanSo c = a + i;
}
```
### Chuyển kiểu
Có 2 loại chuyển kiểu:
- Chuyển kiểu bằng constructor
- Chuyển kiểu bằng toán tử chuyển kiểu
**Chuyển kiểu bằng constructor**
  ```cpp
  #include<iostream>
using namespace std;

class PhanSo
{
private:
	int tu, mau;
public:
	PhanSo (int tu, int mau)
	{
		this->tu= tu;
		this->mau = mau;
	}
	PhanSo (int a)
	{
		this->tu = a;
		this->mau = 1;
	}
	PhanSo ()
	{
		tu = 0;
		mau = 0;
	}
	friend PhanSo operator+(const PhanSo& ps1, const PhanSo& ps2);

};

PhanSo operator +(const PhanSo& ps1, const PhanSo& ps2)
{
	PhanSo kq;
	kq.mau = ps1.mau * ps2.mau;
	kq.tu = ps1.tu * ps2.mau + ps1.mau * ps2.tu;
	return kq;
}

int main ()
{
	PhanSo a (1, 2);
	int i = 1;
	PhanSo c = a + i;
}
	```
**Chuyển kiểu bằng toán tử chuyển kiểu**
Cú pháp
```cpp
operator KieuDL() {
	return x; // x có kiểu dữ liệu là Kieu_DL
}
```
VD muốn chuyển phân số về **float**
```cpp
class PhanSo {
	//...
	operator float();
};
	// Định nghĩa
	PhanSo::operator float() {
	return (float)this->tu / this->mau;
}
```
### Sự nhập nhằng
Sự nhập nhằng xảy ra khi có chuyển kiểu bằng constructor lẫn chuyển bằng toán tử chuyển kiểu. Nó khiến cho trình biên dịch không xác định được nên chuyển kiểu bằng cách nào, dẫn đến việc mất đi cơ chế chuyển kiểu tự động (ngầm định)
```cpp
class PhanSo
{
	//...
public:
	PhanSo (int a);
	operator float ();
};

int main ()
{
	PhanSo a (1, 2);
	a + 2; 
	2 + a;
	// lỗi do không biết nên chuyển 5 thành phân số hay phân số thành float
}
```
Cách xử lý duy nhất cho việc này là thực hiện chuyển kiểu tường minh, việc này làm mất đi sự tiện lợi của cơ chế chuyển đổi tự động. Do đó khi thực hiện chuyển kiểu, ta chỉ được chọn một trong hai, hoặc là chuyển đổi bằng constructor hoặc chuyển đổi bằng toán tử chuyển kiểu.
## Toán tử nhập, xuất (input, output)
Để nạp chồng toán tử nhập xuất, chúng ta sử dụng **hàm toàn cục** (và là **hàm bạn**), có **hai tham số**, tham số đầu tiên là một **tham chiếu** đến đối tượng kiểu **istream** hoặc **ostream**, tham số thứ hai là một **tham chiếu** tới đối tượng cần nhập/xuất, kiểu trả về của hàm chính là **tham chiếu** đến tham số đầu tiên của hàm (**istream** hoặc **ostream**).

**Toán tử nhập**<br>
Chúng ta sẽ thực hiện overload toán tử nhập cho lớp phân bố như sau:
```cpp
class PhanSo
{
	//...
	friend istream& operator >> (istream&, PhanSo&);
};
istream& operator>>(istream& input, PhanSo& ps)
{
	input >> ps.tu;
	input >> ps.mau;

	return input;
}
```
**Toán tử xuất**<br>
```cpp
class PhanSo
{
	//...
	friend istream& operator >> (istream&, PhanSo&);
	friend ostream& operator << (ostream&, const PhanSo&);
};
istream& operator>>(istream& input, PhanSo& ps)
{
	input >> ps.tu;
	input >> ps.mau;

	return input;
}
ostream& operator << (ostream& output, const PhanSo& ps)
{
	output << ps.tu << " / " << ps.mau;
	return output;
}
```
Khác biệt duy nhất nằm ở chỗ tham số thứ 2 của hàm này nên là một **tham chiếu hằng** nhằm tránh việc phải thực hiện sao chép quá nhiều (tốn tài nguyên) đồng thời đảm bảo đối số truyền vào sẽ không bị thay đổi
## Toán tử so sánh (Relational Operator)
```cpp
class PhanSo
{
private:
	int tu;
	int mau;
	//...
	friend istream& operator >> (istream&, PhanSo&);
	friend ostream& operator << (ostream&, PhanSo&);
	friend bool operator > (const PhanSo& a, const PhanSo& b);
};

bool operator > (const PhanSo& a, const PhanSo& b)
{
	float gt1 = (float)a.tu / a.mau;
	float gt2 = (float)b.tu / b.mau;

	return gt1 > gt2;
}
```
## Toán tử gán 
```cpp
class PhanSo
{
private:
	int tu;
	int mau;
	//...
	friend istream& operator >> (istream&, PhanSo&);
	friend ostream& operator << (ostream&, PhanSo&);
	friend bool operator > (const PhanSo& a, const PhanSo& b);
	PhanSo& operator = (const PhanSo& a)
	{
		this->tu = a.tu;
		this->mau = a.mau;
		return *this;
	}
};
```
## Toán tử số học, gán kết hợp
```cpp
class PhanSo
{
private:
	int tu;
	int mau;
	//...
	friend istream& operator >> (istream&, PhanSo&);
	friend ostream& operator << (ostream&, PhanSo&);
	friend bool operator > (const PhanSo& a, const PhanSo& b);
	PhanSo& operator += (const PhanSo& a)
	{
		this->tu += a.tu;
		this->mau += a.mau;
		return *this;
	}
};
```

