# Coding convention Java Script

Nguồn tham khảo: https://www.w3schools.com/js/js_conventions.asp

## 1. Đặt tên

**1.1 Tên biến, hằng**

Tên biến viết kiểu camelCase, ví dụ: `myArray`

Tên biến viết bằng tiếng Anh, rõ nghĩa, không đặt tên chung chung

Các biến boolean có dạng [is + tính từ] hoặc [can + động từ] hoặc [has+động từ dạng quá khứ]

Tên hằng số viết kiểu UpperSnakeCase, ví dụ: `CREATE_LABEL`

**1.2 Tên hàm**

Tên hàm viết kiểu camelCase, tên hàm nên là động từ, ví dụ: `onNextStep, onSearchCategory,…`

## 2. Ngữ pháp

Đánh dấu cách bên trái và bên phải các toán tử (=,+,-,\* ...)

```
let x = y + z;
const myArray = ["Volvo", "Saab", "Fiat"];
```

Lùi đầu dòng các khối lệnh bằng dấu cách (2 dấu cách), không dùng dấu tab

Dùng dấu `;` để đánh dấu kết thúc câu lệnh

```
const cars = ["Volvo", "Saab", "Fiat"];

const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
};
```

Mở ngoặc nhọn `{ }` ngay tại cùng dòng với lệnh lặp, gán, if (xem ví dụ trên), không viết dấu `{` ở dòng mới trong các trường hợp này

Tránh dùng biến, hàm toàn cục

Biến nên được gán giá trị khởi tạo khi khai báo

Dùng `const` cho các biến không bị gán lại giá trị, `let` cho các biến cần gán lại được, hạn chế dùng `var`

Dùng `""` thay vì `new String()`

Dùng `0` thay vì `new Number()`

Dùng `false` thay vì `new Boolean()`

Dùng `{}` thay vì `new Object()`

Dùng `[]` thay vì `new Array()`

Dùng `/()/` thay vì `new RegExp()`

Dùng `function (){}` thay vì `new Function()`

Dùng `===` thay vì `==`

Không nên viết các file code và hàm quá dài, con số cụ thể tùy dự án. Khuyến nghị với file là không quá 500 dòng, với hàm là khống quá 30 dòng
