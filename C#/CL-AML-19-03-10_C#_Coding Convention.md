# C# Coding conventions

## I. Giới thiệu:

### 1. Coding convention là gì?

- Theo wikipedia **Coding convention** là một tập hợp các hướng dẫn cho một ngôn ngữ lập trình cụ thể mà được đề xuất bởi programming styles từ cách đặt tên biến, hàm, class, file, cách bố trí, tổ chức code...
- Trong tài liệu này chúng ta sẽ tập trung vào quy tắc đặt tên và format code.
- Trong tài liệu này sẽ có những từ ngữ chuyên ngành mình xin phép được giữ nguyên tiếng anh.

### 2. Tại sao coding convention lại quan trọng đến thế?

- Theo Robert L. Glass 40% - 80% thời gian trong vòng đời của phần mềm dành cho việc bảo trì.
- Rất hiếm phần mềm được bảo trì bởi chính người viết ra nó.
- Việc tuân thủ theo coding convetion giúp cho các lập trình viên mới tiếp xúc với dự án có thể hiểu code nhanh hơn.
- Việc tuân thủ theo coding convention giúp giảm thiểu chi phí bảo trì phần mềm.

## II. Code standards and naming conventions in C#.

Một `Identifier` là tên mà bạn gán cho một `type`(class, interface, struct, record, delegate, hoặc enum), member, variable, hoặc namespace.

### 1. Quy tắc đặt tên:

Các `Identifier` phải tuân theo các quy tắc sau:

