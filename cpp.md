
# 第二章 变量和基本类型

### 基本内置类型

**基本算数类型**：

| 类型          | 含义           | 最小尺寸                       |
|---------------|----------------|--------------------------------|
| `bool`        | 布尔类型       | 8bits                          |
| `char`        | 字符           | 8bits                          |
| `wchar_t`     | 宽字符         | 16bits                         |
| `char16_t`    | Unicode字符    | 16bits                         |
| `char32_t`    | Unicode字符    | 32bits                         |
| `short`       | 短整型         | 16bits                         |
| `int`         | 整型           | 16bits (在32位机器中是32bits)  |
| `long`        | 长整型         | 32bits                         |
| `long long`   | 长整型         | 64bits （是在C++11中新定义的） |
| `float`       | 单精度浮点数   | 6位有效数字                    |
| `double`      | 双精度浮点数   | 10位有效数字                   |
| `long double` | 扩展精度浮点数 | 10位有效数字                   |

- 大多数机器的字节由8bits组成，字则由32或64bits组成

## 变量
### 变量定义
- 列表初始化
  ```cpp
  int units_sold = 0;
  int units_sold = {0};
  int units_sold{0};
  int units_sold(0);
  ```
- 默认初始化
  * 如果定义变量时没有指定初值，则变量被**默认初始化**
  * 如果是内置类型的变量未被显示初始化，他的值由定义的位置决定
    + 定义于任何函数体之外的变量被初始化为0
    + 定义在函数体内部的内置类型变量将**不被初始化**

### 变量声明和定义的关系
- 为了支持分离式编译，c++将声明和定义区分开来
  * **声明**使得名字为程序所知，一个文件如果想使用别处定义的名字则必须包含对那个名字的声明
  * 而**定义**负责创建与名字关联的实体
```cpp
// 添加extern关键字，声明而非定义
extern int i;  // 声明i而非定义i
int j;        // 声明并定义j
// 任何包含了显示初始化的声明即成为了定义
extern double pi = 3.1416; //定义, 显示初始化抵消了extern
```
- 变量只能被定义一次，但可以被多次声明

### 变量命名规范
1. 需体现实际意义
2. 变量名用小写字母
3. 自定义类名用大写字母开头：`Sales_item`
4. 标识符由多个单词组成，中间须有明确区分：`student_loan`或`studentLoan`，不要用`studentloan`。

### 作用域
- **作用域**是程序的一部分，在其中的名字有特定的含义，c++中大多数作用域都以`{}`分割
- 作用域中一旦声明了某个名字，它所嵌套的作用域中都能访问该名字, 同时允许在内层作用域中重新定义外层作用域已有的名字

## 左值和右值

- **左值**（l-value）**可以**出现在赋值语句的左边或者右边，比如变量；
- **右值**（r-value）**只能**出现在赋值语句的右边，比如常量。

## 复合类型
### 引用
> 一般说的引用是指的左值引用
- **引用**：引用是一个对象的别名，引用类型引用（refer to）另外一种类型。如`int &refVal = val;`。
- 引用必须初始化。
- 引用和它的初始值是**绑定**在一起的，而**不是拷贝**。**一旦定义就不能更改绑定为其他的对象**
- 引用的定义
  ```cpp
  int i = 1024, i2 = 2048
  int &r = i, &r2 = i2
  int &refVal = 10;  // 错误：引用类型的初始值必须是一个对象
  doubel dval = 3.14;
  int &refVal2 = dval;  // 错误：此处引用必须是int型对象
  ```

### 指针
> int *p;
- 是一种`"指向"`另外一种类型的复合类型。
- **定义**指针类型： `int *ip1;`，**从右向左读有助于阅读**，`ip1`是指向`int`类型的指针。
- 指针存放某个对象的**地址**。
- 指针与引用类似，也实现了对其他对象的间接访问, 但指针与引用又有很多不同点
  * 引用本身并非一个对象，引用定义后就不能绑定到其他的对象了；指针并没有此限制，相当于变量一样使用。
  * 指针本身就是一个对象，允许对指针赋值和拷贝
  * 指针无须在定义时赋值

- 获取对象的地址： `int i=42; int *p = &i;`。 `&`是**取地址符**。
- 指针的类型与所指向的对象类型必须一致（均为同一类型int、double等）
- 指针的值的四种状态：
  - 1.指向一个对象；
  - 2.指向紧邻对象的下一个位置；
  - 3.空指针；
  - 4.无效指针。
  - >**对无效指针的操作均会引发错误，第二种和第三种虽为有效的，但理论上是不被允许的**
