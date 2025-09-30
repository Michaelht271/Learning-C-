# Array

## I. Định nghĩa
Mảng (array) được sử dụng để lưu trữ nhiều giá trị trong một biến duy nhất, thay vì khai báo nhiều biến riêng lẻ cho từng giá trị.

## II. Tính chất
1. Array chỉ lưu được 1 loại kiểu dữ liệu được khai báo.
2. Kích thước array là cố định, nếu muốn lưu thêm giá trị → tạo array lớn hơn và copy sang.
3. Các phần tử trong array là liên tiếp nhau trong bộ nhớ.
4. Truy cập mảng thông qua chỉ số (index).
5. Truy cập phần tử trong mảng có thời gian O(1) (tức là truy cập trực tiếp).
6. Tên mảng là địa chỉ phần tử đầu tiên (nếu in ra array không có chỉ số, chính là in ra địa chỉ của phần tử đầu tiên).
7. Truy vấn Array có thể dùng vòng lặp (while(), for()).

## III. Cách khai báo

### 1. Khai báo với kích thước cố định
Để khai báo một mảng, bạn cần định nghĩa kiểu dữ liệu, chỉ định tên của mảng kèm theo dấu ngoặc vuông, và chỉ định số lượng phần tử mà nó sẽ lưu trữ:

**Cú pháp:**
```cpp
datatype array_name[size];
```

**Ví dụ:**
```cpp
string cars[4];
```

### 2. Khai báo và khởi tạo giá trị
Có thể tạo một mảng và đặt các giá trị trong một danh sách cách nhau bằng dấu phẩy, bên trong dấu ngoặc nhọn:

**Cú pháp:**
```cpp
datatype array_name[] = {value_1, value_2, ...};
```

**Ví dụ:**
```cpp
string cars[] = {"Volvo", "BMW", "Ford", "Mazda"};
```

## IV. Hoạt động với hàm
Khi viết một hàm cần kiểu dữ liệu trả về là Array, C++ KHÔNG HỖ TRỢ trả về mảng trực tiếp. Do đó, chúng ta phải sử dụng các phương pháp thay thế.

### 1. Con trỏ (Pointer)
Con trỏ là một biến lưu địa chỉ (tương tự như tên mảng - xem lại tính chất mảng). Ta khai báo con trỏ chỉ đến vị trí đầu tiên của mảng, và truy cập các phần tử giống như mảng.

**Điểm KHÁC BIỆT quan trọng:**  
Con trỏ KHÔNG lưu trữ số lượng phần tử của mảng, nên khi truyền vào hàm, ta phải truyền thêm kích thước.

**Cú pháp khai báo:**
```cpp
data_type* array_name;
```

**Ví dụ:**
```cpp
int* number_list;
```

⚠️ **Lưu ý:**  
Con trỏ là biến lưu địa chỉ và truy cập các phần tử thông qua index. Khi khai báo như trên, hệ thống CHƯA cấp phát bộ nhớ cho mảng. Vì vậy, ta cần chủ động cấp phát bộ nhớ.

### Cấp phát bộ nhớ:

**Cách 1: Dùng malloc (C style - không khuyến khích trong C++)**
```cpp
data_type* array = (data_type*)malloc(n * sizeof(data_type));
// Nhớ giải phóng bộ nhớ
free(array);
```

**Cách 2: Dùng new (C++ style - KHUYẾN KHÍCH)**
```cpp
data_type* array = new data_type[n];
// Nhớ giải phóng bộ nhớ
delete[] array;
```

### Ví dụ hoàn chỉnh:

```cpp
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

### Tóm tắt:
- ✅ Khai báo: `int* array;`
- ✅ Cấp phát: `array = new int[n];` (C++) hoặc `malloc` (C)
- ✅ Giải phóng: `delete[] array;` (C++) hoặc `free(array)` (C)
- ⚠️ Luôn truyền kèm kích thước khi dùng con trỏ
- ⚠️ Nhớ giải phóng bộ nhớ để tránh memory leak

### 2. Vector (KHUYẾN KHÍCH trong C++)
Vector là một container động trong thư viện STL (Standard Template Library) của C++. Vector tự động quản lý bộ nhớ và có thể thay đổi kích thước linh hoạt.

**Ưu điểm so với con trỏ:**
- Tự động quản lý bộ nhớ (không cần delete)
- Có thể thay đổi kích thước (thêm/xóa phần tử)
- An toàn hơn (kiểm tra giới hạn với `.at()`)
- Có nhiều hàm tiện ích sẵn có

**Cú pháp khai báo:**
```cpp
#include <vector>

