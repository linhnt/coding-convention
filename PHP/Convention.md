# Coding Convention PHP

**1. Constant names should comply with a naming convention**

Name constants phải tuân thủ chuỗi regex sau: ``` ^[A-Z][A-Z0-9]*(_[A-Z0-9]+)*$ ```

<i>Noncompliant Code Example</i>

```
define("const1", true);

class Foo {
  const const2 = "bar";
}

```

<i>Compliant Solution</i>
```
define("CONST1", true);

class Foo {
    const CONST2 = "bar";
}
```

**2. Lines should not be too long**

Việc phải cuộn theo chiều ngang khiến bạn khó có được cái nhìn tổng quan và hiểu nhanh về bất kỳ đoạn mã nào.

**3. Method visibility should be explicitly declared**

Các phương thức của lớp có thể được định nghĩa là ```public```, ```private``` hoặc ```protected```. Các phương thức được khai báo mà không có bất kỳ visibility keyword rõ ràng nào được định nghĩa là ```public```. Để tránh mọi hiểu lầm, visibility phải luôn được khai báo rõ ràng.

<i>Noncompliant Code Example</i>
```
function foo(){...}
```
<i>Compliant Solution</i>
```
public function foo(){...}
```
**4. Source code should comply with formatting standards (PSR2)**