- 指针访问对象： `cout << *p;`输出p指针所指对象的数据， `*`是**解引用符**。
- 空指针不指向任何对象。使用`int *p=nullptr;`来使用空指针。
- > 赋值语句永远改变的是**左侧**的对象。
- `void*`指针可以存放**任意**对象的地址。因无类型，仅操作内存空间，对所存对象无法访问。
  ```cpp
  double obj = 3.14, *pd = &obj;
  void *pv = &obj;  // obj可以是任意类型的对象
  pv = pd;          // pv可以存放任意类型的指针
  ```
  * 利用`void*`指针做的事情比较有限，可以拿他和别的指针作比较
  * 作为函数的输入或输出
  * 或者赋给另外一个`void*`指针
  * 不能直接操作`void*`指针所指的对象，因为不知道这个对象到底是什么类型

- 其他指针类型必须要与所指对象**严格匹配**。
- 两个指针相减的类型是`ptrdiff_t`。
- 建议：初始化所有指针。
```cpp
int* p1, p2;//*是对p1的修饰，所以p2还是int型
int ival = 1024;
int *pi = &ival;  // pi指向一个int型的数
int **ppi = &pi;  // ppi指向一个int型的指针
```
- 指向指针的引用
  * 引用本身不是一个对象，因此不能定义指向引用的指针。
  * 指针是对象，所以存在对指针的引用
  ```cpp
  int i = 42;
  int *p;     // p是一个int型指针
  int *&r = p; // r是一个对指针p的引用
  
  r = &i;     // r引用了一个指针，因此给r赋值&i就是令p指向i
  *r = 0;    // 解引用r得到i, 也就是p指向的对象，将i的值改为0 
  ```
- 要理解变量的类型到底是什么，最简单的办法就是**从右向左阅读**r的定义

## const限定符
- 动机：希望定义一些不能被改变值的变量。
  * const对象一旦创建后其值就不能再改变，所以const对象必须初始化

### 初始化和const
- const对象主要的限制就是只能执行不改变其内容的操作，其他像算术运算，类型转换都和普通类型一样
```cpp
int i = 42;
const int ci = i;
const int bufSize = 512;
```
- 默认情况下，const对象被设定为仅在文件内有效，当多个文件中出现了同名的const变量时，其实等同于在不同文件中分别定义了独立的变量
- 只在一个文件中定义const，而在多个文件中使用它，可使用`extern`关键字
```cpp
// file_1.cc
extern const int bufSize = fcn();
// file.h
extern const int bufSize; // 与file_1.cc中定义的是同一个bufSize
```
### const的引用
- 可以将引用绑定到const对象上，称之为**对常量的引用**, 与普通引用不同的事，对常量的引用不能被用作修改它所绑定的对象
```cpp
const int ci = 1024;
const int &r1 = ci;   // 正确：引用及其对应的对象都是常量
r1 = 42;              // 错误：r1是对常量的引用
int &r2 = ci;         // 错误：试图让一个非常量引用指向一个常量对象
```
- 通常来说，引用的类型必须与其所引用的对象类型一致，但是有两个例外:
  * 第一种例外就是在初始化常量引用时允许用任意表达式作为初始值，只要该表达式的结果能够转换成引用的类型即可
  ```cpp
  int i = 42;       // 允许将const int&绑定到一个普通int对象上
  const int &r1 = i;  // 允许将const int&绑定到一个普通int对象上
  const int &r2 = 42;  // 正确：r1是一个常量索引
  const int &r3 = r1 * 2;   // 正确：r3是一个常量引用
  int &r4 = r1 * 2;     // 错误：r4是一个普通的非常量引用 
  ```
- 当一个常量引用被绑定到另外一中类型上时到底发生了什么？
```cpp
double dval = 3.14;
const int &r1 = dval;
```
此处r1引用了一个int型的数，对r1的操作应该是整数运算，但dval是一个双精度
浮点数而非整数，因此为了确保让r1绑定一个整数，编译器把上述代码变成了如下形式：
```cpp
const int temp = dvel;  // 由双精度浮点数生成一个临时的整型常量
const int &r1 = temp;   // 让r1板顶这个临时量
```
在这种情况下r1绑定了一个**临时量**对象，所谓临时量对象就是当编译器需要一个空间来暂存表达式的求值结果时临时创建的一个未命名的对象

