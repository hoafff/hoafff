# README - Diễn giải kiến thức và lời giải Assignment 1 (C)

## 1) Mục tiêu của bộ bài tập

Bộ bài này xoay quanh các chủ đề nền tảng của C:

- chỉ thị tiền xử lý (`#define`, `#include`, ...)
- cách macro hoạt động và lỗi thường gặp do thiếu ngoặc
- ký tự đặc biệt trong chuỗi như `\n`, `\t`, `\\`, `\b`
- nhập/xuất ký tự bằng `getchar()` / `putchar()`
- kiểu dữ liệu cơ bản trong C
- toán tử, độ ưu tiên toán tử
- bitwise, logical, dịch bit
- xử lý chuỗi
- đổi chuỗi hexa sang số nguyên

---

## 2) Dịch yêu cầu từng bài sang tiếng Việt

## Lecture 1

### Bài 1
Xét câu lệnh:

```c
double ans = 18.0 / squared(2+1);
```

Với mỗi phiên bản macro `squared()` bên dưới, hãy cho biết giá trị của `ans`:

```c
#define squared(x) x*x
#define squared(x) (x*x)
#define squared(x) (x)*(x)
#define squared(x) ((x)*(x))
```

### Bài 2
Với mỗi câu lệnh sau, hãy giải thích vì sao nó sai và sửa lại cho đúng:

```c
(a) #include <stdio.h> ;
(b) int function(void arg1) { return arg1-1; }
(c) #define MESSAGE = "Happy new year!"
    puts(MESSAGE);
```

### Bài 3
Viết chương trình đếm số lượng:
- dấu cách (`blank`)
- tab
- xuống dòng (`newline`)

### Bài 4
Viết chương trình sao chép input sang output, nhưng thay mỗi chuỗi gồm một hoặc nhiều dấu cách liên tiếp bằng đúng một dấu cách.

### Bài 5
Viết chương trình sao chép input sang output, nhưng:
- thay mỗi tab bằng `\t`
- thay mỗi backspace bằng `\b`
- thay mỗi dấu `\` bằng `\\`

Mục đích là để nhìn thấy rõ các ký tự đặc biệt.

### Bài 6
Viết chương trình in biểu đồ tần suất xuất hiện của các ký tự trong input.

### Bài 7
Viết chương trình:
- xóa các dấu cách và tab ở cuối mỗi dòng
- xóa hẳn những dòng rỗng

---

## Lecture 2

### Bài 1
Viết chương trình xác định miền giá trị (range) của các kiểu:
- `char`
- `short`
- `int`
- `long`

với cả dạng `signed` và `unsigned`, bằng 2 cách:
1. in ra giá trị từ các header chuẩn
2. tự tính trực tiếp

### Bài 2
Dùng quy tắc độ ưu tiên toán tử để phân tích các biểu thức sau, xác định giá trị biến mà không chạy chương trình. Sau đó viết lại bằng dấu ngoặc để thứ tự thực hiện trở nên rõ ràng.

```c
Assume (x=0xFF33, MASK=0xFF00). Expression: c = x & MASK == 0;
Assume (x=10, y=2, z=2).        Expression: z = y = x++ + ++y * 2;
Assume (x=10, y=4, z=1).        Expression: y >>= x & 0x2 && z;
```

### Bài 3
Kiểm tra các câu lệnh sau có lỗi hay không. Nếu có:
- chỉ ra lỗi
- giải thích vì sao sai

```c
int 2nd value = 10;
alliszero = (x=1) && (y=0);
y = ++x + y; z = z-- > x;
ison = x & MASK == MASK;
```

### Bài 4
Viết một vòng lặp tương đương với vòng `for` đã cho phía trên nhưng không dùng `&&` hoặc `||`.

> Lưu ý: trong file PDF hiện tại, vòng `for` gốc không xuất hiện, nên bài này bị thiếu dữ kiện.

### Bài 5
Viết hàm `htoi(s)` để đổi một chuỗi số hexa sang giá trị số nguyên tương ứng.

Chuỗi có thể có tiền tố:
- `0x`
- `0X`

Ký tự hợp lệ:
- `0` đến `9`
- `a` đến `f`
- `A` đến `F`

---

## 3) Kiến thức nền cần nắm

## 3.1. `#define` là gì?

`#define` là chỉ thị tiền xử lý dùng để thay thế văn bản trước khi chương trình được biên dịch.