<i>Noncompliant Code Example</i>
```
use FooClass;              // khai báo "use" phải được đặt sau khai báo "namespace" 

namespace Vendor\Package;
use FooClass;              // khai báo "namespace" phải được theo sau bởi một dòng trống
$foo = 1;                  // sau khai báo "use" phải có dòng trống

class ClassA {             // một dấu ngoặc nhọn mở phải ở đầu một dòng mới cho các lớp và hàm
  function my_function(){  // dấu ngoặc nhọn trên dòng sai
    if ($firstThing)       // một dấu ngoặc nhọn mở phải ở cuối dòng cho cấu trúc điều khiển
    {
      ...
    }

    if ($secondThing)    { // phải có chính xác một khoảng trắng giữa dấu ngoặc đơn đóng và dấu ngoặc nhọn mở
      ...
    }

    if($thirdThing) {      // Không tuân thủ; phải có chính xác một khoảng trắng giữa từ khóa cấu trúc điều khiển và dấu ngoặc đơn mở
      ...
    }
    else {                 // Không tuân thủ; dấu đóng ngoặc nhọn và từ khóa "else" (hoặc "catch" hoặc "finally") tiếp theo phải nằm trên cùng một dòng
      ...
    }

    try{                   // Không tuân thủ; phải có chính xác một khoảng trắng giữa từ khóa cấu trúc điều khiển và dấu ngoặc nhọn
      ...
    } catch (Exception $e) {
    }

    analyse( $fruit ) ;    // không được có bất kỳ khoảng trắng nào sau dấu ngoặc đơn mở và trước dấu ngoặc đơn đóng

    for ($i = 0;$i < 10;   $i++) { // phải có chính xác một khoảng trắng sau mỗi dấu ";" trong câu lệnh {{for}}
      ...
    }

    pressJuice($apply ,$orange);    // Không tuân thủ; dấu phẩy phải được theo sau bởi một khoảng trắng và không được đặt trước bất kỳ

    do_something ();       // không được có bất kỳ khoảng trắng nào sau tên phương thức

    foreach ($fruits    as $fruit_key =>     $fruit) {  // trong câu lệnh foreach phải có một khoảng trắng trước và sau từ khóa "as" và toán tử "=>"
      ...
    }
  }
}

class ClassB
extends ParentClass  // tên lớp và từ khóa "extends" / "implements" phải nằm trên cùng một dòng 
{
  ...
}

class ClassC extends ParentClass implements \ArrayAccess, \Countable,
    \Serializable    // danh sách các giao diện đã triển khai phải được thụt lề chính xác 
{

  public function aVeryLongMethodName(ClassTypeHint $arg1, // các đối số trong khai báo phương thức phải được thụt lề chính xác 
    &$arg2, array $arg3 = []) {

    $noArgs_longVars = function () use ($longVar1,         // các đối số trong khai báo hàm phải được thụt lề chính xác 
        $longerVar2,
        $muchLongerVar3
    ) {
      ...
    };

    $foo->bar($longArgument,    // các đối số trong lệnh gọi phương thức phải được thụt lề chính xác 
      $longerArgument,
      $muchLongerArgument);     // dấu ngoặc đơn đóng phải được đặt ở dòng tiếp theo 

    $closureWithArgsAndVars = function($arg1, $arg2)use   ($var1, $var2) {  // khai báo đóng phải được đặt cách nhau một cách chính xác - xem (5)
      ...
    };
  }
}
```
<i>Compliant Solution</i>
```
namespace Vendor\Package; // khai báo "namespace" được theo sau bởi một dòng trống 

use FooClass;             // khai báo "use" được đặt sau khai báo "namespace" 
                          // khai báo "use" được theo sau bởi một dòng trống 
$foo = 1;

class ClassA
{                         // dấu ngoặc nhọn mở nằm ở đầu một dòng mới
  function my_function()
  {                       // dấu ngoặc nhọn mở nằm ở đầu dòng mới của hàm
    if ($firstThing) {    // dấu ngoặc nhọn mở ở cuối dòng cho cấu trúc điều khiển
      ...
    }

    if ($secondThing) {   // ó đúng một khoảng trắng giữa dấu ngoặc đơn đóng và dấu ngoặc nhọn mở
      ...
    }

    if ($thirdThing) {    // có chính xác một khoảng trắng giữa từ khóa cấu trúc điều khiển và dấu ngoặc đơn mở
      ...
    } else {              // dấu đóng ngoặc nhọn và từ khóa "else" (hoặc "catch" hoặc "finally") tiếp theo nằm trên cùng một dòng
      ...
    }

    try {                 // có đúng một khoảng trống giữa từ khóa cấu trúc điều khiển và dấu ngoặc nhọn 
      ...
    } catch (Exception $e) {
      ...
    }

    analyse($fruit);      // không có khoảng trắng sau dấu ngoặc đơn mở và trước dấu ngoặc đơn đóng

    for ($i = 0; $i < 10; $i++) { // có đúng một khoảng trắng sau mỗi dấu ";" trong câu lệnh {{for}}
      ...
    }

    pressJuice($apply, $orange);   // Tuân thủ; dấu phẩy được theo sau bởi một khoảng trắng và không được đặt trước bởi bất kỳ

    do_something();       // không có khoảng trắng sau tên phương thức

    foreach ($fruits as $fruit_key => $fruit) {  // trong câu lệnh foreach có một khoảng trắng trước và sau từ khóa "as" và toán tử "=>"
      ...
    }
  }
}

/* The idea here is to make it obvious at first glance that a class extends
 * some other classes and/or implements some interfaces. The names of
 * extended classes or implemented interfaces can be located on subsequent lines.
 */
class ClassB1 extends ParentClass // tên lớp và từ khóa "extends" (hoặc "implements") nằm trên cùng một dòng
{
  ...
}

class ClassB2 extends             // tên lớp và từ khóa "extends" (hoặc "implements") nằm trên cùng một dòng
ParentClass {
  ...
}

/* Lists of implements may be split across multiple lines, where each subsequent line
 * is indented once. When doing so, the first item in the list should be on the next line,
 * and there should be only one interface per line.
 */
class ClassC extends ParentClass implements
    \ArrayAccess,         //  danh sách các giao diện đã triển khai được thụt lề chính xác
    \Countable,
    \Serializable
{
  /* Argument lists may be split across multiple lines, where each subsequent line
   * is indented once. When doing so, the first item in the list should be on the next line,
   * and there should be only one argument per line. Also, when the argument list is
   * split across multiple lines, the closing parenthesis and opening brace should be
   * placed together on their own line with one space between them.
   */
  public function aVeryLongMethodName(
    ClassTypeHint $arg1,  // các đối số trong khai báo phương thức/hàm được thụt lề chính xác
      &$arg2,
      array $arg3 = []
    ) {
      $noArgs_longVars = function () use (
        $longVar1,        // các đối số trong khai báo phương thức/hàm được thụt lề chính xác 
        $longerVar2,
        $muchLongerVar3
      ) {
        ...
      };


    /* Argument lists may be split across multiple lines, where each subsequent line is
     * indented once. When doing so, the first item in the list should be on the next line,
     * and there should be only one argument per line.
     */
    $foo->bar(
      $longArgument,       // các đối số trong lệnh gọi phương thức được thụt lề chính xác 
      $longerArgument,
      $muchLongerArgument
    );                     // dấu ngoặc đơn đóng được đặt trên một dòng riêng biệt 

    /* Closures should be declared with a space after the "function" keyword,
     * and a space before and after the "use" keyword.
     */
    $closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) { // Compliant; the closure declaration is correctly spaced
      ...
    };
  }
}
```
**5. "elseif" keyword should be used in place of "else if" keywords**

Theo tiêu chuẩn mã hóa PSR2

<i>Noncompliant Code Example</i>
```
if ($expr1) {
  ...
} else if ($expr2) {
  ...
} else {...}
```
<i>Compliant Solution</i>
```
if ($expr1) {
  ...
} elseif ($expr2) {
  ...
} else {...}
```

**6. PHP keywords and constants "true", "false", "null" should be lower case**