当r1不是常量时，如果执行了类似于上面的初始化则为非法，如果r1不是常量，则就允许对r1赋值，这样就会改变r1所引用临时量的值；
- 对临时量的引用是非法行为。

**对const的引用可能引用一个并非const的对象**
```cpp
int i = 42;
int &r1 = i;        // 引用r1绑定对象i
const int &r2 = i;  // r2也绑定对象i, 但不允许通过r2修改i的值
r1 = 0;             // r1并非常量，i的值可以修改为0
r2 = 0;             // 错误：r2是一个常量引用
```
- **当变量为常量时，其引用必须为常量引用(const)，而常量引用所引用的对象不一定非的是常量**
- 我们常常将**对const的引用**简称为**常量引用**，但严格来说并不存在常量引用，因为引用不是一个对象

### 指针和const
- **指向常量的指针**不能用于改变其所指对象的值，要想存放常量对象的地址，只能使用指向常量的指针
```cpp
const double pi = 3.14;
double *ptr = &pi;          // 错误：ptr是一个普通指针
const double *cptr = &pi;   // 正确：cptr可以指向一个双精度常量
*cptr = 42;                 // 错误：不能给*cptr赋值
```
- 指针类型必须与其所指对象的类型一致，但是有两个例外：
  * 第一种例外就是允许一个指向常量的指针指向一个非常量对象(与上面提到的引用类似)
  ```cpp
  double dval = 3.14;
  cptr = &dval;
  ```
- 和常量引用一样，指向常量的指针没有规定其所指向的对象必须是一个常量，所谓指向常量的指针仅仅要求不能通过该指针改变对象的值

**const指针**
- 指针是对象而引用不是，因此就像其他对象类型一样，允许把指针本身定为常量。
- **常量指针**必须初始化, 而且一旦初始化他的值就不能再改变了
- 把`*`放在关键词`const`之前，说明指针是一个常量
```cpp
int errNumb = 0;
int *const curErr = &errNumb;   // curErr将一值指向errNumb
const double pi = 3.1415;
const double *const pip = &pi;  // pip是一个指向常量对象的常量指针
```
- **指向常量的指针**是不能通过该指针修改指向对象的值
- **常量指针**则是不能改变指针本身, 但可以通过该指针修改所指对象的值（取决于所指对象的类型）
- 从右往左读变量，靠近`pi`, `pip`的是`const`关键词，因此是常量对象，下一个符号是`*`则表示为常量指针

**顶层const**
- **顶层const**表示指针本身是一个常量, 顶层const可以表示任意对象是常量，这一点对任何数据类型都适用
- **底层const**表示指针指向的对象是一个常量, 底层cosnt则与指针和引用等复合类型的基本类型部分有关。
- 比较特殊的事，指针类型既可以是顶层const，也可以是底层const

```cpp
int i = 0;
int *const p1 = &i;   // 不能改变p1的值，这是一个顶层const
const int ci = 42;    // 不能改变ci的值，这是一个顶层const
const int *p2 = &ci;  // 允许改变p2的值，这是一个底层const 
const int *const p3 = p2;  // 靠右const是顶层const，靠左的是底层const
const int &r = ci;    // 用于声明引用的const都是底层const
```
当执行对象拷贝操作时，常量是顶层const还是底层const区别明显，其中顶层const不受影响
```cpp
i = ci;         // 正确：拷贝ci的值，ci是一个顶层const，对此操作无影响
p2 = p3;        // 正确：p2和p3指向的对象类型相同，p3顶层const部分不影响
```
底层const的限制却不能忽视，当执行对象拷贝操作时，拷入和拷出的对象必须具有相同的底层const资格, 或者两个对象的数据类型必须能够转换,
一般来说非常量可以转换成常量，反之则不行
```cpp
int *p = p3;            // 错误：p3包含底层const定义，而p则没有
p2 = p3;                // 正确：p2和p3都是底层const
p2 = &i                 // 正确：int*能够转换成const int*
int &r = ci;            // 错误：普通的int&不能绑定到int常量上
const int &r2 = i;      // 正确：const int&可以绑定到普通int上
```
**constexpr和常量表达式**
- **常量表达式**是指值不会改变并且在编译过程就能得到计算结果的表达式
```cpp
const int max_files = 20;    // max_files是常量表达式
const int limit = max_files + 1;  // limit是常量表达式
int staff_size = 27;        // staff_size不是常量表达式
const int sz = get_size();  // sz不是常量表达式
```
其中尽管`staff_size`的初始值是一个字面值常量，但是他的数据类型是一个普通的int而非const int;
另一方面尽管`sz`本身是一个常量，但是它的具体值直到运行时才能获得，所以也不是常量表达式

