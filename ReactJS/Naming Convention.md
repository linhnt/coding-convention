# Coding convention ReactJS

Nguồn tham khảo: https://airbnb.io/javascript/react/ và phiên bản cũ của công ty

## 1. Đặt tên

**1.1 Extensions**

Sử dụng đuôi jsx, tsx cho các file Component

**1.2 Tên file**

File component sử dụng PascalCase , không phải component thì viết kiểu camelCase, ví dụ: `ReservationCard.jsx , reservationCardStyle.js`

Tên Component phải trùng với tên file, mỗi Component viết trong 1 file trừ các component dạng StateLess, Pure Component

**1.3 Tên biến, hằng**

Tên biến viết kiểu camelCase, tên component viết kiểu PascalCase ví dụ:

```
import ReservationCard from './ReservationCard';
const reservationItem = <ReservationCard />;
```

Tên biến viết bằng tiếng Anh, rõ nghĩa, không đặt tên chung chung

Các biến boolean có dạng [is + tính từ] hoặc [can + động từ] hoặc [has+động từ dạng quá khứ]

Tên hằng số viết kiểu UpperSnakeCase, ví dụ: `CREATE_LABEL`

**1.4 Tên hàm**

Tên hàm viết kiểu camelCase, tên hàm nên là động từ, ví dụ: `onNextStep, onSearchCategory,…`

**1.5 Tên prop**

Tên prop không nên trùng với các tên thuộc tính mà html, react đã dùng như style, className ...

Tên prop luôn viết dạng camelCase

## 2. Ngữ pháp

Các thẻ image phải có thuộc tính `alt` có nghĩa và có tính mô tả

Các đoạn dùng `map` phải có `key` và không dùng index làm key

```
 // bad
 {todos.map((todo, index) =>
   <Todo
     {...todo}
     key={index}
   />
 )}

 // good
 {todos.map(todo => (
   <Todo
     {...todo}
     key={todo.id}
   />
 ))}
```

Các prop nên khai báo type (bên js thì dùng props-type, bên typescript thì dùng interface)và giá trị default nếu cần

```
// bad
  function SFC({ foo, bar, children }) {
    return <div>{foo}{bar}{children}</div>;
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node,
  };

  // good
  function SFC({ foo, bar, children }) {
    return <div>{foo}{bar}{children}</div>;
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node,
  };
  SFC.defaultProps = {
    bar: '',
    children: null,
  };
```

Chỉ truyền các prop cần thiết

```
  // good
  render() {
    const { irrelevantProp, ...relevantProps  } = this.props;
    return <WrappedComponent {...relevantProps} />
  }

  // bad
  render() {
    return <WrappedComponent {...this.props} />
  }
```

Bọc mã jsx trong ngoặc đơn "()" nếu mã jsx kéo dài trên nhiều dòng

```
// bad
render() {
  return <MyComponent variant="long body" foo="bar">
           <MyChild />
         </MyComponent>;
}

// good
render() {
  return (
    <MyComponent variant="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}

// good, when single line
render() {
  const body = <div>hello</div>;
  return <MyComponent>{body}</MyComponent>;
}
```

Chỉ dùng dấu nháy kép "" cho các prop, các trường hợp khác liên quan đến string đều dùng nháy đơn ' '

```
// bad
<Foo bar='bar' />

// good
<Foo bar="bar" />

// bad
<Foo style= />

// good
<Foo style= />
```

Không nên viết các file code và hàm quá dài, con số cụ thể tùy dự án. Khuyến nghị với file là không quá 500 dòng, với hàm là khống quá 30 dòng code (không tính các dòng jsx và dòng trống)

### 3. LINT

Sử dụng chuẩn ESLint-Prettier

- Check tự động bằng plugin eslint và prettier
- Điều kiện pass : Không còn lỗi warning, error nào ở console khi check coding convension. Cho phép một số trường hợp được đánh ignore

Khuyến khích dùng thêm sonarqube để phân tích smell code