Việc sử dụng tùy tiện chữ thường hoặc chữ hoa cho các từ khóa và hằng PHP "true", "false" và "null" có thể ảnh hưởng đến khả năng đọc của mã nguồn PHP.

<i>Noncompliant Code Example</i>
```
<?php ECHO 'Hello World'; ?>
```
<i>Compliant Solution</i>
```
<?php echo 'Hello World'; ?>
```

**7. More than one property should not be declared per statement**

Để dễ đọc hơn, không đặt nhiều khai báo thuộc tính trong cùng một câu lệnh.

<i>Noncompliant Code Example</i>
```
<?php
class Foo
{
   private $bar = 1, $bar2 = 2;
}
```
<i>Compliant Solution</i>
```
<?php
class Foo
{
   private $bar1 = 1;
   private $bar2 = 2;
}
```

**8. The "var" keyword should not be used**

Phương thức khai báo một biến trong PHP 4, sử dụng từ khóa var, không được dùng trong các phiên bản đầu tiên của PHP 5. Mặc dù nó không được coi là không dùng nữa trong các phiên bản gần đây nhất, nhưng nó vẫn không phải là cách tốt nhất để sử dụng nó. Khi var xuất hiện, nó được hiểu là từ đồng nghĩa với public và được xử lý như vậy. Do đó, công khai nên được sử dụng thay thế.

<i>Noncompliant Code Example</i>
```
<?php
class Foo
{
    var $bar = 1;
}
```
<i>Compliant Solution</i>
```
<?php
class Foo
{
    public $bar = 1;
}
```


**9. "<?php" and "<?=" tags should be used**

Các quy ước mã hóa cho phép các nhóm cộng tác hiệu quả. Để chuẩn hóa và dễ đọc tối đa, mã PHP nên sử dụng các thẻ <?php ?> dài hoặc các thẻ <?= ?> ngắn; nó không nên sử dụng các biến thể thẻ khác.

<i>Noncompliant Code Example</i>
```
<?
$foo = 1;
?>
```
<i>Compliant Solution</i>
```
<?php
$foo = 1;
?>
```

**10. Local variable and function parameter names should comply with a naming convention**

Các quy ước đặt tên được chia sẻ cho phép các nhóm cộng tác hiệu quả. Quy tắc này gây ra sự cố khi một biến cục bộ hoặc tên tham số hàm không khớp với biểu thức chính quy được cung cấp.
Với biểu thức chính quy mặc định ```^[a-z][a-zA-Z0-9]*$```:

<i>Noncompliant Code Example</i>
```
public function doSomething($my_param){
  $LOCAL;
  ...
}
```
<i>Compliant Solution</i>
```
public function doSomething($myParam){
  $local;
  ...
}
```

**11. Field names should comply with a naming convention**

Chia sẻ một số quy ước đặt tên là điểm mấu chốt giúp nhóm có thể cộng tác hiệu quả. Quy tắc này cho phép kiểm tra xem tên trường có khớp với biểu thức chính quy được cung cấp hay không.
Với biểu thức chính quy mặc định ```^[a-z][a-zA-Z0-9]*$```:

<i>Noncompliant Code Example</i>
```
class MyClass {
  $my_field;
}
```
<i>Compliant Solution</i>
```
class MyClass {
  $myField;
}
```

**12. Interface names should comply with a naming convention**

Chia sẻ một số quy ước đặt tên là điểm mấu chốt giúp nhóm có thể cộng tác hiệu quả. Quy tắc này cho phép kiểm tra xem tất cả các tên giao diện có khớp với một biểu thức chính quy được cung cấp hay không.
Với biểu thức chính quy mặc định ```^[a-z][a-zA-Z0-9]*$```:

<i>Noncompliant Code Example</i>
```
interface myInterface {...} // Noncompliant
```
<i>Compliant Solution</i>
```
interface MyInterface {...}
```

**13. Lines should not end with trailing whitespaces**

Các khoảng trắng ở cuối đơn giản là vô ích và không nên ở trong mã. Chúng có thể tạo ra tiếng ồn khi so sánh các phiên bản khác nhau của cùng một tệp.

**14. Files should contain an empty newline at the end**

Một số công cụ hoạt động tốt hơn khi tệp kết thúc bằng một dòng trống.
For example, a Git diff looks like this if the empty line is missing at the end of the file:
```
+class Test {
+}
\ No newline at end of file
```

**15. A close curly brace should be located at the beginning of a line**

Các quy ước viết mã được chia sẻ giúp nhóm có thể cộng tác hiệu quả. Quy tắc này bắt buộc phải đặt dấu ngoặc nhọn đóng ở đầu dòng

<i>Noncompliant Code Example</i>
```
if(condition) {
  doSomething();}
```
<i>Compliant Solution</i>
```
if(condition) {
  doSomething();
}
```
<i>Exceptions</i>
```
if(condition) {doSomething();}
```