**constexpr变量**
- c++ 11新标准规定，允许将变量声明为`constexpr`类型以便由编译器来验证变量的值是否为一个常量表达式。
- 声明为`constexpr`的变量一定是一个变量，而且必须使用常量表达式初始化；
```cpp
constexpr int mf = 20;
constexpr int limit = mf + 1;
constexpr int sz = size();     // 只有当size是一个constexpr函数时才是正确的声明语句
```

**字面值类型**
- 算术类型、引用、指针都属于字面值类型; 自定义类，IO库、string类型则不属于字面值类型
- 只有字面值类型可以定义为`constexpr`
- 尽管指针和引用都能定义成`constexpr`, 但是他们的初始值却收到严格限制，一个`constexpr`的指针初始化必须为`nullptr`或0，或者是存储与某个固定地址中的对象

**指针和constexpr**
- 限定符`constexpr`仅对指针有效，与指针所指的对象无关
- `constexpr`会将指针声明为`顶层const`
- `constexpr`指针只能定义于函数体外，因为函数体内部的变量通常不存放在固定地址中
```cpp
const int *p = nullptr;       // p是一个指向整型常量的指针
constexpr int *q = nullptr;   // q是一个指向整数的常量指针
constexpr int *np = nullptr;  // np是一个指向整数的常量指针，其值为空
int j = 0;
constexpr int i = 42;
// i和j都必须定义在函数体之外
constexpr const int *p = &i;  // p是常量指针，指向整型常量i
constexpr int *p1 = &j        // p1是常量指针，指向整型j
```

## 处理类型

### 类型别名
- 有两种方法可用于定义类型别名
  * 传统方法`typedef`
    ```cpp
    typedef double wages;     // wages是double的同义词
    typedef wages base, *p;   // base是double的同义词，p是double*的同义词
    ```
  * 新标准规定了一种新方法，使用**别名声明**来定义类型的别名
    ```cpp
    using SI = Sales_item;   // SI 是Sales_item的同义词
    ```
- 类型别名和类型的名字等价

**指针、常量和类型别名**
- 如果某个类型别名指代的是复合类型或常量，那么把他用到声明语句里就会产生意想不到的后果
```cpp
typedef char *pstring;    // 创建char* 的别名pstring
const pstring cstr = 0;   // cstr是一个指向char的常量指针
const pstring *ps;        // ps是一个指针，他的对象是指向char的常量指针
const char *cstr = 0;   // 是对const pstring cstr的错误理解
```
const是对给定类型的修饰，pstring是指向char的指针，因此const pstring就是指向char的常量指针，而非指向常量字符的指针
```cpp
// 对于复合类型（指针等）不能代回原式来进行理解
typedef char *pstring;  // pstring是char*的别名
const pstring cstr = 0; // 指向char的常量指针
// 如改写为const char *cstr = 0;不正确，为指向const char的指针

// 辅助理解（可代回后加括号）
// const pstring cstr = 0;代回后const (char *) cstr = 0;
// const char *cstr = 0;即为(const char *) cstr = 0;
```

### auto类型说明符
- c++11新标准引入`auto`类型说明符，用它能让编译器替我们去分析表达式所属的类型
- 与原来那些只对应一种特定类型的说明符(比如double)不同，`auto`让编译器通过初始值来推算变量的类型, 显然auto定义的变量必须有初始值

```cpp
auto item = val1 + val2   // item初始化为val1和val2相加的结果, 编译器将自动根据结果来推断item的类型
```
- 使用`auto`也能在一条语句中声明多个变量，但所有变量的数据类型必须一致
```cpp
auto i = 0, *p = &i;     // 正确：i是整数，p是整数指针
auto sz = 0, pi = 3.14;  // 错误
```
**复合类型、常量和auto**
- 当引用被用作初始值时，编译器以引用对象的类型作为auto的类型
```cpp
int i = 0, &r = i;
auto a = r;    // a是一个整数
```
- `auto`一般会忽略掉顶层const，同时底层const则会保留下来
```cpp
const int ci = i, &cr = ci;
auto b = ci;    // b是一个整数(ci的顶层const被忽略了)
auto c = cr;    // c是一个整数(cr是ci的别名，ci本身是一个顶层const)
auto d = &i;    // d是一个整型指针(整数的地址就是指向整数的指针)
auto e = &ci;   // e是一个指向整数常量的指针(对常量对象取地址是一种底层const)
// 如果希望推断出的auto是一个顶层const，需要明确指出
const auto f = ci;

// 还可以将引用的类型设为auto，此时原来的初始化规则仍然适用
auto &g = ci;         // g是一个整型常量引用，绑定到ci
auto &h = 42;         // 错误：不能为非常量引用绑定字面值
const auto &j = 42;   // 正确：可以为常量引用板顶字面值
```
设置一个类型为auto的引用时，初始值中的顶层常量属性仍然保留, 和往常一样，如果给初始值绑定一个引用，则此时的常量就不是顶层常量了

