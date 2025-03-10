### C语言核心知识体系（结构化精简版）

---

### 一、基础语法与数据类型
#### 1.1 常量与变量
```c
#define MAX 100        // 宏定义常量（预处理阶段替换）
const int MIN = 0;     // const常量（编译期检查，推荐）
int var = 10;          // 普通变量
```

#### 1.2 数据类型
**整型家族**：
| 类型         | 字节 | 范围             |
| ------------ | ---- | ---------------- |
| char         | 1    | -128~127 / 0~255 |
| unsigned int | 4    | 0~4,294,967,295  |
| long long    | 8    | -9e18~9e18       |

**浮点型**：
```c
float f = 3.14f;      // 4字节，6-7位精度
double d = 3.1415926; // 8字节，15位精度
```

**类型转换规则**：
- 隐式：小类型→大类型（int→double）
- 显式：(目标类型)变量

#### 1.3 运算符与表达式
**特殊运算符**：
```c
// 位运算（效率关键场景）
a ^= b; b ^= a; a ^= b; // 无临时变量交换
unsigned mask = 1 << n; // 位掩码

// 取模应用
last_digit = num % 10;         // 取个位
if(num % 2 == 0) {...}        // 奇偶判断
```

**运算优先级口诀**：
括号 > 单目 > 乘除 > 加减 > 移位 > 关系 > 位 > 逻辑 > 赋值

---

### 二、流程控制结构
#### 2.1 条件分支
```c
// 常量前置防误写
if(5 == var) {...} 

// 多条件规范
if(x >=1 && x <10)  // 正确写法
// NOT if(1 <= x <10)
```

#### 2.2 循环结构
```c
// 文件结束控制循环
while((ch = getchar()) != EOF) {...}

// 位运算优化循环
for(int i=0; i<32; i++) 
   if(num & (1<<i)) {...} // 遍历二进制位
```

---

### 三、复合数据结构
#### 3.1 数组与字符串
**一维数组**：
```c
int arr[5] = {1,2}; // 部分初始化→[1,2,0,0,0]
for(int i=0; i<sizeof(arr)/sizeof(int); i++) {...}
```

**字符数组**：
```c
char str[100];
scanf("%s", str); // 自动补'\0'
// 安全输入：fgets(str, sizeof(str), stdin);
```

**多维数组**：
```c
int matrix[3][4] = {{1,2}, {5}}; // 行优先存储
```

#### 3.2 结构体与联合体
```c
typedef struct {
   int id;
   char name[20];
} Student;

union Data {          // 共享内存空间
   int i;
   float f;
};
```

---

### 四、指针与内存管理
#### 4.1 指针基础
```c
int var = 10;
int *p = &var;      // 指针声明
*p = 20;            // 解引用修改

// 指针运算
int arr[5] = {0};
int *p = arr;
*(p+2) = 5;        // arr[2] = 5
```

#### 4.2 动态内存
```c
int *arr = malloc(10*sizeof(int)); // 堆内存分配
free(arr);                        // 必须手动释放
```

---

### 五、函数与模块化
#### 5.1 函数设计
```c
// 参数传递：值传递 vs 指针传递
void swap(int *a, int *b) {
   int tmp = *a;
   *a = *b;
   *b = tmp;
}
```

#### 5.2 递归应用
```c
int factorial(int n) {
   return (n <=1) ? 1 : n * factorial(n-1);
}
```

---

### 六、文件与标准库
#### 6.1 文件操作
```c
FILE *fp = fopen("data.txt", "r");
if(fp) {
   fscanf(fp, "%d", &num);
   fclose(fp);
}
```

#### 6.2 常用库函数
```c
// 字符串处理
strcpy(dest, src);    // 字符串复制
strcat(dest, src);    // 字符串拼接

// 内存操作
memset(arr, 0, sizeof(arr)); // 内存置零
memcpy(dest, src, sizeof(src)); // 内存复制
```

---

### 七、高级技巧
#### 7.1 位域与压缩存储
```c
struct {
   unsigned flag:1;   // 1位存储
   unsigned code:4;   // 4位存储
} Packet;
```

#### 7.2 函数指针
```c
int (*calc)(int, int) = add; // 指向函数
result = calc(3,5);         // 调用函数
```

---

### 八、调试与优化
#### 8.1 调试技巧
```c
#ifdef DEBUG
   printf("Debug info: x=%d\n", x); // 条件编译
#endif
```

#### 8.2 性能优化
```c
// 循环展开
for(int i=0; i<100; i+=4) {
   process(i);
   process(i+1);
   //... 
}
```

---

### 附录：经典代码模板
#### 快速排序实现
```c
void qsort(int arr[], int l, int r) {
   if(l >= r) return;
   int pivot = partition(arr, l, r);
   qsort(arr, l, pivot-1);
   qsort(arr, pivot+1, r);
}
```

---

本体系通过【概念】→【语法】→【应用场景】→【优化技巧】的递进式结构，帮助构建完整的C语言知识框架。建议配合实际编码练习，重点攻克指针、内存管理和算法实现三大核心领域。