**16. Class names should comply with a naming convention**

Các quy ước mã hóa được chia sẻ cho phép các nhóm cộng tác hiệu quả. Quy tắc này cho phép kiểm tra xem tất cả các tên lớp có khớp với một biểu thức chính quy được cung cấp hay không.
Với biểu thức chính quy được cung cấp mặc định ``` ^[A-Z][a-zA-Z0-9]*$ ```

<i>Noncompliant Code Example</i>
```
class my_class {...}
```
<i>Compliant Solution</i>
```
class MyClass {...}
```

**17. "global" should not be used**

Các biến toàn cục là một cấu trúc hữu ích, nhưng chúng không nên bị lạm dụng. Các hàm có thể truy cập phạm vi toàn cầu thông qua từ khóa toàn cầu hoặc thông qua mảng $GLOBALS, nhưng những thực tiễn này làm giảm đáng kể khả năng đọc và khả năng sử dụng lại của hàm. Thay vào đó, biến toàn cục sẽ được truyền dưới dạng tham số cho hàm.

<i>Noncompliant Code Example</i>
```
$myGlobalVariable;

function foo()
{
  global $myGlobalVariable; // Noncompliant
  $GLOBALS['myGlobalVariable']; // Noncompliant
  // ...
}
```
<i>Compliant Solution</i>
```
function foo($myStateVariable)
{
  // ...
}
```

**18. The names of methods with boolean return values should start with "is" or "has"**

Các chức năng được đặt tên hay có thể cho phép người dùng mã của bạn hiểu nhanh những gì mong đợi từ chức năng - ngay cả trước khi đọc tài liệu. Để đạt được điều đó, các phương thức trả về thuộc tính boolean nên có tên bắt đầu bằng "is" hoặc "has" thay vì "get".
Note that this rule will only apply to functions that are documented to return a boolean.

<i>Noncompliant Code Example</i>
```
/**
 * @return boolean
 */
public function getFoo() // Noncompliant
{
  return foo;
}
```
<i>Compliant Solution</i>
```
/**
 * @return boolean
 */
public function isFoo()
{
  return true;
}
```

**19. Statements should be on separate lines**

Để dễ đọc hơn, không đặt nhiều hơn một câu lệnh trên một dòng.

<i>Noncompliant Code Example</i>
```
if(someCondition) doSomething();
```
<i>Compliant Solution</i>
```
if(someCondition) {
  doSomething();
}
```
<i>Exceptions</i>
```
$max_comparator = function ($v) { return $v > 2; };           // Compliant
$max_comparator = function ($v) { echo $v; return $v > 2; };  // Noncompliant
```

**20. Colors should be defined in upper case**

Các quy ước mã hóa được chia sẻ cho phép các nhóm cộng tác hiệu quả. Viết màu bằng chữ in hoa làm cho chúng nổi bật, do đó làm cho mã dễ đọc hơn.
Quy tắc này kiểm tra xem các định nghĩa màu thập lục phân có được viết bằng chữ hoa không.

<i>Noncompliant Code Example</i>
```
$white = '#ffffff';  // Noncompliant
$dkgray = '#006400';
$aqua = '#00ffff';  // Noncompliant
```
<i>Compliant Solution</i>
```
$white = '#FFFFFF';  // Compliant
$dkgray = '#006400';
$aqua = '#00FFFF';  // Compliant
```

**21. Comments should not be located at the end of lines of code**

<i>Noncompliant Code Example</i>
```
$a = $b + $c; // This is a trailing comment that can be very very long
```
<i>Compliant Solution</i>
```
// This very long comment is better placed before the line of code
$a = $b + $c;
```

**22. An open curly brace should be located at the beginning of a line**

Các quy ước mã hóa được chia sẻ giúp cộng tác hiệu quả. Quy tắc này bắt buộc phải đặt dấu ngoặc nhọn mở ở đầu dòng.

<i>Noncompliant Code Example</i>
```
function myMethod() {  // Noncompliant
  if(something) {  // Noncompliant
    executeTask();
  } else {  //Noncompliant
    doSomethingElse();
  }
}
```
<i>Compliant Solution</i>
```
function myMethod()
{
  if(something)
  {
    executeTask();
  } else
  {
    doSomethingElse();
  }
}
```

**23. An open curly brace should be located at the end of a line**

Các quy ước đặt tên được chia sẻ cho phép các nhóm cộng tác hiệu quả. Quy tắc này gây ra sự cố khi dấu ngoặc nhọn mở không được đặt ở cuối dòng mã.

<i>Noncompliant Code Example</i>
```
if(condition)
{
  doSomething();
}
```
<i>Compliant Solution</i>
```
if(condition) {
  doSomething();
}
```
<i>Exceptions</i>
```
if(condition) {doSomething();}
```