- Các `Identifier` phải bắt đầu băng chữ hoặc ký tự dấu gạch dưới (`_`)
- Các `Identifier` có thể chứa các ký tự Unicode, decimal digit characters, Unicode combining characters, Unicode formatting characters. Để biết thêm thông tin về các danh mục Unicode xem thêm tại [Unicode Category Table](https://www.unicode.org/reports/tr44/). Bạn có thể khai báo `Identifier` trùng với keyword của C# bằng cách thêm tiền tố `@`.

### 2. Quy ước đặt tên:

Ngoài quy tắc đạt tên, có rất nhiều các quy ước về đặt tên được sử dụng trong các API .Net. Theo quy ước, chương trình C# sử dụng `PascalCase` cho type names, namespace, và tất cả các public members. Ngoài ra các quy ước sau đây là phổ biến:

- `Interface` bắt đầu với ký tự `I`.
- `Attribute types` kết thúc với từ `Attribute`.
- `Enum types` sử dụng danh từ số ít cho none-flag, và danh từ số nhiều cho flags.
- `Identifier` không nên chứa 2 ký tự gạch dưới (`_`) liên tiếp.

#### 2.1 Naming guidelines.

| Object Name      | Notation   | Length | Plural | Prefix | Suffix | Abbreviation | Char Mask  | Underscores |
| ---------------- | ---------- | ------ | ------ | ------ | ------ | ------------ | ---------- | ----------- |
| Namespace name   | PascalCase | 128    | Yes    | Yes    | No     | No           | [A-z][0-9] | No          |
| Class name       | PascalCase | 128    | No     | No     | Yes    | No           | [A-z][0-9] | No          |
| Constructor name | PascalCase | 128    | No     | No     | Yes    | No           | [A-z][0-9] | No          |
| Method name      | PascalCase | 128    | Yes    | No     | No     | No           | [A-z][0-9] | No          |
| Method arguments | camelCase  | 128    | Yes    | No     | No     | Yes          | [A-z][0-9] | No          |
| Local variables  | camelCase  | 50     | Yes    | No     | No     | Yes          | [A-z][0-9] | No          |
| Constants name   | PascalCase | 50     | No     | No     | No     | No           | [A-z][0-9] | No          |
| Field name       | camelCase  | 50     | Yes    | No     | No     | Yes          | [A-z][0-9] | Yes         |
| Properties name  | PascalCase | 50     | Yes    | No     | No     | Yes          | [A-z][0-9] | No          |
| Delegate name    | PascalCase | 128    | No     | No     | Yes    | Yes          | [A-z]      | No          |
| Enum type name   | PascalCase | 128    | Yes    | No     | No     | No           | [A-z]      | No          |

##### 2.1.1 Sử dụng `PascalCasing` cho tên class, tên method.

```C#
// ✔️ Good
public class Customer
{
  public void ChangeStatus()
  {
    //...
  }

  public void ChangeAddress()
  {
    //...
  }
}

// ❌ Bad
public class customer
{
  public void changeStatus()
  {
    //...
  }

  public void Changeaddress()
  {
    //...
  }
}
```

> **Why: Dễ đọc và nhất quán với Microsoft's .NET Framework**

<br/>

##### 2.1.2 Sử dụng `camelCasing` cho tham số của method và các biến cục bộ.

```C#
public class UserLog
{
  public void Add(LogEvent logEvent)
  {
    int itemCount = logEvent.Items.Count;
    // ...
  }
}
```

> **Why: Dễ đọc và nhất quán với Microsoft's .NET Framework**

<br/>

##### 2.1.3 Không sử dụng Hungarian notation hoặc bất kỳ loại nhận dạng khác trong identifier.

```C#
// ✔️ Good
int counter;
string name;

// ❌ Bad
int iCounter;
string strName;
```

> **Why: Nhất quán với Microsoft's .NET Framework và các IDE giúp chỉ ra các loại dễ dàng(Thông qua Tooltip). Nhìn chung cần tránh việc đặt các ký hiệu nhận dạng cho identifier**

<br/>

##### 2.1.4 Không sử dụng Screaming Cáp Cho constants hoặc các biến readonly.

```C#
// ✔️ Good
public const string ShippingType = "DropShip";

// ❌ Bad
public const string SHIPPINGTYPE = "DropShip";
```

> **Why: Nhất quán với Microsoft's .NET Framework. Viết hoa toàn bộ khó đọc và đoán nghĩa của biến**

<br/>

##### 2.1.5 Sử dụng tên biến có nghĩa. VD sau đây sử dụng `seattleCustomers` cho khách hàng ở Seattle.

```C#
// ✔️ Good
var seattleCustomers = from customer in customers
  where customer.City == "Seattle"
  select customer.Name;

// ❌ Bad
var query = from customer in customers
  where customer.City == "Seattle"
  select customer.Name;
```

> **Why: Nhất quán với Microsoft's .NET Framework và dễ đọc**

<br/>

##### 2.1.6 Không nên sử dụng các ký tự viết tắt. Ngoại lệ: viết tắt sử dụng trong các tên thông dụng như: Id, Xml, Ftp, Uri.

```C#
// ✔️ Good
UserGroup userGroup;
Assignment employeeAssignment;

// ✔️ Exceptions
CustomerId customerId;
XmlDocument xmlDocument;
FtpHelper ftpHelper;
UriPart uriPart;

// ❌ Bad
UserGroup usrGrp;
Assignment empAssignment;


```

> **Why: Nhất quán với Microsoft's .NET Framework và ngăn chặn viết tắt không nhất quán trong ứng dụng.**

<br/>

##### 2.1.7 Sử dụng PascalCasing hoặc camelCasing (Tuỳ thuộc vào loại identifier) cho các từ viết tắt từ 3 ký tự trở lên (2 ký tự đều viết hoa khi PascalCasing phù hợp hoặc nằm bên trong identifier).

```C#
// ✔️ Good
HtmlHelper htmlHelper;
FtpTransfer ftpTransfer, fastFtpTransfer;
UIControl uiControl, nextUIControl;
```

> **Why: Nhất quán với Microsoft's .NET Framework.**

<br/>

##### 2.1.8 Không sử dụng dấu gạch dưới (`_`). Ngoại lệ khi sử dụng là tiền tố của private fields.

```C#
// ✔️ Good
public DateTime clientAppointment;
public TimeSpan timeLeft;

// ✔️ Exceptions
private DateTime _registrationDate;

// ❌ Bad
public DateTime client_Appointment;
public TimeSpan time_Left;
```

> **Why: Nhất quán với Microsoft's .NET Framework và giúp code dễ đọc hơn**

<br/>

##### 2.1.9 Sử dụng các tên kiểu dữ liệu được định nghĩa trước (C# alias) như `int`, `float`, `string` cho biến cục bộ, tham số và các member declaration. Sử dụng .Net Framework names như `Int32`, `Single`, `String` khi truy cập type's static member như `Int32.TryParse` hoặc `String.Join`

```C#
// ✔️ Good
string firstName;
int lastIndex;
bool isSaved;
string commaSeparatedNames = String.Join(", ", names);
int index = Int32.Parse(input);

// ❌ Bad
String firstName;
Int32 lastIndex;
Boolean isSaved;
string commaSeparatedNames = string.Join(", ", names);
int index = int.Parse(input);
```

> **Why: Nhất quán với Microsoft's .NET Framework và giúp code dễ đọc hơn**

<br/>

##### 2.1.10 Sử dụng `var` để khai bao cho các biến cục bộ. Ngoài lệ các kiểu giữ liệu nguyên thuỷ (int, string, double, ...) sử dụng các tên đã được định nghĩa trước.

```C#
// ✔️ Good
var stream = File.Create(path);
var customers = new Dictionary();

// ✔️ Exceptions
int index = 100;
string timeSheet;
bool isCompleted;
```

> **Why: Loại bỏ sự lộn xộn, đặc biệt với các generic types phức tạp. Type có thể dễ dàng nhận biết bởi tooltips của visual studio.**

<br/>

##### 2.1.11 Sử dụng danh từ hoặc cụm danh từ để đặt tên cho class.

```C#
// ✔️ Good
public class Employee
{
}
public class BusinessLocation
{
}
public class DocumentCollection
{
}
```

> **Why: Nhất quán với Microsoft .Net framework và dễ ghi nhớ.**

<br/>

##### 2.1.12 Sử dụng chữ `I` làm tiền tố cho interface. Tên interface là danh từ, cụm danh từ hoặc tính từ.

```C#
// ✔️ Good
public interface IShape
{
}
public interface IShapeCollection
{
}
public interface IGroupable
{
}
```

> **Why: Nhất quán với Microsoft .Net framework.**

<br/>

##### 2.1.13 Đặt tên source file theo tên của class chính của file đó. Ngoại lệ tên file với partial class phản ánh mục đích của nó VD: designer, generated,...

```C#
// ✔️ Good
// Located in Task.cs
public partial class Task
{
}
// Located in Task.generated.cs
public partial class Task
{
}
```

> **Why: Nhất quán với Microsoft .Net framework. File được sắp xếp theo thứ tự alphabet và các file partial vẫn đứng cạnh các file chính.**

<br/>

##### 2.1.14 Đặt tên các namespace với cấu trúc được định nghĩa rõ ràng.

```C#
// ✔️ Good
namespace Amela.Employee.Api.Controllers
{
}
namespace Amela.Domain.Models
{
}
namespace Amela.Domain.IServices
{
}
namespace Amela.Infrastructure.Services
{
}

// ❌ Bad
namespace Amela
{
}

namespace Services
{
}
```

> **Why: Nhất quán với Microsoft .Net framework. Dễ dàng quản lý code base.**

<br/>

##### 2.1.15 Sử dụng dấu ngoặc nhọn trên dòng mới.

```C#
// ✔️ Good
class Program
{
  static void Main(string[] args)
  {
    //...
  }
}

// ❌ Bad
class Program {
  static void Main(string[] args) {
    //...
  }
}
```

> **Why: Microsoft có một tiêu chuẩn khác nhưng các lập trình viên ưu tiên áp dụng dấu ngoặc nhọn trên dòng mới.**

<br/>

##### 2.1.16 Khai báo tất cả các member variable trên cùng của class, các biến static xếp trước.

```C#
// ✔️ Good
public class Account
{
  public static string BankName;
  public static decimal Reserves;
  public string Number { get; set; }
  public DateTime DateOpened { get; set; }
  public DateTime DateClosed { get; set; }
  public decimal Balance { get; set; }
  // Constructor
  public Account()
  {
    // ...
  }
}

// ❌ Bad
public class Account
{
  // Constructor
  public Account()
  {
    // ...
  }

  public static string BankName;
  public static decimal Reserves;
  public string Number { get; set; }
  public DateTime DateOpened { get; set; }
  public DateTime DateClosed { get; set; }
  public decimal Balance { get; set; }
}
```

> **Why: Quy ước ví trị đặt tên biến hỗ trợ cho quá trình tiềm kiếm biến được dễ dàng hơn.**

<br/>

##### 2.1.17 Sử dụng tên số ít cho enum. Ngoại trừ bit field enum

```C#
// ✔️ Good
public enum Color
{
  Red,
  Green,
  Blue,
  Yellow,
  Magenta,
  Cyan
}

// ✔️ Exception
[Flags]
public enum Dockings
{
  None = 0,
  Top = 1,
  Right = 2,
  Bottom = 4,
  Left = 8
}

// ❌ Bad
public enum Colors
{
  Red,
  Green,
  Blue,
  Yellow,
  Magenta,
  Cyan
}
```

> **Why: Nhất quán với Microsoft .Net Framework và giúp code dễ đọc hơn. Bit field sửa dụng danh từ số nhiều vì có thể chưa nhiều hơn một giá trị (Sử dụng bitwise 'OR')**

<br/>

##### 2.1.18 Không chỉ rõ kiểu dữ liệu hoặc giá trị sử dụng cho enum (Ngoại trừ bit field).

```C#
// ✔️ Good
public enum Direction
{
  North,
  East,
  South,
  West
}

// ❌ Bad
public enum Direction : long
{
  North = 1,
  East = 2,
  South = 3,
  West = 4
}
```

> **Why: Có thể tạo ra sự nhầm lẫn khi dựa vào các kiểu giữ liệu và giá trị.**

<br/>

##### 2.1.19 Không sử dụng hậu tố `Enum` cho tên của kiểu enum.

```C#
// ✔️ Good
public enum Coin
{
  Penny,
  Nickel,
  Dime,
  Quarter,
  Dollar
}

// ❌ Bad
public enum CoinEnum
{
  Penny,
  Nickel,
  Dime,
  Quarter,
  Dollar
}
```

> **Why: Nhất quán với Microsoft .Net Framework và nhất quán với quy tắc trước đó là không type indicator trong indentifier.**

<br/>

##### 2.1.20 Không sử dụng `"Flag"` hoặc `"Flags"` làm hậu tố của tên kiểu enum.

```C#
// ✔️ Good
[Flags]
public enum Dockings
{
  None = 0,
  Top = 1,
  Right = 2,
  Bottom = 4,
  Left = 8
}

// ❌ Bad
[Flags]
public enum DockingsFlags
{
  None = 0,
  Top = 1,
  Right = 2,
  Bottom = 4,
  Left = 8
}
```

> **Why: Nhất quán với Microsoft .Net Framework và nhất quán với quy tắc trước đó là không type indicator trong indentifier.**

<br/>

##### 2.1.21 Sửa dụng hậu tố EventArgs khi tạo mới class chứa thông tin của event.

````C#
// ✔️ Good
public class BarcodeReadEventArgs : System.EventArgs
{
}

> **Why: Nhất quán với Microsoft .Net Framework dễ đọc.**

<br/>

##### 2.1.22 Đặt tên của event handler với hậu tố là `"EventHandler"`  (delegates used as types of events).

``` C#
// ✔️ Good
public delegate void ReadBarcodeEventHandler(object sender, ReadBarcodeEventArgs e);
}
````

> **Why: Nhất quán với Microsoft .Net Framework và dễ đọc.**

<br/>

##### 2.1.23 tên các parameter trong method phải là duy nhất.

```C#
// ✔️ Good
private void MyFunction(string name, string description)
{
  //...
}

// ❌ Bad
private void MyFunction(string name, string Name)
{
  //...
}
```

> **Why: Nhất quán với Microsoft .Net Framework và dễ đọc. Loại trừ khả năng xung đột trong code.**

<br/>

##### 2.1.24 Đặt tên 2 tham số là `sender` và `e` trong event handler. Tham số `sender` đại diện cho object raise lên sự kiên. Thông tường tham số `sender` là kiểu object, ngay cả khi có thể sử dụng một kiểu dữ liệu cụ thể hơn.

```C#
// ✔️ Good
public void ReadBarcodeEventHandler(object sender, ReadBarcodeEventArgs e)
{
  //...
}
```

> **Why: Nhất quán với Microsoft .Net Framework và nhất quán với quy tắc trước đó là không type indicator trong indentifier.**

<br/>

##### 2.1.25 Sử dụng hậu tố `Exception` cho các class exception.

```C#
// ✔️ Good
public class BarcodeReadException : System.Exception
{
}

// ❌ Bad
public class BarcodeRead : System.Exception
{
}
```

> **Why: Nhất quán với Microsoft .Net Framework và dễ đọc.**

<br/>

##### 2.1.26 Sử dụng prefix là Any hoặc Is cho các boolean identifier.

```C#
// ✔️ Good
public static bool IsNullOrEmpty(string value) {
    return (value == null || value.Length == 0);
}

public static bool HaveValue(string value) {
    return (value == null || value.Length == 0);
}

// ❌ Bad
public static bool NullOrEmpty(string value) {
    return (value == null || value.Length == 0);
}
```

> **Why: Nhất quán với Microsoft .Net Framework và dễ đọc.**

<br/>

##### 2.1.27 Sử dụng named argument trong method call.

```C#
// Method
public void DoSomething(string foo, int bar)
{
...
}

// ✔️ Good
DoSomething(foo: "someString", bar: 1);

// ❌ Avoid
DoSomething("someString", 1);
```

> **Why: Nhất quán với Microsoft .Net Framework và dễ đọc. Khi sử dụng named argument chúng ta không cần truyền tham số theo đúng thứ tự.**

<br/>

##### 2.1.28 Quy ước về layout.

Bố cục và formatting code tốt giúp code dễ dọc và maintain hơn. Microsoft example và samples tuân theo các quy tắc sau:

- Viết một statement trên một dòng.
- Viết một khai báo trên một dòng.
- Nếu một câu lệnh trên nhiều dòng nối tiếp nhau mà không tự động thụt lề, thì hãy thụt lề các dòng tiếp theo 1 tab (4 spaces).
- Thêm ít nhất một dòng trống giữa phần khai báo phương thức và thuộc tính.
- Sử dụng dấu ngoặc đơn để làm rõ các mệnh đề trong một biểu thức. Như VD sau:

```C#
if ((val1 > val2) && (val1 > val3))
{
    // Take appropriate action.
}
```

<br/>

##### 2.1.29 Quy ước comment.

- Sử dụng comment ở các dòng riêng biệt, không comment ở cuối dòng code.
- Bắt đầu comment text bằng chữ cái đầu tiền viết hoa.
- Kết thúc comment bằng dấu chấm.
- Thêm vào 1 khoảng trống (Space) giữ comment identifier (`//`) và comment text.
- Không comment đoạn code với cú pháp `/**/`
- Đảm bảo tất cả các member đều có XML comments cung cấp mô tả về hành động của nó.

```C#
/// <summary>
/// Amela customer.
/// </summary>
public class Customer
{
    /// <summary>
    /// Name of customer.
    /// </summary>
    public string Name { get; set; }
}
```

<br/>

##### 2.1.30 Sử dụng string interpolation để nối chuỗi ngắn.

``` C#

// ✔️ Good
string displayName = $"{nameList[n].LastName}, {nameList[n].FirstName}";

// ❌ Avoid
string displayName = nameList[n].LastName + ", " + {nameList[n].FirstName};

```

<br/>

##### 2.1.31 Để thêm chuỗi trong vòng lặp, đặc biệt khi khi làm việc với lượng text lớn, sử dụng object StringBuilder.

``` C#

// ✔️ Good
var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
//Console.WriteLine("tra" + manyPhrases);
```

<br/>

##### 2.1.32 Để thêm chuỗi trong vòng lặp, đặc biệt khi khi làm việc với lượng text lớn, sử dụng object StringBuilder.

``` C#

// ✔️ Good
var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
//Console.WriteLine("tra" + manyPhrases);
```

<br/>

##### 2.1.33 Sử dụng `int` thay vì unsign int.

``` C#

// ✔️ Good
var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
//Console.WriteLine("tra" + manyPhrases);
```

<br/>

##### 2.1.34 Array sử dụng cú pháp ngắn gọn để khởi tạo mảng, lưu ý không thể sử dụng `var` thay cho `string[]`.

``` C#

// ✔️ Good
string[] vowels1 = { "a", "e", "i", "o", "u" };
var vowels2 = new string[] { "a", "e", "i", "o", "u" };
```

<br/>

##### 2.1.35 Sử dụng `Func<>` và `Action<>` thay vì định nghĩa delegate type.

``` C#
// Define delegate method.
public static Action<string> ActionExample1 = x => Console.WriteLine($"x is: {x}");

public static Action<string, string> ActionExample2 = (x, y) => 
    Console.WriteLine($"x is: {x}, y is {y}");

public static Func<string, int> FuncExample1 = x => Convert.ToInt32(x);

public static Func<int, int, int> FuncExample2 = (x, y) => x + y;

// Call the method using the signature defined by the Func<> or Action<> delegate.
ActionExample1("string for x");

ActionExample2("string for x", "string for y");

Console.WriteLine($"The value is {FuncExample1("1")}");

Console.WriteLine($"The sum is {FuncExample2(1, 2)}");

```

Trường hợp muốn tạo instance của delegate type, sử dụng cú phép rút gọn. Trong một class, định nghĩa delegate type và method có chung signature.

``` C#
public delegate void Del(string message);

public static void DelMethod(string str)
{
    Console.WriteLine("DelMethod argument: {0}", str);
}
```

Tạo một thể hiện của delegate type và gọi nó:
``` C#
Del exampleDel2 = DelMethod;
exampleDel2("Hey");
```

khai báo sau đây sử dụng cú pháp đầy đủ:
``` C#
Del exampleDel1 = new Del(DelMethod);
exampleDel1("Hey");
```
<br/>

##### 2.1.36 Sử dụng `try-catch` và using statement trong xử lý exception.
- Sử dụng try-catch cho hầu hết các xử lý ngoại lệ.

``` C#
static string GetValueFromArray(string[] array, int index)
{
    try
    {
        return array[index];
    }
    catch (System.IndexOutOfRangeException ex)
    {
        Console.WriteLine("Index is out of range: {0}", index);
        throw;
    }
}
```

- Sử dụng `using statement` thay vì `try-finally` nếu finally block chỉ xử lý duy nhất việc việc gọi dispost method.

``` C#
Font font1 = new Font("Arial", 10.0f);
try
{
    byte charset = font1.GdiCharSet;
}
finally
{
    if (font1 != null)
    {
        ((IDisposable)font1).Dispose();
    }
}

// Có thể xử lý tương tự như trên bằng cách sử dụng "using"
using (Font font2 = new Font("Arial", 10.0f))
{
    byte charset2 = font2.GdiCharSet;
}

// Có thể sử dụng cú pháp using mới không yêu cầu phải có ngoặc nhọn.
using Font font3 = new Font("Arial", 10.0f);
byte charset3 = font3.GdiCharSet;
```
<br/>



##### 2.1.37 Sử dụng `&&` thay vì `&` `||` thay vì `|` trong các phép so sánh để tránh gặp lỗi và tăng performance.

``` C#

// ✔️ Good
string[] vowels1 = { "a", "e", "i", "o", "u" };
var vowels2 = new string[] { "a", "e", "i", "o", "u" };
```

<br/>

##### 2.1.38 Sử dụng cú pháp của khởi tạo object mới. Cú pháp này bắt đầu từ C# 9.


``` C#

// ✔️ Old
var instance1 = new ExampleClass();

// ✔️ New
ExampleClass instance2 = new();
```

Sử dụng object initialize để đơn giản hoá việc tạo object.

``` C#
// ✔️ Không sử dụng object initialize
var instance4 = new ExampleClass();
instance4.Name = "Desktop";
instance4.ID = 37414;
instance4.Location = "Redmond";
instance4.Age = 2.3;

// ✔️ Sử dụng initialize.
var instance3 = new ExampleClass { Name = "Desktop", ID = 37414,
    Location = "Redmond", Age = 2.3 };    
```
<br/>

##### 2.1.39 Sử dụng cú pháp của khởi tạo object mới. Cú pháp này bắt đầu từ C# 9.


``` C#

// ✔️ Old
var instance1 = new ExampleClass();

// ✔️ New
ExampleClass instance2 = new();
```

Sử dụng object initialize để đơn giản hoá việc tạo object.

``` C#
// ✔️ Không sử dụng object initialize
var instance4 = new ExampleClass();
instance4.Name = "Desktop";
instance4.ID = 37414;
instance4.Location = "Redmond";
instance4.Age = 2.3;

// ✔️ Sử dụng initialize.
var instance3 = new ExampleClass { Name = "Desktop", ID = 37414,
    Location = "Redmond", Age = 2.3 };    
```
<br/>

##### 2.1.40 Nếu định nghĩa event handler mà không cần xoá sau này có thể sử dụng lambda expression.


``` C#

// ✔️ Traditional
public Form1()
{
    this.Click += new EventHandler(Form1_Click);
}

void Form1_Click(object? sender, EventArgs e)
{
    MessageBox.Show(((MouseEventArgs)e).Location.ToString());
}

// ✔️ Using lambda expression.
public Form2()
{
    this.Click += (s, e) =>
        {
            MessageBox.Show(
                ((MouseEventArgs)e).Location.ToString());
        };
}
```

Sử dụng object initialize để đơn giản hoá việc tạo object.

``` C#
// ✔️ Không sử dụng object initialize
var instance4 = new ExampleClass();
instance4.Name = "Desktop";
instance4.ID = 37414;
instance4.Location = "Redmond";
instance4.Age = 2.3;

// ✔️ Sử dụng initialize.
var instance3 = new ExampleClass { Name = "Desktop", ID = 37414,
    Location = "Redmond", Age = 2.3 };    
```
<br/>

