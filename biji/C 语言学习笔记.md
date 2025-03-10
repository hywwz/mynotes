# C 语言学习笔记

## 头文件

| 头文件                | 功能描述                                                     |
| --------------------- | ------------------------------------------------------------ |
| `#include <stdio.h>`  | 标准输入输出库，提供 `printf`、`scanf`、`getchar`、`putchar` 等函数。 |
| `#include <stdlib.h>` | 标准库函数，包含内存分配（`malloc`、`free`）、随机数（`srand`、`rand`）等。 |
| `#include <time.h>`   | 时间处理函数，如 `time()` 用于获取当前时间戳。               |
| `#include <ctype.h>`  | 字符处理函数，如 `isupper`、`tolower`、`isalpha`             |

##### 字符类型检查函数

- `isalpha(int c)`：判断字符 `c` 是否为字母，示例：若 `ch = 'A'`，`isalpha(ch)` 为真。
- `isdigit(int c)`：判断字符 `c` 是否为数字，示例：若 `ch = '5'`，`isdigit(ch)` 为真。
- `isspace(int c)`：判断字符 `c` 是否为空白字符（如空格、制表符等），示例：若 `ch = ' '`，`isspace(ch)` 为真。
- `isupper(int c)`：判断字符 `c` 是否为大写字母，示例：若 `ch = 'B'`，`isupper(ch)` 为真。
- `islower(int c)`：判断字符 `c` 是否为小写字母，示例：若 `ch = 'd'`，`islower(ch)` 为真。
- `ispunct(int c)`：判断字符 `c` 是否为标点符号，示例：若 `ch = '!'`，`ispunct(ch)` 为真。

##### 大小写转换函数

- `toupper(int c)`：将字符 `c` 转换为大写字母，若 `ch = 'b'`，`toupper(ch)` 得 `'B'`。
- `tolower(int c)`：将字符 `c` 转换为小写字母，若 `ch = 'D'`，`tolower(ch)` 得 `'d'`。

## 函数声明

```c
返回类型 函数名(参数类型 参数名1, 参数类型 参数名2, ...) {
    // 函数体
    // 执行一些操作
    return 返回值;  // 如果函数是非 void 类型，则返回一个值
```

## 一、常量与变量

### 1.1 常量前置

- 赋值时，顺序为 `a = 0`，即把 0 赋值给 a。
- 相等关系比较运算时，倒序为 `0 == a`，表示判断 a 是否等于 0。

### 1.2 常量定义方式

#### 1.2.1 `const` 关键字

语法：`const type variable_name = value;`
适用于需要类型检查、作用域控制的常量，尤其是常量可能变为更复杂对象（如数组、结构体）的情况。

#### 1.2.2 `#define` 宏定义

语法：`#define NAME value`
对于常量值（如数字常量、固定的配置信息等），若不需要关心类型且常量不会改变范围，使用 `#define` 较为简洁。

## 二、数据类型

### 2.1 整数类型

| 类型      | 大小（字节） |
| --------- | ------------ |
| char      | 1            |
| short     | 2            |
| int       | 4            |
| long      | 4/8          |
| long long | 8            |



`unsigned` 是类型修饰符，用于修饰整数类型（如 `char`、`short`、`int`、`long`、`long long`），只能存储非负数（0 或正数），能表示的最大值比有符号整数大一倍，默认整数是 `signed`（有符号的），需手动加 `unsigned` 变为无符号数。

### 2.2 浮点型

| 类型        | 大小（字节） |
| ----------- | ------------ |
| float       | 4            |
| double      | 8            |
| long double | 12/16        |

`unsigned` 无法修饰浮点数类型。

### 2.3 隐式类型转换

存储范围小的类型自动转换为存储范围大的类型。

- 整数 + 整数 = 整数
- 整数 + 浮点数 = 浮点数
- 浮点数 + 浮点数 = 浮点数

### 2.4 强制类型转换

