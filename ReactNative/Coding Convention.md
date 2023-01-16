# Coding convention ReactNative

## Mục lục

- [Naming](#naming)
  - [Files, Extensions](#files-extensions)
  - [Variables, Constants, Interfaces](#variables-constants-interfaces)
  - [Functions, Methods](#functions-methods)
  - [Projects](#projects)
  - [Branches](#branches)
  - [Commits](#commits)
  - [Pull requests, Merge requests](#pull-requests-merge-requests)
- [Lint](#lint)
  - [Standard references](#standards-references)
  - [Tools](#tools)

## Nguồn tham khảo:

- https://airbnb.io/javascript/react/
- https://github.com/amela-technology/amela-coding-standards
- https://github.com/amela-technology/react-native-templet-v1
- https://eslint.org/docs/latest/rules/

##Naming

#####Files, Extensions

- Do dự án dùng typescript nên các file phải có các đuôi `.ts`, `.tsx`. Tuy nhiên các files nào import export đơn giản thì chỉ cần đuôi `.ts` Còn các files cần tới vòng đời (component life-cycles) hoặc cần import hooks thì phải dùng đuôi `.tsx`.
- Components/Screens/Pages thì đặt tên **PascalCase**. Ví dụ `HomeScreen.tsx`, `HomeTab.tsx`, `StyledButton.tsx`, v.v.
- Các files không phải các trường hợp trên thì dùng **camelCase**. Ví dụ `utils.ts`, `helper.tsx`, v.v.

#####Variables, Constants, Interfaces

- Variables
  - Viết theo **camelCase**, bằng tiếng Anh, rõ nghĩa tường minh.
  - Không đặt tên chung chung như `item`, `index`, `count`, v.v.
  - Boolean thì cần theo 1 trong 3 cấu trúc: **[is + tính từ]**, **[can + động từ]**, **[has + động từ dạng phân từ II]**. Ví dụ: `isChecked`, `canDelete`, `hasBeenAdded`, v.v.
- Constants
  - Kế thừa Variables bên trên.
  - Viết theo **UPPER_SNAKE_CASE**. Ví dụ: `MAX_LENGTH_PASSWORD`, v.v.
- Interfaces
  - Kế thừa Variables bên trên.
  - Cần có tiền tố `I` ở đầu biến.
  - Viết theo kiểu **PascalCase** như `IFormRegister`, v.v.

#####Functions, Methods

- Viết theo **camelCase**, bằng tiếng Anh, rõ nghĩa tường minh.
- Tên phải là 1 hành động.
- Nên bắt đầu bởi 2 từ **on** hoặc **handle**, ví dụ `onChangeText`, `handleSearchPosts`, v.v.

#####Projects

- Tên Projects là tên gọi thường ngày của dự án, hoặc là **mã SKU** của Projects trên Backlog.
- Viết theo lower-case.
- Hậu tố tuỳ vào dạng dự án. **-web**, **-app**, **-api**, **-cms**
- Ví dụ: `test-app`, `test-next-web`, `test-prev-api`, v.v.

#####Branches

- Tên Branches viết theo lower-case.
- Thường có tiền tố bắt đầu từ **feature/**, **fixbug/** hoặc **fix/**, **changerequest/** hoặc **cr/**, **hotfix/**, v.v.
- Hậu tố cần nêu rõ mục đích tạo nhánh, tránh viết quá chung chung như **test**, **change**, v.v.
- Ví dụ: `feature/login-ui`, `fix/api-register-no-error-handle`, `hotfix/bug-message-button`, `cr/add-button-save-video` v.v.

#####Commits

- Theo chuẩn của commitlint-config-conventional. [Xem thêm ở đây.](https://github.com/conventional-changelog/commitlint/tree/master/@commitlint/config-conventional#type-enum)
- Ví dụ: `feat(blog): add comment section`, `fix(server): send cors headers`, v.v.

#####Pull Requests, Merge Requests

- Sẽ có template mỗi khi tạo PR/MR.
- Các phần quan trọng của template gồm:
  - Mục đích của PR/MR.
  - Link backlog của các tasks/bugs/change-requests có liên quan tới PR/MR (nếu có).
  - Phạm vi ảnh hưởng của PR/MR (BugFix, NewFeature, BreakingChange, DocumentUpdate).
  - Screenshots cho thấy sự thay đổi hoặc tạo mới UI (thường là 1 ảnh design kèm với 1 ảnh màn iPhone và 1 màn Android, nếu vội quá có thể chỉ cần ảnh màn iPhone hoặc Android).

##Lint

#####Standard references

- airbnb
- plugin:react/recommend
- plugin:@typescript-eslint/recommended
- plugin:prettier/recommended

#####Tools

- husky
- commitlint/commitizen/cz-conventional-changelog
- eslint
- prettier
