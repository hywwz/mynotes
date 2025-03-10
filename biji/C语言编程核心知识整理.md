# C语言编程核心知识整理

## 一、基础语法规范

### 1. 常量前置写法
- 赋值操作：`a = 0`（0赋值给a）
- 比较操作：`0 == a`（判断a是否等于0）

### 2. 代码结构规范
```c
// 正确写法
if (x >= 1 && x < 10)  // 复合条件需拆分

// 错误写法
if (1 <= x < 10)       // 错误的条件表达式
```

### 3. 程序退出控制
- break：仅用于跳出循环结构
- return：在函数中提前返回，可终止程序执行

## 二、数据类型详解

### 1. 数值类型
| 类型          | 字节  | 范围/说明       |
| ------------- | ----- | --------------- |
| char          | 1     | -128~127        |
| unsigned char | 1     | 0~255           |
| int           | 4     | -2^31~2^31-1    |
| unsigned int  | 4     | 0~4,294,967,295 |
| float         | 4     | 单精度浮点型    |
| double        | 8     | 双精度浮点型    |
| long double   | 12/16 | 扩展精度浮点型  |

### 2. 类型转换
```c
// 隐式转换（自动提升）
int a = 5;
double b = 3.14;
double c = a + b;  // int自动转double

// 显式转换
double d = 3.14159;
int i = (int)d;    // 强制转换为int
```

### 3. 布尔类型
```c
#include <stdbool.h>
bool flag = true;  // C99标准布尔类型
```

## 三、运算符与表达式

### 1. 算术运算
```c
5 / 2     // 整数除法，结果为2
5.0 / 2   // 浮点除法，结果为2.5
10 % 3    // 取余运算，结果为1
```

### 2. 位运算符
| 运算符 | 说明     | 示例               |
| ------ | -------- | ------------------ |
| &      | 按位与   | 0x0F & 0x3C → 0x0C |
| \|     | 按位或   | 0x0F               |
| ^      | 按位异或 | 0x0F ^ 0x3C → 0x33 |
| ~      | 按位取反 | ~0x00 → 0xFF       |
| <<     | 左移     | 1 << 3 → 8         |
| >>     | 右移     | 8 >> 2 → 2         |

### 3. 特殊运算技巧
```c
// 变量交换（无需临时变量）
a ^= b;
b ^= a;
a ^= b;

// 快速判断奇偶
if (num & 1) { /* 奇数 */ }

// 取末位数字
last_digit = num % 10;
```

## 四、流程控制结构

### 1. 分支结构
```c
// if-else结构
if (score >= 90) {
    printf("A");
} else if (score >= 60) {
    printf("B");
} else {
    printf("C");
}

// switch结构
switch(grade) {
    case 'A': bonus = 1000; break;
    case 'B': bonus = 500;  break;
    default:  bonus = 0;
}
```

### 2. 循环结构
```c
// for循环（固定次数）
for(int i=0; i<10; i++) {
    printf("%d ", i);
}

// while循环（条件控制）
int count = 0;
while(count < 5) {
    printf("Hello");
    count++;
}

// do-while循环（至少执行一次）
do {
    scanf("%d", &num);
} while(num < 0);
```

## 五、数组与字符串

### 1. 数组操作
```c
// 一维数组
int arr[5] = {1,2,3,4,5};
printf("%d", arr[2]);  // 访问第三个元素

// 二维数组
int matrix[2][3] = {{1,2,3}, {4,5,6}};

// 数组遍历
for(int i=0; i<5; i++) {
    arr[i] *= 2;  // 每个元素翻倍
}
```

### 2. 字符处理
```c
// 字符判断与转换
char c = getchar();
if(isupper(c)) c = tolower(c);

// 字符串操作
char str[20] = "Hello";
strcat(str, " World");  // 字符串拼接
printf("Length: %zu", strlen(str));  // 获取长度
```

## 六、指针与内存管理

### 1. 指针基础
```c
int num = 10;
int *p = &num;    // 指针声明
*p = 20;          // 通过指针修改值
printf("%p", p);  // 输出内存地址
```

### 2. 指针与数组
```c
int arr[] = {1,2,3};
int *ptr = arr;       // 指向数组首地址
printf("%d", *(ptr+1));  // 输出第二个元素
```

## 七、函数与模块化

### 1. 函数定义
```c
// 函数声明
int add(int a, int b);

// 函数实现
int add(int a, int b) {
    return a + b;
}
```

### 2. 递归函数
```c
int factorial(int n) {
    if(n <= 1) return 1;
    return n * factorial(n-1);
}
```

## 八、预处理指令

### 1. 宏定义
```c
#define PI 3.14159
#define MAX(a,b) ((a)>(b)?(a):(b))
```

### 2. 文件包含
```c
#include <stdio.h>   // 标准输入输出
#include <stdlib.h>  // 内存管理
#include <math.h>    // 数学函数
```

## 九、实用编程技巧

### 1. 输入验证
```c
int num;
if(scanf("%d", &num) != 1) {
    printf("Invalid input!");
    exit(1);
}
```

### 2. 随机数生成
```c
#include <time.h>
srand(time(0));  // 初始化随机种子
int rand_num = rand() % 100;  // 0-99随机数
```

### 3. 文件操作
```c
FILE *fp = fopen("data.txt", "r");
if(fp == NULL) {
    perror("Error opening file");
    return -1;
}
char buffer[100];
fgets(buffer, 100, fp);
fclose(fp);
```

## 十、调试与优化

### 1. 常见错误处理
- 数组越界访问
- 空指针解引用
- 内存泄漏
- 除零错误

### 2. 调试技巧
```c
#ifdef DEBUG
    printf("Current value: %d\n", var);
#endif
```

本笔记系统整理了C语言核心知识点，可作为快速参考手册。建议配合实际编码练习，通过项目实践加深理解。在编程过程中要注意代码规范和安全问题，养成良好编码习惯。