Ví dụ:

```c
#define MAX 100
#define PI 3.14159
#define NAME "Hoa"
#define CH 'A'
```

Khi trình tiền xử lý gặp `MAX`, nó sẽ thay bằng `100`.

### Macro có tham số

```c
#define SQUARE(x) ((x) * (x))
```

Dùng:

```c
int a = SQUARE(3 + 1);   // thành ((3 + 1) * (3 + 1))
```

### Quy tắc rất quan trọng
Khi viết macro có tham số:
- phải đặt ngoặc quanh từng tham số
- phải đặt ngoặc quanh toàn bộ biểu thức

Sai:

```c
#define SQUARE(x) x*x
```

Đúng:

```c
#define SQUARE(x) ((x) * (x))
```

---

## 3.2. Một số chỉ thị tiền xử lý thường gặp

### `#include`
Chèn nội dung file header vào chương trình.

```c
#include <stdio.h>
#include "myheader.h"
```

- Dùng `<...>` cho thư viện chuẩn
- Dùng `"..."` cho file tự viết

### `#undef`
Hủy định nghĩa macro.

```c
#define MAX 100
#undef MAX
```

### `#if`, `#ifdef`, `#ifndef`, `#elif`, `#else`, `#endif`
Dùng để biên dịch có điều kiện.

```c
#define DEBUG

#ifdef DEBUG
printf("Dang debug\n");
#endif
```

### `#error`
Báo lỗi ngay ở giai đoạn tiền xử lý.

```c
#ifndef VERSION
#error VERSION chua duoc dinh nghia
#endif
```

### `#pragma`
Chỉ thị phụ thuộc compiler.

```c
#pragma once
```

### `#line`
Đổi số dòng và tên file mà compiler báo lỗi.

---

## 3.3. Escape sequence

Một số ký tự đặc biệt hay gặp:

```c
' '   // dấu cách
'\n'  // xuống dòng
'\t'  // tab
'\\'  // in ra dấu \
'\b'  // backspace
'\"'  // dấu "
'\''  // dấu '
```

Ví dụ:

```c
printf("Hello\nWorld\n");
printf("Cot1\tCot2\n");
printf("In ra dau gach cheo: \\\n");
```

---

## 3.4. Kiểu dữ liệu cơ bản trong C

## Nhóm số nguyên
- `char`
- `short`
- `int`
- `long`
- `long long`
- `signed`
- `unsigned`

Ví dụ:

```c
int a = 10;
unsigned int b = 20;
short s = -3;
```

## Nhóm số thực
- `float`
- `double`
- `long double`

Ví dụ:

```c
float x = 3.14f;
double y = 3.1415926;
```

## Kiểu ký tự
```c
char c = 'A';
```

## Kiểu `void`
Dùng khi:
- hàm không trả về gì
- hàm không nhận tham số
- con trỏ generic: `void *`

Ví dụ:

```c
void hello(void) {
    printf("Xin chao\n");
}
```

---

## 3.5. Kích thước kiểu dữ liệu

Kích thước phụ thuộc hệ thống, nhưng thường gặp:

| Kiểu | Thường gặp |
|---|---:|
| `char` | 1 byte |
| `short` | 2 bytes |
| `int` | 4 bytes |
| `long` | 4 hoặc 8 bytes |
| `long long` | 8 bytes |
| `float` | 4 bytes |
| `double` | 8 bytes |
| `long double` | 8, 12, hoặc 16 bytes |

Dùng `sizeof` để kiểm tra thực tế:

```c
printf("%zu\n", sizeof(int));
printf("%zu\n", sizeof(double));
```

---

## 3.6. Biến, ép kiểu, con trỏ, chuỗi

### Biến
```c
int hm = 2;
```

### Ép kiểu
```c
double x = (double)5 / 2;   // 2.5
```

### Con trỏ
```c
int a = 10;
int *p = &a;
```

- `&a` là địa chỉ của `a`
- `p` là con trỏ trỏ tới `a`
- `*p` là giá trị tại địa chỉ đó

### Mảng ký tự / chuỗi
```c
char hihi[] = "xnn chao";
```

Chuỗi trong C kết thúc bằng ký tự `'\0'`.

---

## 3.7. Độ ưu tiên toán tử - cực kỳ quan trọng

Ví dụ:

```c
c = x & MASK == 0;
```

