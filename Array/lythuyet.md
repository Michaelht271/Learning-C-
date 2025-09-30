		Array
I. Định nghĩa
	Mảng (array) được sử dụng để lưu trữ nhiều giá trị trong một biến duy nhất, thay vì khai báo nhiều biến riêng lẻ cho từng giá trị.

II. Tính chất
	1. Array chỉ lưu được 1 loại kiểu dữ liệu được khai báo.
	2. Kích thước array là cố đinh, nếu muốn lưu thêm giá trị -> tạo array lớn hơn và copy sang.
	3.Các phần tử trong array là liên tiếp nhau trong bộ nhớ.
	4. Truy cập mảng thông quan chỉ số (index)
	5. Truy cập phần tử trong mảng có thời gian O(1) ( tức là truy cập trực tiếp)
	6. Tên mảng là địa chỉ phần tử đầu tiên ( nếu in ra array là không có chỉ số, chính là in ra địa chỉ của phần tử đầu tiên)
	7. Truy vấn Array có thể dùng vòng lặp ( while(), for(;;))
    
III.Cách khai báo
	1.Để khai báo một mảng, bạn cần định nghĩa kiểu dữ liệu, chỉ định tên của mảng kèm theo dấu ngoặc vuông, và chỉ định số lượng phần tử mà nó sẽ lưu trữ:
	Syntax:
		datatype array_name[size];
	Example:
		string cars[4];
	
	2.Có thể tạo một mảng và đặt các giá trị trong một danh sách cách nhau bằng dấu phẩy, bên trong dấu ngoặc nhọn:
	Syntax:
		datatype array_name[] = {value_1, value_2, ...};
	Example:
		string cars[] = {"Volvo", "BMW", "Ford", "Mazda"};

IV.Hoạt động với hàm
	Khi viết một hàm cần kiểu dữ liệu trả về là Array, C++ KHÔNG HỖ TRỢ trả về mảng trực tiếp. Do đó, chúng ta phải sử dụng các phương pháp thay thế.

	## 1. Con trỏ (Pointer)

	Con trỏ là một biến lưu địa chỉ (tương tự như tên mảng - xem lại tính chất mảng). Ta khai báo con trỏ chỉ đến vị trí đầu tiên của mảng, và truy cập các phần tử giống như mảng.

	Điểm KHÁC BIỆT quan trọng:
	Con trỏ KHÔNG lưu trữ số lượng phần tử của mảng, nên khi truyền vào hàm, ta 		phải truyền thêm kích thước.
	
	Cú pháp khai báo:

		data_type* array_name;
	 Example:
	 	int* number_list;
	 
	 Con trỏ là biến lưu địa chỉ và truy cập các phần tử thông qua index. Khi khai báo như trên, hệ thống CHƯA cấp phát bộ nhớ cho mảng. Vì vậy, ta cần chủ động cấp phát bộ nhớ.
	Cấp phát bộ nhớ:
	Cách 1: Dùng malloc (C style - không khuyến khích trong C++)
		data_type* array = (data_type*)malloc(n * sizeof(data_type));
		// Nhớ giải phóng bộ nhớ
		free(array);
	Cách 2: Dùng new (C++ style - KHUYẾN KHÍCH)
		data_type* array = new data_type[n];
		// Nhớ giải phóng bộ nhớ
		delete[] array;
		
	Example:
	```
		#include <stdio.h>
		#include <stdlib.h>

		// Hàm tạo và trả về mảng thông qua con trỏ
		int* createArray(int n) {
  		
  			// Cấp phát bộ nhớ động
   			int* array = new int[n];
    
    			// Khởi tạo giá trị cho mảng
    			for(int i = 0; i < n; i++) {
        			array[i] = i + 1;
    			}
    
    			return array;  // Trả về con trỏ
		}

			// Hàm nhận mảng và kích thước
		void printArray(int* array, int n) {
    			for(int i = 0; i < n; i++) {
        			printf("%d ", array[i]);
    			}
    			printf("\n");
		}

		int main() {
    			int n = 5;
    
    			// Nhận con trỏ mảng từ hàm
    			int* numbers = createArray(n);
    
    			// In mảng
    			printArray(numbers, n);
    
    			// QUAN TRỌNG: Giải phóng bộ nhớ
    			delete[] numbers;
    
    			return 0;
		}
```