std::vector<data_type> vector_name;
std::vector<data_type> vector_name(size);
std::vector<data_type> vector_name = {value_1, value_2, ...};
```

**Ví dụ:**
```cpp
#include <vector>

std::vector<int> numbers;              // Vector rỗng
std::vector<int> numbers(5);           // Vector 5 phần tử, giá trị mặc định 0
std::vector<int> numbers(5, 10);       // Vector 5 phần tử, mỗi phần tử = 10
std::vector<int> numbers = {1, 2, 3};  // Vector với giá trị khởi tạo
```

**Các thao tác cơ bản:**
```cpp
std::vector<int> vec;

// Thêm phần tử
vec.push_back(10);           // Thêm 10 vào cuối
vec.push_back(20);

// Truy cập phần tử
int first = vec[0];          // Truy cập trực tiếp (không kiểm tra)
int second = vec.at(1);      // Truy cập an toàn (có kiểm tra)

// Kích thước
int size = vec.size();       // Số phần tử hiện tại
bool empty = vec.empty();    // Kiểm tra rỗng

// Xóa phần tử
vec.pop_back();              // Xóa phần tử cuối
vec.clear();                 // Xóa tất cả phần tử

// Thay đổi kích thước
vec.resize(10);              // Đổi kích thước thành 10
```

### Ví dụ hoàn chỉnh với Vector:

```cpp
#include <iostream>
#include <vector>

// Hàm tạo và trả về vector
std::vector<int> createVector(int n) {
    std::vector<int> vec;
    
    // Thêm giá trị vào vector
    for(int i = 0; i < n; i++) {
        vec.push_back(i + 1);
    }
    
    return vec;  // Trả về vector (tự động copy hoặc move)
}

// Hàm nhận vector (truyền tham chiếu để tiết kiệm bộ nhớ)
void printVector(const std::vector<int>& vec) {
    for(int i = 0; i < vec.size(); i++) {
        std::cout << vec[i] << " ";
    }
    std::cout << std::endl;
}

// Hoặc dùng range-based for loop (C++11)
void printVectorModern(const std::vector<int>& vec) {
    for(int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
}

int main() {
    int n = 5;
    
    // Tạo vector
    std::vector<int> numbers = createVector(n);
    
    // In vector
    printVector(numbers);
    printVectorModern(numbers);
    
    // Thêm phần tử mới
    numbers.push_back(6);
    numbers.push_back(7);
    
    std::cout << "After adding: ";
    printVector(numbers);
    
    // KHÔNG CẦN delete - vector tự động giải phóng bộ nhớ!
    
    return 0;
}
```

### So sánh Con trỏ vs Vector:

| Tiêu chí | Con trỏ (Pointer) | Vector |
|----------|-------------------|--------|
| Quản lý bộ nhớ | Thủ công (new/delete) | Tự động |
| Kích thước | Cố định | Động (thay đổi được) |
| An toàn | Thấp (dễ lỗi) | Cao (có kiểm tra) |
| Hiệu năng | Nhanh hơn một chút | Tốt (overhead nhỏ) |
| Sử dụng | Code C-style | Code C++ hiện đại |
| Khuyến nghị | Chỉ khi cần thiết | **Ưu tiên sử dụng** |

### Khi nào dùng Con trỏ, khi nào dùng Vector?

**Dùng Con trỏ khi:**
- Cần hiệu năng tối đa
- Làm việc với code C cũ
- Kích thước cố định và biết trước
- Yêu cầu cụ thể của bài toán

**Dùng Vector khi:**
- Code C++ hiện đại (khuyến khích)
- Cần thay đổi kích thước động
- Muốn code an toàn và dễ bảo trì
- Sử dụng các thuật toán STL

### Tóm tắt Vector:
- ✅ Khai báo: `std::vector<int> vec;`
- ✅ Thêm phần tử: `vec.push_back(value);`
- ✅ Truy cập: `vec[i]` hoặc `vec.at(i)`
- ✅ Kích thước: `vec.size()`
- ✅ Tự động giải phóng bộ nhớ - KHÔNG CẦN delete!
- 🎯 **Khuyến khích sử dụng trong C++ hiện đại**