### decltype类型指示符
- 有时希望从表达式的类型推断出要定义的变量类型，但不想用该表达式的值初始化变量
- 因此C++11新标准引入了第二种类型说明符`decltype`, 它的作用是选择并返回操作数的数据类型, 在此过程中编译器分析表达式并得到他的类型，却不实际计算表达式的值
```cpp
decltype(f()) sum = x;    // sum的类型就是函数f的返回类型
```
编译器并不实际调用函数f，而是使用当调用发生时f的返回值类型作为sum的类型
- `decltype`处理顶层const和引用的方式与`auto`有些许不同，如果`decltype`使用的是表达式是一个变量，则`decltype`返回该变量的类型(包括顶层const和引用)
```cpp
const int ci = 0, &cj = ci;
decltype(ci) x = 0;     // x是const int
decltype(cj) y = x;     // y的类型是const int&，y绑定到变量x
decltype(cj) z;         // 错误：z是一个引用，必须初始化
```

**decltype和引用**
```cpp
// decltype的结果可以是引用类型
int i = 42, *p = &i, &r = i;
decltype(r + 0) b;  // 正确：加法的结果是int，因此b是一个（未初始化的）int
decltype(*p) c;     // 错误：c是int&，必须初始化
```
因为`r`是一个引用，因此`decltype(r)`的结果是引用类型，如果想让结果类型是r所指的类型，可以把r作为表达式的一部分
如`r+0`

```cpp
// decltype的表达式如果是加上了括号的变量，结果将是引用
decltype((i)) d;         // 错误：d是int&，必须初始化
decltype(i) e;          // 正确：e是一个未初始化的int
```
- decltype((variable))的结果永远都是引用，而decltype(variable)只有当variable本身是引用时才是引用

## 自定义数据结构
> 尽量不要吧类定义和对象定义放在一起。如`struct Student{} xiaoming,xiaofang;`
- 类可以以关键字`struct`开始，紧跟类名和类体。
- 类数据成员：类体定义类的成员。
- `C++11`：可以为类数据成员提供一个**类内初始值**（in-class initializer）。
```cpp
struct Sales_data {
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
  };
```

**头文件**
- 类通常定义在头文件里

预处理器概述：

- **预处理器**（preprocessor）：确保头文件多次包含仍能安全工作。
- 当预处理器看到`#include`标记时，会用指定的头文件内容代替`#include`
- **头文件保护符**（header guard）：头文件保护符依赖于预处理变量的状态：已定义和未定义。
  - `#ifdef`已定义时为真
  - `#ifndef`未定义时为真
  - 头文件保护符的名称需要唯一，且保持全部大写。养成良好习惯，不论是否该头文件被包含，要加保护符。

```cpp
// 使用这些功能就能有效防止重复包含的发生
#ifndef SCALES_DATA_H
#define SCALES_DATA_H
#include <string>
struct Sales_data {
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue 0.0;
  };
#endif
```

# 第三章 字符串、向量和数组

## using声明
- 使用某个命名空间：例如 `using std::cin`表示使用命名空间`std`中的名字`cin`。
- 头文件中不应该包含`using`声明。这样使用了该头文件的源码也会使用这个声明，会带来风险。

## string
- 标准库类型`string`表示可变长的字符序列。
- `#include <string>`，然后 `using std::string;`
- **string对象**：注意，不同于字符串字面值。
```cpp
#include <string>
using std::string;
string s1;              // 默认初始化，s1是一个空字符串
string s2 = s1;
string s3 = "hiya";
string s4(10, 'c');     // cccccccccc
```

### 定义和初始化string对象

初始化`string`对象的方式：