示例：`double d = 3.14159; int i = (int)d;` 强制将 double 类型的 d 转换为整数，i 的值为 3。

### 2.5 指针类型

| 指针类型  | 32 位系统大小 | 64 位系统大小 |
| --------- | ------------- | ------------- |
| `int*`    | 4             | 8             |
| `double*` | 4             | 8             |
| `char*`   | 4             | 8             |
| `void*`   | 4             | 8             |

### 2.6 布尔类型

| 类型         | C 语言            | C++ 语言                  |
| ------------ | ----------------- | ------------------------- |
| bool         | `int` (0 或 非 0) | `true`（1），`false`（0） |
| 大小（字节） | 4（等同于 `int`） | 1                         |

## 三、字符与字符串

### 3.1字符与字符串的区别

- 字符用单引号 `'` 括起来，如 `'C'` 表示单个字符 C。
- 字符串用双引号 `"` 括起来，如 `"C"` 表示包含字符 C 和终止符 `\0` 的字符串。
- 比较单个字符时用 `if (T == 'C')`，而非 `if (T == "C")`。

### 3.2大小写转换

c

```c
char a[100];
for (int i = 0; a[i] != '\0'; i++) {
    if (islower(a[i])) a[i] = toupper(a[i]);
    else if (isupper(a[i])) a[i] = tolower(a[i]);
}
```

### 3.3 getchar与putchar

getchar 从标准输入读取一个字符，并返回该字符的 ASCII 值。如果读取到文件结束符（EOF），则返回 EOF。
putchar() 将读取到的字符输出到标准输出。

eg：char c;
      c=getchar();//读取 == scanf (“%d”,&c);
       putchar(c);//输出 == printf(“%d”,c);

但是只能处理单个字符，适合将输入的字符大小写转换。
小写字母的ascll码比对应大写多32
小写转大写：c-=32 大写转小写：c+=32
代码示例：

```c
#include <stdio.h>
int main() {
    char ch;
    while ((ch = getchar()) != EOF) {
        if (ch >= 'a' && ch <= 'z') ch -= 32;
        putchar(ch);
    }
    return 0;
}
```

## 四、运算

### 4.1 加减乘除

- 加 (`+`)、减 (`-`)、乘 (`*`)：整数运算结果为整数，整数与浮点数运算结果为浮点数，浮点数运算结果为浮点数。
- 除 (`/`)：整数相除结果为整数（丢弃小数部分），整数与浮点数相除或浮点数相除结果为浮点数。若要确保除法得到浮点数，可让其中一个数变成浮点数（如 `5.0 / 2`）或使用强制类型转换（如 `(float)5 / 2`）。

### 4.2 取余运算

- 只能用于整数（`int`、`long` 等），不能直接用于浮点数（`float`、`double`）。
- 余数的符号与被除数相同。
- 公式：`a % b = a - (a / b) * b`，其中 `a / b` 取整后再相乘。
- 应用：判断奇偶（`if (n % 2 == 0)`）、循环中构造周期（`for (int i = 0; i < 10; i++) { printf("%d ", i % 3); }`）、取数位（`int last_digit = n % 10`）。

### 4.3 平方与开根

- 平方直接用 `x * x`。
- `pow(x, y)` 计算 x 的 y 次方。
- `sqrt(x)` 计算 x 的平方根。

## 五、数组

### 5.1 数组的基本概念

- 数组是一组相同类型的元素在内存中连续存储的数据结构。
- 特点：元素类型相同、内存连续存储、通过索引（下标）访问（从 0 开始编号）、大小固定（定义时必须指定长度，无法动态扩展）。

### 5.2 一维数组

#### 5.2.1 定义数组

语法：`类型 数组名[大小];` 示例：`int numbers[5];`

#### 5.2.2 数组的初始化

