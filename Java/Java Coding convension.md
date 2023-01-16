## Mục lục
### 1. [Introduction](#1-introduction)
1. [Why Have Code Conventions](#11-why-have-code-conventions)
2. [Acknowledgments](#12-acknowledgments)
### 2. [File Names](#2-file-names)
1. [File Suffixes](#21-file-suffixes)
2. [Common File Names](#22-common-file-names)
### 3. [File Organization](#3-file-organization)
1. [Java Source Files](#31-java-source-files)
2. [Beginning Comments](#32-beginning-comments)
3. [Package and Import Statements](#33-package-and-import-statements)
4. [Class and Interface Declarations](#34-class-and-interface-declarations)
### 4. [Indentation](#4-indentation)
1. [Line Length](#41-line-length)
2. [Wrapping Lines](#42-wrapping-lines)
### 5. [Comments](#5-comments)
1. [Implementation Comment Formats](#51-implementation-comment-formats)
2. [Documentation Comments](#52-documentation-comments)
### 6. [Declarations](#6-declarations)
1. [Number Per Line](#61-number-per-line)
2. [Initialization](#62-initialization)
3. [Placement](#63-placement)
4. [Class and Interface Declarations](#64-class-and-interface-declarations)
### 7. [Statements](#7-statements)
1. [Simple Statements](#71-simple-statements)
2. [Compound Statements](#72-compound-statements)
3. [return Statements](#73-return-statements)
4. [if, if-else, if else-if else Statements](#74-if-if-else-if-else-if-else-statements)
5. [for Statements](#75-for-statements)
6. [while Statements](#76-while-statements)
7. [do-while Statements](#77-do-while-statements)
8. [switch Statements](#78-switch-statements)
9. [try-catch Statements](#79-try-catch-statements)
### 8. [White Space](#8-white-space)
1. [Blank Lines](#81-blank-lines)
2. [Blank Spaces](#82-blank-spaces)
### 9. [Naming Conventions](#9-naming-conventions)
### 10. [Programming Practices](#10-programming-practices)
1. [Providing Access to Instance and Class Variables](#101-providing-access-to-instance-and-class-variables)
2. [Referring to Class Variables and Methods](#102-referring-to-class-variables-and-methods)
3. [Constants](#103-constants)
4. [Variable Assignments](#104-variable-assignments)
5. [Miscellaneous Practices](#105-miscellaneous-practices)

<br/><br/><br/><br/><br/>

## 1. Introduction
### 1.1 Why Have Code Conventions
Code conventions là quan trọng đối với lập trình viên bởi các lý do sau:
* 80% chi phí trọn đời của phần mềm là dành cho việc maintain
* Hầu như không có phần mềm nào được maintain bởi chính tác giả tạo ra nó
* Code conventions cải thiện tính dễ đọc của phần mềm, cho phép các kỹ sư hiểu code mới một cách nhanh chóng và đầy đủ
* Nếu source code được coi như sản phẩm nộp hàng thì cần chắc chắn rằng nó được đóng gói một cách cẩn thận và sạch sẽ

### 1.2 Acknowledgments
Tài liệu này phản ánh các tiêu chuẩn coding của ngôn ngữ Java được trình bày trong [Java Language Specification](https://docs.oracle.com/javase/specs/), từ Sun Microsystems, Inc.

## 2. File Names
Phần này liệt kê các hậu tố (sufifx) và tên của file thường được sử dụng
### 2.1 File Suffixes
Java Software sử dụng các file có suffix dưới đây

| File Type     | Suffix   |
|---------------|----------|
| Java source   | `.java`  |
| Java bytecode | `.class` |

### 2.2 Common File Names
Tên tệp thường được sử dụng bao gồm:

| File Name     | Use                                                                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `GNUmakefile` | Tập tin được sử dụng bởi các tiện ích Make GNU, một công cụ được thiết kế để xây dựng các thư viện và các chương trình bằng cách thực hiện mã nguồn, hoặc makefiles; |
| `README`      | Tên file thường được dùng để tóm tắt nội dung của một thư mục cụ thể.                                                                                                |

## 3. File Organization
Các phần trong một file nên được phân tách bởi các dòng trống và các comment để xác định mỗi phần.<br/>
Nên tránh tạo các file quá dài (hơn 2000 lines).<br/>
Ví dụ về chương trình Java được định dạng đúng được viết tại [Java Source File Example](#31-java-source-files)

### 3.1 Java Source Files
Mỗi file source Java thì chỉ chưa duy nhất một public class hoặc interface. Khi các private class hoặc interface liên kết với public class thì có thể đặt chúng vào trong cùng file source với public class.<br/>
Public class nên là class hoặc interface đầu tiên ở trong file source.<br/>

Một file Java source phải có thứ tự như sau:
* Comment bắt đầu
* Các câu lệnh khai báo package và import
* Khai báo Class hoặc interface

### 3.2 Beginning Comments
Tất cả các file source nên bắt đầu bằng comment gồm tên class, thông tin version, ngày tháng và thông tin copyright
```java
/*
 * Classname
 *
 * Version information
 *
 * Date
 *
 * Copyright notice
 */
```

### 3.3 Package and Import Statements
Dòng đầu tiên không phải comment trong hầu hết Java file là một lệnh `package`. Sau đó có thể là các câu lệnh `import`.<br/>
Ví dụ:
```java
package java.awt;
import java.awt.peer.CanvasPeer;
```

### 3.4 Class and Interface Declarations
Table dưới đây mô tả các phần khai báo của một class hoặc interface, tuân theo thứ tự mà chúng sẽ xuất hiện trong Java source file.

| No  | Part of Class/Interface Declaration                                       | Notes                                                                                                                                                                                   |
|-----|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | Class/interface documentation comment (`/**...*/`)                        | Được mô tả tại [3.2 Beginning Comments](#32-beginning-comments)                                                                                                                         |
| 2   | Từ khóa `class` hoặc `interface`                                          |                                                                                                                                                                                         |
| 3   | Class/interface implementation comment (`/*...*/`) (Có thể có hoặc không) | Comment này phải chứa thông tin với phạm vi sử dụng trong toàn class (khác với documentation comment ở trên)                                                                            |
| 4   | Khai báo `static` variables                                               | Đầu tiên là biến có level `public`, sau đó đến `protected`, tiếp theo là `package level` (no access modifier), và cuối cùng là `private`                                                |
| 5   | Khai báo instance variables                                               | Đầu tiên là biến có level `public`, sau đó đến `protected`, tiếp theo là `package level` (no access modifier), và cuối cùng là `private`                                                |
| 6   | Định nghĩa các Constructor                                                |                                                                                                                                                                                         |
| 6   | Định nghĩa các Method                                                     | Các method nên được nhóm theo chức năng hơn là nhóm theo scope hoặc accessibility (ví dụ một private method có thể ở giữa 2 method public). Mục đích là tăng khả năng dễ đọc và dễ hiểu |

## 4. Indentation
Một đơn vị của indentation nên được dùng tương đương với 4 spaces.

### 4.1 Line Length
Một dòng code không nên quá 120 ký tự.

### 4.2 Wrapping Lines
Khi một câu lệnh không viết đủ trên 1 dòng thì cần ngắt dòng theo các nguyên tắc dưới đây:
* Ngắt dòng sau dấu phẩy
* Ngắt dòng trước toán tử

Ví dụ về ngắt dòng khi gọi method
```java
someMethod(longExpression1, longExpression2, longExpression3,
    longExpression4, longExpression5);
 
var = someMethod1(longExpression1,
        someMethod2(longExpression2,
            longExpression3));
```

Ví dụ ngắt dòng trong biểu thức toán học
```java
longName1 = longName2 * (longName3 + longName4 - longName5) + 4 * longname6; // PREFER
        
longName1 = longName2 * (longName3 + longName4
- longName5) + 4 * longname6; // AVOID
```

Ví dụ ngắt dòng trong biểu thức logic
```java
if ((condition1 && condition2) || (condition3 && condition4)
    ||!(condition5 && condition6)) {
        doSomethingAboutIt();
}
```

Ví dụ về ngắt dòng trong biểu thức toán tử 3 ngôi
```java
alpha = (aShortBooleanExpression) ? beta : gamma;

alpha = (aLongBooleanExpression)
        ? beta
        : gamma;
```

## 5. Comments
Các chương trình Java có thể có hai loại comment là _implementation comments_ và _documentation comments_<br/>
* _Implementation comments_ là chú thích cho các phần implement trong source code và được phân định bởi `/*...*/` hoặc `//`
* _Documentation comments_ (doc comments) là chú thích để mô tả đặc điểm kỹ thuật (của các chức năng, method, class, ...), được phân định bởi `/**...*/`. Doc comment có thể extract thành file HTML bắng cách sử dụng _javadoc tool_

Comment nên dược dùng để cung cấp thông tin tổng quan và thông tin bổ sung mà source code không thể hiện được. Comment chỉ nên chứa thông tin liên quan đến việc đọc hiểu source code<br/>
Comment không nên được đặt trong các hộp lớn được vẽ bằng dấu hoa thị hoặc các ký tự khác.<br/>
Comments không nên bao gồm các ký tự đặc biệt như form-feed ( \ ) và backspace.

### 5.1 Implementation Comment Formats
Có 4 kiểu implementation comment là: block, single-line, trailing, end-of-line

#### 5.1.1 Block Comments
Block comment dùng để mô tả file, method, cấu trúc dữ liệu và giải thuật. Block comment có thể được dùng ở đầu mỗi file hoặc mỗi method.
Chúng cũng có thể được sử dụng ở các vị trí khác như bên trong method. Block comment bên trong function hoặc method thì phải có indent giống với level của source code mà nó đang mô tả.</br>

Một block comment nên được đặt sau một dòng trống để phân biệt với phần code phía trên

```java
/*
 * Here is a block comment.
 */
```

#### 5.1.2 Single-Line Comments
Các comment ngắn có thể để trên một dòng và có level của indent cùng với source code mà nó mô tả. Nếu comment không thể viết trên một dòng thì nên chuyển thành block comment

```java
/* This is a short comment */
```

#### 5.1.3 Trailing Comments
Các comment rất ngắn thì có thể đặt ở cùng với dòng code mà nó mô tả (ở giữa hoặc cuối dòng)

```java
if (a == 2) {
    return isPrime(null /* value */); /* special case */
} else {
    return isPrime(a); /* works only for odd a */
}
```

#### 5.1.4 End-Of-Line Comments
Dấu phân tách `//` có thể comment out cả dòng hoặc một phần dòng code. Nó không nên được dùng trên nhiều dòng liên tiếp để mô tả nội dung cần thể hiện nhưng có thể dùng để comment out nhiều dòng source code

```java
if (foo > 1) { // Do a double-flip.
    ...
}
else {
    return false; // Explain why here.
}

//if (bar > 1) {
//
//    // Do a triple-flip.
//    ...
//}
//else {
//    return false;
//}
```

### 5.2 Documentation Comments
Doc comments mô tả các class, interface, constructor, method và các trường. Mỗi doc comment thì được đặt trong `/**...*/`<br/>
Doc comments không nên đặt trong method hoặc constructor vì Java liên kết doc comments với khai báo đầu tiên sau comment.

Để biết thêm chi tiết, hãy xem [Cách viết nhận xét tài liệu cho Javadoc](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html) bao gồm thông tin về các thẻ (`@return, @param, @see`)

```java
/**
 * The Example class provides ...
 */
public class Example { ...
```

## 6. Declarations
### 6.1 Number Per Line
Mỗi khai báo thì nên viết trên một dòng để có thể thêm comment mô tả.

Ví dụ:
```java
    int level; // indentation level
    int size;  // size of table
```

Không được khai báo các kiểu dữ liệu khác nhau trên cùng một dòng. Ví dụ:

```java
    int foo, fooarray[]; //WRONG!
```

**Lưu ý**: Các ví dụ trên đang sử dụng 1 `space` để phân tách giữa `type` và `tên biến`. Tuy nhiên, cũng có trường hợp sẽ sử dụng `tab` như dưới đây

```java
    int     level;        // indentation level
    int     size;         // size of table
    Object  currentEntry; // currently selected table entry
```

### 6.2 Initialization
Hãy cố gắng khởi tạo giá trị cho biến local tại vị trí mà nó được khai báo. Trường hợp duy nhất không khởi tạo giá trị tại vị trí nó được khai báo là khi biến đó phụ thuộc vào các xử lý tính toán sau đó.

### 6.3 Placement
Đặt các khai báo ở đầu mỗi block (Một block được bao bởi cặp dấu ngoặc nhọn `{` và `}`). Không nên chờ đến khi sử dụng mới khai báo biến vì nó dễ gây nhầm lẫn

```java
    void myMethod() {
        int int1 = 0;     // beginning of method block
    
        if (condition) {
            int int2 = 0; // beginning of "if" block
            ...
        }
}
```

Có một ngoại lệ là đối với các biến `index` trong vòng lặp `for` thì có thể khai báo trong câu lệnh `for`

```java
    for (int i = 0; i < maxLoops; i++) { ... }
```

Không được khai báo biến trùng tên với biến bên trong inner block

```java
    int count;
    ...
    myMethod() {
        if (condition) {
            int count = 0;   // AVOID!
            ...
        }
        ...
    }
```

### 6.4 Class and Interface Declarations
Khi viết code trong Class hoặc Interface thì cần tuần thủ các format rule sau đây:
* Không có space giữa tên method và dấu ngoặc đơn `(` bắt đầu nhóm các tham số của nó
* Dấu mở ngoặc nhọn `{` phải được đặt ở cuối dòng cùng với lệnh khai báo
* Dấu đóng ngoặc nhọn `}` phải đặt riêng một dòng cuối cùng, có indent cùng với level của câu lệnh khai bao. Trừ trường hợp khối lệnh trống thì dấu `}` có thể đặt ngay sau `{`
* Các method được phân tách với nhau bởi một dòng trống

```java
class Sample extends Object {
    int ivar1;
    int ivar2;

    Sample(int i, int j) {
        ivar1 = i;
        ivar2 = j;
    }

    int emptyMethod() {}

    ...
}
```

## 7. Statements
### 7.1 Simple Statements
Mỗi dòng chỉ nên chứa duy nhất một statement. Ví dụ:

```java
    argv++;         // Correct
    
    argc--;         // Correct  
    argv++; argc--; // AVOID!
```

### 7.2 Compound Statements
Compound Statements là các câu lệnh chứa nhiều câu lệnh khác và được bao bởi cặp dấu ngoặc nhọn (`{}`)
* Các câu lệnh bên trong cặp `{}` thì phải có indent lùi vào 1 level so với compound statement
* Dấu mở ngoặc `{` phải ở vị trí cuối cùng của dòng bắt đầu compound statement. Dấu đóng ngoặc `}` thì phải đặt riêng một dòng cuối cùng và có indent bằng level của compound statement

### 7.3 return Statements
Lệnh `return` cùng giá trị thì không nên sử dụng cặp dấu ngoặc tròn, trừ khi chúng làm cho giá trị trả về rõ ràng hơn theo một cách nào đó. Ví dụ:

```java
    return myDisk.size();
    return (size ? size : defaultSize);
```

### 7.4 if, if-else, if else-if else Statements
Các câu lệnh `if-else` nên có form như sau:
```java
    if (condition) {
        statements;
    }
    
    if (condition) {
        statements;
    } else {
        statements;
    }
    
    if (condition) {
        statements;
    } else if (condition) {
        statements;
    } else {
        statements;
    }
```

**Lưu ý:** Lệnh `if` sẽ luôn luôn sử dụng cặp dấu ngoặc nhọn
```java
    if (condition) !statement; //AVOID! THIS OMITS THE BRACES {}
```

### 7.5 for Statements
Câu lệnh `for` nên có form như sau:
```java
    for (initialization; condition; update) {
        statements;
    }
```
Một câu lệnh `for` rỗng nên có form như sau:
```java
    for (initialization; condition; update);
```

### 7.6 while Statements
Câu lệnh `while` nên có form như sau:
```java
    while (condition) {
        statements;
    }
```
Một câu lệnh `while` rỗng nên có form như sau:
```java
    while (condition);
```

### 7.7 do-while Statements
Câu lệnh `do-while` nên có form như sau:
```java
    do {
        statements;
    } while (condition);
```
### 7.8 switch Statements
Câu lệnh `switch` nên có form như sau:
```java
    switch (condition) {
        case ABC:
            statements;
            /* falls through */
        case DEF:
            statements;
            break;
        case XYZ:
            statements;
            break;
        default:
            statements;
            break;
    }
```

* Trường hợp trong mệnh đề `case` không bao gồm lệnh `break` thì tại vị trí của lệnh `break` đó sẽ thêm một comment để mô tả rõ hơn (trong ví dụ trên thì đang comment `/* falls through */`)
* Mọi câu lệnh `switch` đều cần có trường hợp `default`. Lệnh `break` trong default case mặc dù là hơi thừa nhưng nó có thể giúp phòng ngừa lỗi nếu sau này có một `case` mới được thêm vào

### 7.9 try-catch Statements
Câu lệnh `try-catch` nên có form như sau:
```java
    try {
        statements;
    } catch (ExceptionClass e) {
        statements;
    }
```

Câu lệnh `try-catch` cũng có thể bao gồm `finally` để thực thi các lệnh bên trong nó bất kể `try` block đã hoàn thành thành công hay chưa.

```java
    try {
        statements;
    } catch (ExceptionClass e) {
        statements;
    } finally {
        statements;
    }
```

## 8. White Space
### 8.1 Blank Lines

Blank line cải thiện khả năng đọc qua việc phân cách các đoạn code có liên kết với nhau về logic

Hai blank line nên luôn được sử dụng trong các trường hợp sau đây:

* Giữa các section của source code
* Giữa các định nghĩa class và interface

Một blank line nên luôn được sử dụng trong các trường hợp sau đây:

* Giữa các method
* Giữa các biến cục bộ trong một method và các câu lệnh đầu tiên của method đó
* Trước một khối và các single-line comment
* Giữa các khối xử lý logic bên trong một method để tăng khả năng đọc hiểu

### 8.2 Blank Spaces

Blank space nên được sử dụng trong các trường hợp sau đây:

* Một keyword được theo sau bởi dấu ngoặc đơn nên được cách bởi 1 space. Ví dụ

```java
    while (true) {
      ...
    }
```

Lưu ý rằng 1 Blank Space không nên được sử dụng giữa tên của một method và dấu mở ngoặc đơn đầu tiên.

* Một blank space nên được xuất hiện sau dấu phẩy trong list các tham số.
* Tất cả các toán tử nhị phân ngoại trừ ```.``` nên được phân cách với toán hạng của chúng bởi các space. Các blank
  space không bao giờ được tách các toán tử như ("++") và giảm ("--"). Ví dụ:

```java
    a += c + d;
    a = (a + b) / (c * d);

    while (d++ == s++) {
        n++;
    }
    printSize("size is " + foo + "\n");
```

* Các biểu thức trong câu lệnh ```for``` nên được phân tách bởi các dấu space. Ví dụ:

```java
    for(expr1; expr2; expr3)
```

* Casts (ép kiểu) nên được theo sau bởi một space. Ví dụ:

```java
    myMethod((byte) aNum, (Object) x);
    myMethod((int) (cp + 5), ((int) (i + 3)) + 1);
```

## 9. Naming Conventions

Naming conventions giúp chương trình dễ hiểu hơn qua việc làm chúng dễ đọc hơn.
Chúng cũng có thể cung cấp thông tin về các identifier (như là constant, package, class...), từ đó sẽ có ích hơn trong
việc hiểu source code

| Identifier Type | Rules for Naming                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Examples                                                                                                                           |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Packages        | Tiền tố của một tên package duy nhất thì luôn được bắt đầu bởi các ký tự ASCII viết thường và nên là một trong nhưng tên miền top-level (như là ```com, edu, gov, mil, net, org```) hoặc là một trong hai ký tự định danh quốc gia được chỉ định trong tiêu chuẩn **ISO Standard 3166, 1981**.<br/>Các thành phần tiếp theo của tên package thì tùy theo quy ước đặt tên nội bộ của tổ chức.<br/> Package thường được đặt tên giống như đặt tên thư mục trên ổ đĩa tức là sẽ được bắt đầu bằng tên có phạm vi lớn cho đến phạm vi nhỏ dần. Thông tường sẽ đặt tên package với các phạm vi và thứ tự như sau: Tên miền → Tên công ty → Tên dự án → Tên module.<br/>Các ký tự trong định danh package là chữ, số in thường. | ```com.sun.eng```<br/>```com.apple.quicktime.v2```<br/>```edu.cmu.cs.bovik.cheese```                                               |
| Classes         | Class name nên là danh từ, trong trường hợp nhiều hơn một từ thì các từ sẽ được mix với nhau bằng cách viết hoa chữ cái đầu tiên của các từ.<br/>Cố gắng đặt tên class đơn giản và có khả năng mô tả, tránh viết tắt, trừ trường hợp các từ viết tắt được sử dụng rộng rãi (ví dụ: URL, HTML, SQL, ...). <br/> Tránh đặt tên trùng với các kiểu dữ liệu đã được định nghĩa sẵn (ví dụ: String, Number, ...)                                                                                                                                                                                                                                                                                                               | ```class Raster;```<br/>```class ImageSprite;```                                                                                   |
| Interfaces      | Tên của interface nên được viết giống như tên class.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | ```interface RasterDelegate;```<br/>```interface Storing;```                                                                       |
| Methods         | Tên method nên là động từ, được viết theo format camelCase (chữ cái đầu tiên viết thường, trong trường hợp nhiều hơn một từ thì các từ tiếp theo sẽ được mix với nhau bằng cách viết hoa chữ cái đầu tiên)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | ```run();```<br/>```runFast();```<br/>```getBackground();```                                                                       |
| Variables       | Tên biến được viết theo format camelCase, không nên bắt đầu bởi ký tự underscore (`_`) hoặc dollar (`$`).<br/> Tên biến nên được đặt ngắn gọn nhưng đầy đủ ý nghĩa và mang tính gợi nhớ.<br/> Tránh đặt tên biến chỉ có duy nhất một ký tự, ngoại trừ các biến tạm thời như: `i`, `j`, `k`, `m`, `n` cho kiểu integer, `c`, `d`, `e` cho kiểu charactor                                                                                                                                                                                                                                                                                                                                                                   | ```int             i;```<br/><br/>```char            c;```<br/>```float           myWidth;```                                      |
| Constants       | Tên của const nên được viết bằng các ký tự in hoa và phân cách nhau với dấu underscores (`_`). (Nên tránh các hằng số ANSI để dễ debug)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | ```static final int MIN_WIDTH = 4;```<br/>```static final int MAX_WIDTH = 999;```<br/><br/>```static final int GET_THE_CPU = 1;``` |

## 10. Programming Practices
### 10.1 Providing Access to Instance and Class Variables
Không public bất kỳ instance hoặc class variable nào mà không có lý do chính đáng.

### 10.2 Referring to Class Variables and Methods
Không sử dụng 1 instance để access tới biến static hoặc method của class. Thay vào đó hãy sử dụng tên class. Ví dụ:
```java
    classMethod();             //OK
    AClass.classMethod();      //OK
    anObject.classMethod();    //AVOID!
```

### 10.3 Constants
Các giá trị số (hoặc chuỗi) không nên viết trực tiếp (hard code) vào source, thay vào đó hãy tạo các const và sử dụng.
Ngoại trừ các giá trị `-1, 0, 1` thì có thể xuất hiện trong các câu lệnh `for` với vai trò là giá trị của index.

### 10.4 Variable Assignments
* Tránh gán cùng 1 giá trị cho nhiều biến ở cùng 1 statement. Điều đó rất khó để đọc. Ví dụ:
```java
    fooBar.fChar = barFoo.lchar = 'c'; // AVOID!
```

* Không sử dụng toán tử gán ở nơi có thể dễ nhầm lẫn với toán hạng đẳng thức.Ví dụ:
```java
    if (c++ = d++) { // AVOID! (Java disallows)
        ...
    }
```
↓↓↓
```java
    if ((c++ = d++) != 0) {
        ...
    }
```

* Không sử dụng embedded assignments. Ví dụ:
```java
    d = (a = b + c) + r; // AVOID!
```
↓↓↓
```java
    a = b + c;
    d = a + r;
```

### 10.5 Miscellaneous Practices
#### 10.5.1 Returning Values
Cố gắn làm cho cấu trúc chương trình matching với ý định của mình. Ví dụ
```java
    if (booleanExpression) {
        return true;
    } else {
        return false;
    }
```
↓↓↓
```java
    return booleanExpression;
```

Tương tự:
```java
    if (condition) {
        return x;
    } else {
        return y;
    }
```
↓↓↓
```java
    if (condition) {
        return x;
    }
    return y;
```
hoặc
```java
    return (condition ? x : y);
```