| 方式                  | 解释                                                    |
| --                    | --                                                      |
| `string s1`           | 默认初始化，`s1`是个空字符串                            |
| `string s2(s1)`       | `s2`是`s1`的副本                                        |
| `string s2 = s1`      | 等价于`s2(s1)`，`s2`是`s1`的副本                        |
| `string s3("value")`  | `s3`是字面值“value”的副本，除了字面值最后的那个空字符外 |
| `string s3 = "value"` | 等价于`s3("value")`，`s3`是字面值"value"的副本          |
| `string s4(n, 'c')`   | 把`s4`初始化为由连续`n`个字符`c`组成的串                |

- 拷贝初始化（copy initialization）：使用等号`=`将一个已有的对象拷贝到正在创建的对象。
- 直接初始化（direct initialization）：通过括号给对象赋值。

### string对象上的操作

| 操作                 | 解释                                                                                       |
|----------------------|--------------------------------------------------------------------------------------------|
| `os << s`            | 将`s`写到输出流`os`当中，返回`os`                                                          |
| `is >> s`            | 从`is`中读取字符串赋给`s`，字符串以空白分割，返回`is`                                      |
| `getline(is, s)`     | 从`is`中读取一行赋给`s`，返回`is`                                                          |
| `s.empty()`          | `s`为空返回`true`，否则返回`false`                                                         |
| `s.size()`           | 返回`s`中字符的个数                                                                        |
| `s[n]`               | 返回`s`中第`n`个字符的引用，位置`n`从0计起                                                 |
| `s1+s2`              | 返回`s1`和`s2`连接后的结果                                                                 |
| `s1=s2`              | 用`s2`的副本代替`s1`中原来的字符                                                           |
| `s1==s2`             | 如果`s1`和`s2`中所含的字符完全一样，则它们相等；`string`对象的相等性判断对字母的大小写敏感 |
| `s1!=s2`             | 同上                                                                                       |
| `<`, `<=`, `>`, `>=` | 利用字符在字典中的顺序进行比较，且对字母的大小写敏感（对第一个不相同的位置进行比较）       |

**读写string对象**
- string io：
    - 执行读操作`>>`：忽略掉开头的空白（包括空格、换行符和制表符），直到遇到下一处空白为止。
```cpp
int main()
{
    string s;    // 空字符串
    cin >> s;    // 将string对象读入s，遇到空白停止
    cout << s << endl;

    string s1, s2;
    cin >> s1 >> s2;    // 把第一个输入读到s1中，第二个读到s2中
    cout << s1 << s2 << endl;
    return 0;
}
```

**读取位置数量的string对象**
```cpp
int main()
{
  string word;
  while (cin >> word)    // 反复读取，直到文件末尾
    count << word << endl;
  return 0
}
```
**使用getline读取一整行**
- `getline`：读取一整行，**包括空白符**。
```cpp
int main()
{
  string line;
  // 每次读入一整行，直到文件末尾
  while (getline(cin, line))
    cout << line << endl;
  return 0
}
```
**string的empty和size**
```cpp
while (getline(cin, line))
  if (!line.empty())
    cout << line << endl;
```

```cpp
while (getline(cin, line))
  if (line.size() > 80)
    cout << line << endl;
```
- `s.size()`返回的是`string::size_type`类型，记住是一个**无符号**类型的值，不要和`int`混用


**比较string对象**
1. 如果两个string对象长度不同，且较短string的每个字符都与较长string对象对应位置上的字符相同，则短string小于较长string
2. 如果两个string对象在某些对应的位置上不一致，则**string对象比较的结果其实是string对象总第一对相异字符比较的结果**
```cpp
string str = "Hello";
string phrase = "Hello world";
string slang = "Hiya";
```
根据规则1可知`str`小于`phrase`; 根据规则2可知，对象`slang`即大于`str`也大于`phrase`

**两个string相加**
```cpp
string s1 = "hello, ", s2 = "world\n";
string s3 = s1 + s2;
s1 += s2;     // 等价于s1 = s1 + s2
```
**字面值和string对象相加**
- 当把`string`对象和字符字面值以及字符串字面值混在一条语句中使用时，必须确保每个加法运算法(+)的两侧至少有一个是`string`
```cpp
string s1 = "hello", s2 = "world";
string s3 = s1 + ", " + s2 + "\n";
string s4 = s1 + ", ";
string s5 = "hello" + ", ";    // 错误，两个运算对象都不是string
string s6 = s1 + ", " + "world";   // 正确：s1和", "首先相加得到一个string再与“world”相加
string s6 = (s1 + ", ") + "world"; // 等价于上一行
string s7 = "hello" + ", " + s2;  // 错误：不能把字面值直接相加
```