- 可在声明时赋初值，如 `int numbers[5] = {1, 2, 3, 4, 5};`
- 部分初始化，未赋值元素默认为 0，如 `int numbers[5] = {1, 2};` 等价于 `{1, 2, 0, 0, 0}`
- 若初始化时提供全部数据，可省略大小，如 `int numbers[] = {1, 2, 3, 4, 5};` 自动推导大小为 5

#### 5.2.3 访问数组元素

使用 `数组名[索引]` 访问，索引从 0 开始，如 `int numbers[5] = {10, 20, 30, 40, 50}; printf("%d\n", numbers[0]);`

#### 5.2.4 修改数组元素

示例：`int numbers[3] = {1, 2, 3}; numbers[1] = 100;`

#### 5.2.5 遍历数组

使用 for 循环遍历，如：

c

```c
#include <stdio.h>
int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }
    return 0;
}
```

### 5.3 多维数组（以二维数组为例）

#### 5.3.1 定义二维数组

语法：`类型 数组名[行][列];` 示例：`int matrix[2][3];`

#### 5.3.2 二维数组初始化

c

```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

或省略行数：`int matrix[][3] = { {1, 2, 3}, {4, 5, 6} };`

#### 5.3.3 访问二维数组

`printf("%d\n", matrix[0][1]);` 访问第 1 行第 2 列元素

#### 5.3.4 遍历二维数组

c

```c
#include <stdio.h>
int main() {
    int matrix[2][3] = {
        {1, 2, 3},
        {4, 5, 6}
    };
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

### 5.4 数组与指针

####    定义指针

```c
int* p;
```

####     访问和修改变量

int a = 10;
int *p = &a;
*p = 20; // 解引用：获取指针指向的数值，此时 a 的值变为 20

- 数组变量本质上是指向首元素的指针，数组名是首地址

  int numbers[3] = {10, 20, 30};

   printf("%p\n", numbers);

   printf("%p\n", &numbers[0]);`

  

- 指针访问数组

- `int numbers[3] = {10, 20, 30};`

  int *p = numbers; 

  printf("%d\n", *p);

   printf("%d\n", *(p + 1));`

  

- int arr[] = {1, 2, 3, 4, 5};
  int *p = arr; // p 指向数组第一个元素
  for(int i = 0; i < 5; i++){
      printf("%d", *(p + i)); // 得到每一个元素
  }

### 5.5 常见错误

越界访问：`int arr[3] = {1, 2, 3}; printf("%d\n", arr[5]);` 会导致错误，C 语言不会检查数组越界，越界可能导致意外行为。

## 六、条件判断与循环

### 6.1 条件判断书写格式

`else if (1 <= x < 10)` 错误，应拆分成 `1 <= x && x < 10`。

### 6.2 循环语句

#### 6.2.1 `while` 循环

`while (q--)` 是倒计时循环，循环执行 `q` 次，每次执行后 `q` 的值减 1。

`while (n > 0) {`       

 `digit = n % 10;  // 获取最后一位数字`       

 `l += position * digit;  // 计算并加到 l`       

 `n /= 10;  // 去掉最后一位`        

`position++;  // 位号递增`    

`}`

#### 6.2.2 `for` 循环

`for (int i = 1; i <= 8; i++) {`

  `l += (n % 10) * i;  // 获取 n 的最后一位，并与当前位数 i 相乘`   

 `n /= 10;              // 去掉 n 的最后一位 }`

`}`

### 6.2.3 switch语句

1，expression是变量（读取）
2，case后面可以是字母（''）也可以是数字

c

```c
switch (expression) {
    case constant1: /* 代码块 */ break;
    default: /* 默认代码块 */ break;
}
```

### 6.3 退出程序

`break` 只能用于循环语句中，在 `if/else` 中用 `return 0` 提前结束。

## 七、其他常用操作

### 7.1 随机数生成

c

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    srand(time(0));  // 使用当前时间作为种子值，确保每次运行程序时生成不同的随机数序列
    int random_number = rand();  // 生成一个随机数
    printf("生成的随机数: %d\n", random_number);
    int random_number_mod = rand() % 10;  // 生成一个介于 0 和 9 之间的随机整数
    printf("生成的随机整数 (0-9): %d\n", random_number_mod);
    return 0;
}
```

### 7.2 字符处理函数

c

```c
#include <ctype.h>
// 示例：大小写转换
char a[100];
scanf("%s", a);
for (int i = 0; a[i] != '\0'; i++) {
    if (islower(a[i])) a[i] = toupper(a[i]);
    else if (isupper(a[i])) a[i] = tolower(a[i]);
}
```

### 7.3 取模操作

取模（modulo）是一种数学运算，用于得到两个数相除后的**余数**。

- 作用：防止溢出、处理循环和周期性问题。
- 示例：`lastFourDigits = a % 10000;` 取后四位；`n % 10;` 获取最低位数字，`n /= 10;` 去掉最低位数字。
-    // 翻转后四位
      for (i = 0; i < 4; i++) {
          reversed = reversed * 10 + (lastFourDigits % 10);
          lastFourDigits /= 10;
      }

   unsigned int result = (a / 10000) * 10000 + reversed;  // 将翻转后的后四位与剩余部分拼

### 7.4 计算数字位数

#### 7.4.1 通过循环除以 10

c

```c
long long n = 22873289749328;  // 给定的数字
int count = 0；
// 特殊情况：如果数字为0，应该有1位
if (n == 0) {
   count = 1;
} else {
   while (n > 0) {
        count++;
        n /= 10;  // 每次除以10，去掉最低位
   }
}
```

#### 7.4.2 使用对数（log10）

c

```c
#include <math.h>
int count = (int)log10(n) + 1;  // 计算位数
```

#### 7.4.3 将数字转换为字符串

c

```c
#include <stdio.h>
#include <string.h>
long long n = 22873289749328;  // 给定的数字
char str[20];
sprintf(str, "%lld", n);// 将数字转换为字符串
count=strlen(str));//字符长度为数字位数
```

### 7.5 字符串变数字

c

```c
char str[] = "12345";
for (int i = 0; str[i] != '\0'; i++) {
    int digit = str[i] - '0';// 字符转换为数字
    printf("%d ", digit);// 打印每个数字
}
```

### 7.6 异或操作（XOR）

#### 7.6.1 交换两个数不使用临时变量

c

```c
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

