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