### 处理string对象中的字符

- **ctype.h vs. cctype**：C++修改了c的标准库，名称为去掉`.h`，前面加`c`。
  > 如c++版本为`cctype`，c版本为`ctype.h`
  - **尽量使用c++版本的头文件**，即`cctype`

`cctype`头文件中定义了一组标准函数：

| 函数          | 解释                                                                      |
|---------------|---------------------------------------------------------------------------|
| `isalnum(c)`  | 当`c`是字母或数字时为真                                                   |
| `isalpha(c)`  | 当`c`是字母时为真                                                         |
| `iscntrl(c)`  | 当`c`是控制字符时为真                                                     |
| `isdigit(c)`  | 当`c`是数字时为真                                                         |
| `isgraph(c)`  | 当`c`不是空格但可以打印时为真                                             |
| `islower(c)`  | 当`c`是小写字母时为真                                                     |
| `isprint(c)`  | 当`c`是可打印字符时为真                                                   |
| `ispunct(c)`  | 当`c`是标点符号时为真                                                     |
| `isspace(c)`  | 当`c`是空白时为真（空格、横向制表符、纵向制表符、回车符、换行符、进纸符） |
| `isupper(c)`  | 当`c`是大写字母时为真                                                     |
| `isxdigit(c)` | 当`c`是十六进制数字时为真                                                 |
| `tolower(c)`  | 当`c`是大写字母，输出对应的小写字母；否则原样输出`c`                      |
| `toupper(c)`  | 当`c`是小写字母，输出对应的大写字母；否则原样输出`c`                      |

**遍历字符**
- C++新标准提供for
```cpp
/*
expression部分是一个对象，表示一个序列
declaration负责定义一个变量，用于访问序列中的基础元素
每次迭代，declaration部分变量会被初始化为expression的下一个元素
*/
for (declaration: expression)
  statement
```
```cpp
string str("some string");
// 每行输出一个字符
for (auto c: str)
  cout << c << endl;
```
```cpp
string s("Hello World!!!");
decltype(s.size()) punct_cnt = 0;
// 统计s中的标点符号数量
for (auto c : s)
  if (ispunct(c))
    ++punct_cnt;
count << punct_cnt
      << " punctuation characters in " << s << endl;
```

**使用范围for语句改变字符串中的字符**
- 如果想要改变string对象中的字符值，必须把循环变量定义成引用类型
```cpp
string s("Hello World!!!");
// 转换成大写形式
for (auto &c : s)
  c = toupper(c);
count << s<< endl
```
**下标索引**
- `str[x]`,[]输入参数为`string::size_type`类型，给出`int`整型也会自动转化为该类型
```cpp
string s("somge string");
if (!s.empty())
  s[0] = toupper(s[0])

// 依次处理s中的字符直至我们处理完全部字符或者遇到一个空白
for (decltype(s.size()) index = 0;
    index != s.size() && !isspace(s[index]); ++index)
      s[index] = toupper(s[index]);
```

**使用下标执行随机访问**
```cpp
const string hexdigits = "0123456789ABCDEF";
cout << "Enter a series of numbers between 0 and 15"
     << " separated by spaces. Hit Enter when finished: "
     << endl;
string result;
string::size_type n;
while (cin >> n)
  if (n < hexdigits.size())
    result += hexdigits[n];
count << "Your hex number is: " << result <<endl;
```
## vector
- vector是一个**容器**，也是一个类模板；
- 容器：包含其他对象。
- 类模板：本身不是类，但可以**实例化instantiation**出一个类。 `vector`是一个模板， `vector<int>`是一个类型。

```cpp
#include <vector>
using std::vector;
vector<int> ivec;    // ivec保存int类型的对象
vector<vector<string>> file;   // 该向量的元素是vector对象
```

### 定义和初始化vector对象

初始化`vector`对象的方法