Không được hiểu là:

```c
c = (x & MASK) == 0;
```

Mà theo độ ưu tiên toán tử, nó được hiểu là:

```c
c = x & (MASK == 0);
```

Đây là nguồn gốc của rất nhiều lỗi khi học C.

---

## 3.8. Input ký tự trong C

Hai hàm rất hay dùng:

```c
int c = getchar();
putchar(c);
```

`getchar()` trả về:
- ký tự đọc được
- hoặc `EOF` khi hết dữ liệu

Mẫu vòng lặp rất phổ biến:

```c
int c;
while ((c = getchar()) != EOF) {
    putchar(c);
}
```

---

## 4) Lời giải chi tiết

## Lecture 1 - Bài 1

Ta xét:

```c
double ans = 18.0 / squared(2+1);
```

### Trường hợp 1
```c
#define squared(x) x*x
```

Thay vào:

```c
18.0 / 2+1*2+1
```

Theo thứ tự ưu tiên:
- `18.0 / 2 = 9`
- `1 * 2 = 2`
- `9 + 2 + 1 = 12`

Kết quả:

```c
ans = 12.0
```

### Trường hợp 2
```c
#define squared(x) (x*x)
```

Thay vào:

```c
18.0 / (2+1*2+1)
```

Trong ngoặc:
- `1*2 = 2`
- `2 + 2 + 1 = 5`

Nên:

```c
ans = 18.0 / 5 = 3.6
```

### Trường hợp 3
```c
#define squared(x) (x)*(x)
```

Thay vào:

```c
18.0 / (2+1) * (2+1)
```

Do `*` và `/` cùng mức ưu tiên, tính từ trái sang phải:

```c
(18.0 / 3) * 3 = 6 * 3 = 18
```

Kết quả:

```c
ans = 18.0
```

### Trường hợp 4
```c
#define squared(x) ((x)*(x))
```

Thay vào:

```c
18.0 / (((2+1)*(2+1)))
```

Ta có:

```c
(2+1)*(2+1) = 9
18.0 / 9 = 2.0
```

Kết quả:

```c
ans = 2.0
```

### Kết luận
- (1) `12.0`
- (2) `3.6`
- (3) `18.0`
- (4) `2.0`

---

## Lecture 1 - Bài 2

### (a)
Sai:

```c
#include <stdio.h> ;
```

Lý do:
- Chỉ thị tiền xử lý không kết thúc bằng dấu `;`

Đúng:

```c
#include <stdio.h>
```

### (b)
Sai:

```c
int function(void arg1) { return arg1 - 1; }
```

Lý do:
- `void` nghĩa là không có tham số
- đã ghi `arg1` thì tham số phải có kiểu cụ thể

Đúng:

```c
int function(int arg1) {
    return arg1 - 1;
}
```

### (c)
Sai:

```c
#define MESSAGE = "Happy new year!"
puts(MESSAGE);
```

Lý do:
- trong `#define` không dùng dấu `=`

Đúng:

```c
#define MESSAGE "Happy new year!"

puts(MESSAGE);
```

---

## Lecture 1 - Bài 3
Đếm số dấu cách, tab, newline:

```c
#include <stdio.h>

int main(void) {
    int c;
    int blanks = 0, tabs = 0, newlines = 0;

    while ((c = getchar()) != EOF) {
        if (c == ' ')
            blanks++;
        else if (c == '\t')
            tabs++;
        else if (c == '\n')
            newlines++;
    }

    printf("Blanks   : %d\n", blanks);
    printf("Tabs     : %d\n", tabs);
    printf("Newlines : %d\n", newlines);

    return 0;
}
```

---

## Lecture 1 - Bài 4
Gộp nhiều dấu cách liên tiếp thành một dấu cách:

```c
#include <stdio.h>

int main(void) {
    int c;
    int prev_blank = 0;

    while ((c = getchar()) != EOF) {
        if (c == ' ') {
            if (!prev_blank) {
                putchar(c);
                prev_blank = 1;
            }
        } else {
            putchar(c);
            prev_blank = 0;
        }
    }

    return 0;
}
```

Ý tưởng:
- nếu gặp dấu cách đầu tiên thì in
- nếu tiếp tục gặp dấu cách nữa thì bỏ qua
- gặp ký tự khác thì in và reset trạng thái

---