#### 7.6.2 在数组中找到唯一的数

c

```c
#include <stdio.h>
int findUnique(int arr[], int size) {
    int res = 0;
    for (int i = 0; i < size; i++) {
        res ^= arr[i];
    }
    return res;
}
```

#### 7.6.3 判断两个数是否相等

`a ^ b == 0` 说明 a 和 b 相等。

### 7.7输入输出

- `printf("%%")` 输出 `%`

- 返回值检查：

  c

  ```c
  if (scanf(" <%d><%c>", &n, &T) != 2) { /* 处理错误 */ }
  ```

### 7.8拼接保留代码示例

```c
// 保存原始学号，以便最后输出
int original = n;

// 输出最终学号（加识别码后的学号）
printf("%d%d\n", original, I);  // 输出原学号和识别码，最终为9位数
```

## 八、代码优化建议

### 1，相同结果条件合并

未给出具体示例，可在实际代码中，将具有相同处理逻辑的条件合并。

### 2，`if - else` 循环优化

如果 `if - else` 语句块中只有一句话，可以不写括号，甚至写在一行；如果有多句，则需要写括号。

### 3，巧用逻辑表达式

使用括号 `()` 包围的表达式通常是逻辑表达式或条件表达式，用于比较两个值，并返回一个布尔值（`true` 或 `false`），`true` 表示为 1，`false` 表示为 0。例如：

c

```c
lucky = (1 == a) + (2 == b) + (3 == c) + (4 == d) + (5 == e) + (6 == f);
```

### 4，预防错误