| 方法                        | 解释                                                          |
|-----------------------------|---------------------------------------------------------------|
| `vector<T> v1`              | `v1`是一个空`vector`，它潜在的元素是`T`类型的，执行默认初始化 |
| `vector<T> v2(v1)`          | `v2`中包含有`v1`所有元素的副本                                |
| `vector<T> v2 = v1`         | 等价于`v2(v1)`，`v2`中包含`v1`所有元素的副本                  |
| `vector<T> v3(n, val)`      | `v3`包含了n个重复的元素，每个元素的值都是`val`                |
| `vector<T> v4(n)`           | `v4`包含了n个重复地执行了值初始化的对象                       |
| `vector<T> v5{a, b, c...}`  | `v5`包含了初始值个数的元素，每个元素被赋予相应的初始值        |
| `vector<T> v5={a, b, c...}` | 等价于`v5{a, b, c...}`                                        |

- 列表初始化： `vector<string> v{"a", "an", "the"};` （C++11）

### 向vector对象中添加元素

- `v.push_back(e)` 在尾部增加元素。
```cpp
#include <vector>
using std::vector;
vector<int> v2;
for (int i = 0; i != 100; ++i)
  v2.push_back(i);

```

### 其他vector操作

`vector`支持的操作：

| 操作               | 解释                                                             |
|--------------------|------------------------------------------------------------------|
| `v.emtpy()`        | 如果`v`不含有任何元素，返回真；否则返回假                        |
| `v.size()`         | 返回`v`中元素的个数                                              |
| `v.push_back(t)`   | 向`v`的尾端添加一个值为`t`的元素                                 |
| `v[n]`             | 返回`v`中第`n`个位置上元素的**引用**                             |
| `v1 = v2`          | 用`v2`中的元素拷贝替换`v1`中的元素                               |
| `v1 = {a,b,c...}`  | 用列表中元素的拷贝替换`v1`中的元素                               |
| `v1 == v2`         | `v1`和`v2`相等当且仅当它们的元素数量相同且对应位置的元素值都相同 |
| `v1 != v2`         | 同上                                                             |
| `<`,`<=`,`>`, `>=` | 以字典顺序进行比较                                               |

```cpp
vector<int> v{1, 2, 3, 4, 5, 6, 7, 8, 9};
for (auto &i : v)
  i *= i;
for (auto i : v)
  cout << i << " ";
cout << endl;
```

```cpp
vector<unsigned> scores(11, 0)
unsigned grade;
while (cin >> grade) {
    if (grade <= 100)
      ++score[grade/10];
  }
```

## 迭代器
- 所有标准库容器都可以使用迭代器。
- 类似于指针类型，迭代器也提供了对对象的间接访问。

- `auto b = v.begin();`返回指向第一个元素的迭代器。
- `auto e = v.end();`返回指向最后一个元素的下一个（哨兵，尾后,one past the end）的迭代器（off the end）。
- 如果容器为空，则begin和end返回的是同一个迭代器，都是尾后迭代器

- 使用解引用符`*`访问迭代器指向的元素。
- 养成使用迭代器和`!=`的习惯（泛型编程）。
- **容器**：可以包含其他对象；但所有的对象必须类型相同。
- **迭代器（iterator）**：每种标准容器都有自己的迭代器。`C++`倾向于用迭代器而不是下标遍历元素。
- **const_iterator**：只能读取容器内元素不能改变。
- **箭头运算符**： 解引用 + 成员访问，`it->mem`等价于 `(*it).mem`
- **谨记**：但凡是使用了**迭代器**的循环体，都**不要**向迭代器所属的容器**添加元素**。

标准容器迭代器的运算符:

| 运算符           | 解释                                   |
|------------------|----------------------------------------|
| `*iter`          | 返回迭代器`iter`所指向的**元素的引用** |
| `iter->mem`      | 等价于`(*iter).mem`                    |
| `++iter`         | 令`iter`指示容器中的下一个元素         |
| `--iter`         | 令`iter`指示容器中的上一个元素         |
| `iter1 == iter2` | 判断两个迭代器是否相等                 |

```cpp
string s("some string");
if (s.begin() != s.end()) {
    auto it = s.begin();
    *it = toupper(*it);
  }
```

**将迭代器从一个元素移动到另一个元素(++运算符)**
```cpp
for (auto it = s.begin(); it != s.end() && !isspace(*it); ++it)
  *it = toupper(*it);
```

**迭代器类型**

```cpp
// 一般来说不知道迭代器的精确类型，采用iterator和const_iterator表示迭代器类型
vector<int>iterator it;     // it能读写vector<int>的元素
string::iterator it2;       // it2能读写string对象中的字符

vector<int>::const_iterator it3;  // it3只能读元素，不能写元素
string::const_iterator it4;  // it4只能读字符，不能写字符
```

<++>