## Lecture 1 - Bài 5
Hiển thị tab, backspace, backslash dưới dạng nhìn thấy được:

```c
#include <stdio.h>

int main(void) {
    int c;

    while ((c = getchar()) != EOF) {
        if (c == '\t') {
            putchar('\\');
            putchar('t');
        } else if (c == '\b') {
            putchar('\\');
            putchar('b');
        } else if (c == '\\') {
            putchar('\\');
            putchar('\\');
        } else {
            putchar(c);
        }
    }

    return 0;
}
```

---

## Lecture 1 - Bài 6
In histogram tần suất ký tự:

```c
#include <stdio.h>

int main(void) {
    int c, i;
    int freq[128] = {0};

    while ((c = getchar()) != EOF) {
        if (c >= 0 && c < 128)
            freq[c]++;
    }

    for (i = 0; i < 128; i++) {
        if (freq[i] > 0) {
            if (i == '\n')
                printf("\\n : ");
            else if (i == '\t')
                printf("\\t : ");
            else if (i == ' ')
                printf("' ' : ");
            else if (i >= 32 && i <= 126)
                printf("%c : ", i);
            else
                printf("0x%02X : ", i);

            for (int j = 0; j < freq[i]; j++)
                putchar('*');

            printf(" (%d)\n", freq[i]);
        }
    }

    return 0;
}
```

---

## Lecture 1 - Bài 7
Xóa blank/tab ở cuối dòng và xóa dòng rỗng:

```c
#include <stdio.h>

#define MAXLINE 1000

int main(void) {
    int c, i = 0;
    char line[MAXLINE];

    while ((c = getchar()) != EOF) {
        if (c != '\n' && i < MAXLINE - 1) {
            line[i++] = c;
        } else {
            int end = i - 1;

            while (end >= 0 && (line[end] == ' ' || line[end] == '\t'))
                end--;

            if (end >= 0) {
                for (int k = 0; k <= end; k++)
                    putchar(line[k]);
                putchar('\n');
            }

            i = 0;

            if (c == EOF)
                break;
        }
    }

    if (i > 0) {
        int end = i - 1;

        while (end >= 0 && (line[end] == ' ' || line[end] == '\t'))
            end--;

        if (end >= 0) {
            for (int k = 0; k <= end; k++)
                putchar(line[k]);
            putchar('\n');
        }
    }

    return 0;
}
```

---

## Lecture 2 - Bài 1

### Cách 1: dùng header chuẩn `limits.h`

```c
#include <stdio.h>
#include <limits.h>

int main(void) {
    printf("signed char   : %d to %d\n", SCHAR_MIN, SCHAR_MAX);
    printf("unsigned char : 0 to %u\n", UCHAR_MAX);

    printf("signed short  : %d to %d\n", SHRT_MIN, SHRT_MAX);
    printf("unsigned short: 0 to %u\n", USHRT_MAX);

    printf("signed int    : %d to %d\n", INT_MIN, INT_MAX);
    printf("unsigned int  : 0 to %u\n", UINT_MAX);

    printf("signed long   : %ld to %ld\n", LONG_MIN, LONG_MAX);
    printf("unsigned long : 0 to %lu\n", ULONG_MAX);

    return 0;
}
```

### Cách 2: tự tính trực tiếp

```c
#include <stdio.h>
#include <limits.h>

unsigned long long max_unsigned_bits(int bits) {
    if (bits >= 64)
        return ~0ULL;
    return (1ULL << bits) - 1ULL;
}

void print_range(const char *name, int bits) {
    unsigned long long umax = max_unsigned_bits(bits);
    unsigned long long smax = umax >> 1;
    long long smin = -(long long)smax - 1;

    printf("%-14s signed   : %lld to %lld\n", name, smin, (long long)smax);
    printf("%-14s unsigned : 0 to %llu\n", name, umax);
}

int main(void) {
    print_range("char",  sizeof(char)  * CHAR_BIT);
    print_range("short", sizeof(short) * CHAR_BIT);
    print_range("int",   sizeof(int)   * CHAR_BIT);
    print_range("long",  sizeof(long)  * CHAR_BIT);
    return 0;
}
```

> Ghi chú:
> - `char` thường cần phân biệt thêm `signed char`, `unsigned char`
> - `plain char` có thể signed hoặc unsigned tùy compiler

---

## Lecture 2 - Bài 2

### Câu 1
```c
c = x & MASK == 0;
```