`scanf` 函数的返回值是成功读取并赋值的输入项数。可以通过检查 `scanf` 的返回值来判断输入格式是否正确。示例：

c

```c
if (scanf(" <%d><%c>", &n, &T) != 2) {
    // 输入格式不正确的处理代码
}
```

### 5，范围限制展示

在进行温度转换等操作时，需要对输入值进行范围检查，超出范围则输出错误信息并终止程序。示例：

c

```c
if (T == 'C') {
    if (n < -273 || n > 1000) {
        // 如果摄氏温度值不在 [-273, 1000] 范围内，输出错误信息并终止程序
        printf("摄氏温度值超出范围，请输入 [-273, 1000] 范围内的值\n");
        return 1; // 返回非零值表示错误
    }
    // 将摄氏温度转换为华氏温度
    float F = (float)(n * 9) / 5 + 32;
    // 输出转换后的温度，保留一位小数
    printf("<%d><%c>=<%.1f><F>", n, T, F);
}
```

## 附录：综合示例

#### 1 判断火仙草数

c

```c
#include <stdio.h>
// 判断一个四位数是否是火仙草数
int jud(int n) {
    int original = n;
    int hou = n % 100;  // 后两位
    n /= 100;  // 去掉后两位
    int qian = n;  // 前两位
    // 判断是否符合火仙草数的条件
    if (hou * hou + qian * qian == original) {
        return original;  // 如果是火仙草数，返回原始数值
    }
    return 0;  // 不是火仙草数，返回 0
}

int main() {
    int n;
    scanf("%d", &n);
    int found = 0;  // 初始化找到了标志
    // 从 n+1 开始，找到第一个火仙草数
    for (int i = n + 1; i <= 9999; i++) {
        if (jud(i) != 0) {  // 如果是火仙草数
            printf("%d\n", i);  // 输出该火仙草数
            found = 1;
            break;  // 找到后立即停止遍历
        }
    }
    // 如果没有找到火仙草数，输出 -1
    if (!found) {
        printf("-1\n");
    }
    return 0;
}
```

#### 2 二进制位运算处理

 1，输入         1，q行数         2，q行组数（遍历循环）             分别两行，一行数字，一行标准，空格      2，将每组数据第一行转换为二进制位（循环），看满足w中的谁（if）存储      3，将存储的数据再转换为十进制    

c

```c
#include <stdio.h>
int main() {
    int q;  // 输入的数据组数
    scanf("%d", &q);  // 读取组数
    while (q--) {  // 遍历每一组数据
        unsigned int a, b;  // 输入的两个非负整数
        int w0, w1, w2, w3;  // 四个运算值
        scanf("%u %u", &a, &b);  // 读取 a 和 b
        scanf("%d %d %d %d", &w0, &w1, &w2, &w3);  // 读取 w0, w1, w2, w3
        unsigned int result = 0;  // 结果初始化为 0
        unsigned int power_of_two = 1;  // 当前位的权值初始化为 1
        // 逐位处理
        for (int j = 0; j < 32; j++) {
            int a_bit = a & 1;  // 取 a 当前最低位
            int b_bit = b & 1;  // 取 b 当前最低位
            // 根据 a_bit 和 b_bit 计算当前位的结果
            if (a_bit == 0 && b_bit == 0) {
                result += w0 * power_of_two;
            } else if (a_bit == 0 && b_bit == 1) {
                result += w1 * power_of_two;
            } else if (a_bit == 1 && b_bit == 0) {
                result += w2 * power_of_two;
            } else if (a_bit == 1 && b_bit == 1) {
                result += w3 * power_of_two;
            }
            // 移动到下一位
            a >>= 1;  // a 右移 1 位
            b >>= 1;  // b 右移 1 位
            power_of_two <<= 1;  // 当前位的权值乘以 2
        }
        printf("%u\n", result);  // 输出当前组的结果
    }
    return 0;
}
```