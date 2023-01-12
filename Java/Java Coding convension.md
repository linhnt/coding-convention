# 1. Introduction
# 2. File Names
# 3. File Organization
# 4. Indentation
# 5. Comments
# 6. Declarations
# 7. Statements
# 8. White Space
## 8.1 Blank Lines
Blank line cải thiện khả năng đọc qua việc phân cách các đoạn code có liên kết với nhau về logic

Hai blank line nên luôn được sử dụng trong các trường hợp sau đây:
* Giữa các section của source code
* Giữa các định nghĩa class và interface

Một blank line nên luôn được sử dụng trong các trường hợp sau đây:
* Giữa các method
* Giữa các biến cục bộ trong một method và các câu lệnh đầu tiên của method đó
* Trước một khối và các single-line comment
* Giữa các khối xử lý logic bên trong một method để tăng khả năng đọc hiểu

## 8.2 Blank Spaces
Blank space nên được sử dụng trong các trường hợp sau đây:
* Một keyword được theo sau bởi dấu ngoặc đơn nên được cách bởi 1 space. Ví dụ


```
while (true) {
           ...
       }
```

Lưu ý rằng 1 Blank Space không nên được sử dụng giữa tên của một method và dấu mở ngoặc đơn đầu tiên.
* Một blank space nên được xuất hiện sau dấu phẩy trong list các tham số.
* Tất cả các toán tử nhị phân ngoại trừ ```.``` nên được phân cách với toán hạng của chúng bởi các space. Các blank space không bao giờ được tách các toán tử như ("++") và giảm ("--"). Ví dụ:

```
a += c + d;
    a = (a + b) / (c * d);
    
    while (d++ = s++) {
        n++;
    }
    printSize("size is " + foo + "\n");
```
* Các biểu thức trong câu lệnh ```for``` nên được phân tách bởi các dấu space. Ví dụ:
```for (expr1; expr2; expr3)```
* Casts (ép kiểu) nên được theo sau bởi một space. Ví dụ:
```
    myMethod((byte) aNum, (Object) x);
    myMethod((int) (cp + 5), ((int) (i + 3)) 
                                  + 1);
```

# 9. Naming Conventions
Naming conventions giúp chương trình dễ hiểu hơn qua việc làm chúng dễ đọc hơn.
Chúng cũng có thể cung cấp thông tin về các identifier (như là constant, package, class...), từ đó sẽ có ích hơn trong việc hiểu source code

Identifier Type  | Rules for Naming                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Examples
------------- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| -------------
Packages  | Tiền tố của một tên package duy nhất thì luôn được bắt đầu bởi các ký tự ASCII viết thường và nên là một trong nhưng tên miền top-level (như là ```com, edu, gov, mil, net, org```) hoặc là một trong hai ký tự định danh quốc gia được chỉ định trong tiêu chuẩn ISO Standard 3166, 1981.<br/>Các thành phần tiếp theo của tên package thì tùy theo quy ước đặt tên nội bộ của tổ chức.<br/> Package thường được đặt tên giống như đặt tên thư mục trên ổ đĩa tức là sẽ được bắt đầu bằng tên có phạm vi lớn cho đến phạm vi nhỏ dần. Thông tường sẽ đặt tên package với các phạm vi và thứ tự như sau: Tên tổ chức, tên miền → Tên công ty → Tên dự án → Tên module.<br/>Các ký tự trong định danh package là chữ, số in thường. | ```com.sun.eng```<br/>```com.apple.quicktime.v2```<br/>```edu.cmu.cs.bovik.cheese```
Classes | Class name nên là danh từ, trong trường hợp nhiều hơn một từ thì các từ sẽ được mix với nhau bằng cách viết hoa chữ cái đầu tiên của các từ.<br/>Cố gắng đặt tên class đơn giản và có khả năng mô tả, tránh viết tắt, trừ trường hợp các từ viết tắt được sử dụng rộng rãi (ví dụ: URL, HTML, SQL, ...). <br/> Tránh đặt tên trùng với các kiểu dữ liệu đã được định nghĩa sẵn (ví dụ: String, Number, ...)                                                                                                                                                                                                                                                                                                                      |```class Raster;```<br/>```class ImageSprite;```
Interfaces | Tên của interface nên được viết giống như tên class.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | ```interface RasterDelegate;```<br/>```interface Storing;```
Methods | Tên method nên là động từ, được viết theo format camelCase (chữ cái đầu tiên viết thường, trong trường hợp nhiều hơn một từ thì các từ tiếp theo sẽ được mix với nhau bằng cách viết hoa chữ cái đầu tiên)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | ```run();```<br/>```runFast();```<br/>```getBackground();```
Variables | Tên biến được viết theo format camelCase, không nên bắt đầu bởi ký tự underscore (```_```) hoặc dollar (```$```).<br/> Tên biến nên được đặt ngắn gọn nhưng đầy đủ ý nghĩa và mang tính gợi nhớ.<br/> Tránh đặt tên biến chỉ có duy nhất một ký tự, ngoại trừ các biến tạm thời như: ```i```, ```j```, ```k```, ```m```, ```n``` cho kiểu integer, ```c```, ```d```, ```e``` cho kiểu charactor                                                                                                                                                                                                                                                                                                                                                                                          | ```int             i;```<br/><br/>```char            c;```<br/>```float           myWidth;```
Constants | Tên của const nên được viết bằng các ký tự in hoa và phân cách nhau với dấu underscores (```_```). (Nên tránh các hằng số ANSI để dễ debug)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |  ```static final int MIN_WIDTH = 4;```<br/>```static final int MAX_WIDTH = 999;```<br/><br/>```static final int GET_THE_CPU = 1;```

<style>
table th:first-of-type {
    width: 30%;
}
table th:nth-of-type(2) {
    width: 40%;
}
table th:nth-of-type(3) {
    width: 30%;
}
</style>

# 10. Programming Practices
# 11. Code Examples