Theo độ ưu tiên toán tử, biểu thức được hiểu là:

```c
c = x & (MASK == 0);
```

Vì:
- `MASK = 0xFF00`
- `MASK == 0` là sai, tức bằng `0`

Nên:

```c
c = x & 0 = 0
```

Kết quả:
- `c = 0`

Nếu ý định ban đầu là kiểm tra `(x & MASK)` có bằng 0 hay không thì phải viết:

```c
c = ((x & MASK) == 0);
```

---

### Câu 2
```c
z = y = x++ + ++y * 2;
```

Nhóm theo độ ưu tiên:

```c
z = (y = ((x++) + ((++y) * 2)));
```

Nếu chỉ xét theo thứ tự ưu tiên:
- `x++` trả về `10`, sau đó `x` thành `11`
- `++y` làm `y` từ `2` thành `3`, rồi dùng giá trị `3`
- `3 * 2 = 6`
- `10 + 6 = 16`
- `y = 16`
- `z = 16`

Kết quả suy luận kiểu "bài tập lớp":
- `x = 11`
- `y = 16`
- `z = 16`

### Nhưng phải biết thêm điều này
Biểu thức này có vấn đề trong C thực tế:
- `y` bị thay đổi bởi `++y`
- rồi lại bị gán bởi `y = ...`
- trong cùng một full-expression

Điều này dẫn tới **undefined behavior**.

Nói ngắn gọn:
- nếu làm bài theo kiểu ưu tiên toán tử: ra `x=11, y=16, z=16`
- nếu xét chuẩn C nghiêm ngặt: biểu thức này không an toàn, kết quả không đáng tin cậy

Cách viết tốt hơn:

```c
x++;
y++;
y = (x - 1) + y * 2;
z = y;
```

---

### Câu 3
```c
y >>= x & 0x2 && z;
```

Theo độ ưu tiên toán tử:

```c
y >>= ((x & 0x2) && z);
```

Với:
- `x = 10` tức `1010`
- `0x2 = 0010`
- `x & 0x2 = 0010`, khác 0, tức true
- `z = 1`, cũng true

Vậy:

```c
((x & 0x2) && z) = 1
```

Nên:

```c
y >>= 1
```

Vì `y = 4`, ta được:

```c
y = 4 >> 1 = 2
```

Kết quả cuối:
- `x = 10`
- `y = 2`
- `z = 1`

---

## Lecture 2 - Bài 3

### 1)
```c
int 2nd value = 10;
```

Sai vì:
- tên biến không được bắt đầu bằng số
- trong tên biến không được có dấu cách

Sửa:

```c
int second_value = 10;
```

hoặc:

```c
int value2 = 10;
```

---

### 2)
```c
alliszero = (x=1) && (y=0);
```

Sai về logic nếu mục tiêu là kiểm tra `x` và `y` có bằng 0 không.

Vì:
- `x=1` là phép gán, không phải so sánh
- `y=0` cũng là phép gán

Biểu thức này sẽ:
- gán `x = 1`
- gán `y = 0`
- rồi tính logic

Nếu muốn kiểm tra:

```c
alliszero = (x == 0) && (y == 0);
```

---

### 3)
```c
y = ++x + y;
z = z-- > x;
```

Dòng đầu:

```c
y = ++x + y;
```

- `x` tăng trước rồi mới dùng
- nếu `x=10, y=3` thì `x` thành `11`, `y = 11 + 3 = 14`

Dòng này không đẹp lắm nhưng vẫn hiểu được.

Dòng sau:

```c
z = z-- > x;
```

Có vấn đề vì:
- `z--` làm thay đổi `z`
- đồng thời lại gán kết quả cho chính `z`

Đây là cách viết gây lỗi logic và có thể dẫn tới undefined behavior.

Nên tách ra rõ ràng:

```c
z--;
z = (z > x);
```

hoặc nếu chỉ muốn kiểm tra:

```c
z = (z > x);
```

---

### 4)
```c
ison = x & MASK == MASK;
```

Theo độ ưu tiên toán tử, biểu thức bị hiểu thành:

```c
ison = x & (MASK == MASK);
```

Vì `MASK == MASK` luôn đúng, tức bằng `1`, nên thành:

```c
ison = x & 1;
```

Đây không phải điều mong muốn.

Nếu muốn kiểm tra 4 bit cuối của `x` đều bằng 1:

```c
ison = ((x & MASK) == MASK);
```

Trong đó:

```c
MASK = 0xF
```

Ví dụ:
- `x = 0x2F` thì 4 bit cuối là `1111`, kết quả đúng
- `x = 0x2D` thì 4 bit cuối là `1101`, kết quả sai

---

## Lecture 2 - Bài 4

Trong PDF hiện tại, bài này bị thiếu vòng `for` gốc, nên không thể giải chính xác 100% nếu bám đúng đề.

Tuy nhiên, bài này rất giống bài kinh điển trong K&R:

```c
for (i = 0; i < lim-1 && (c=getchar()) != '\n' && c != EOF; ++i)
    s[i] = c;
```

Một phiên bản tương đương không dùng `&&` hoặc `||` là:

```c
i = 0;
while (i < lim - 1) {
    c = getchar();

    if (c == '\n')
        break;
    if (c == EOF)
        break;

    s[i] = c;
    ++i;
}
```

Nếu muốn giữ cả ký tự newline:

```c
if (c == '\n') {
    s[i++] = c;
}
s[i] = '\0';
```

---

## Lecture 2 - Bài 5
Hàm đổi chuỗi hexa sang số nguyên:

```c
#include <stdio.h>
#include <ctype.h>

int htoi(const char s[]) {
    int i = 0;
    int result = 0;
    int digit;

    while (isspace((unsigned char)s[i]))
        i++;

    if (s[i] == '0' && (s[i + 1] == 'x' || s[i + 1] == 'X'))
        i += 2;

    for (; s[i] != '\0'; i++) {
        if (s[i] >= '0' && s[i] <= '9')
            digit = s[i] - '0';
        else if (s[i] >= 'a' && s[i] <= 'f')
            digit = s[i] - 'a' + 10;
        else if (s[i] >= 'A' && s[i] <= 'F')
            digit = s[i] - 'A' + 10;
        else
            break;

        result = result * 16 + digit;
    }

    return result;
}

int main(void) {
    printf("%d\n", htoi("0x1A"));   // 26
    printf("%d\n", htoi("FF"));     // 255
    printf("%d\n", htoi("7b"));     // 123
    return 0;
}
```

### Ý tưởng
Mỗi lần đọc 1 chữ số hexa:
- ký tự `'0'..'9'` tương ứng `0..9`
- `'A'..'F'` hoặc `'a'..'f'` tương ứng `10..15`

Mỗi bước:

```c
result = result * 16 + digit;
```

Ví dụ `"1A"`:
- ban đầu `result = 0`
- đọc `'1'`: `result = 0*16 + 1 = 1`
- đọc `'A'`: `result = 1*16 + 10 = 26`

---

## 5) Những lỗi người mới học C hay gặp

1. Viết macro mà không bọc ngoặc
```c
#define SQUARE(x) x*x
```

2. Nhầm `=` với `==`
```c
if (x = 0)   // sai logic
```

3. Không hiểu độ ưu tiên toán tử
```c
x & MASK == 0
```

4. Dùng biến chưa khởi tạo

5. Quên `'\0'` khi xử lý chuỗi

6. Lẫn lộn giữa:
- ký tự: `'A'`
- chuỗi: `"A"`

7. Nhầm giữa:
- địa chỉ: `&a`
- giá trị tại địa chỉ: `*p`

---

## 6) Cách học bộ bài này hiệu quả

Thứ tự nên học:

1. hiểu `#define`, macro, `#include`
2. hiểu `getchar()`, `putchar()`, `EOF`
3. làm chắc `if`, `while`, `for`
4. học escape sequence
5. học bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`
6. luyện operator precedence
7. luyện mảng ký tự và chuỗi

---

## 7) Kết luận ngắn

Nếu phải rút gọn bộ này thành vài ý cốt lõi, thì là:

- Macro trong C chỉ thay thế văn bản, không phải hàm thật
- Thiếu ngoặc trong macro là lỗi cực kỳ phổ biến
- `=` là gán, `==` là so sánh
- Phải rất cẩn thận với độ ưu tiên toán tử
- Xử lý input ký tự bằng `getchar()` là nền tảng rất quan trọng
- Bit masking là kiến thức bắt buộc nếu muốn học C chắc
- Với chuỗi hexa, quy tắc chung là: `result = result * 16 + digit`

---
