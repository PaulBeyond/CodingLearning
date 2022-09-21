[TOC]

# BOOK_1_C与指针

## CHAPTER_1_上手

​	空白、注释、制表符 -> 提升代码可读性，便于后续修改

​	若有一份声明需要运用到不同的源文件中，可以include第一个头文件，而后在需要用到的源文件中声明一份拷贝，而用不着在许多不同的地方进行复制，避免维护时出现错误。

​	宏定义：字符串常量；函数原型的声明；main函数。

​	C语言中不存在string类型，字符串终止符为NUL，且终止符不看作是字符串的一部分，字符串常量就是用双引号括起来的一串字符。

​	格式化字符输出：%d %o %x ： 二进制、八进制、十六进制。

## CHAPTER_2_基本概念

翻译环境：源代码被转化成为可执行的机器指令；

执行环境：实际执行代码；

两种环境不必位于同一台机器上，例如交叉编译器；

独立环境是指不存在操作系统的环境，一般在嵌入式系统中遇到该类环境

### 翻译过程：

1. 预处理器处理：该阶段预处理器在源代码上执行一些文本操作，例如以实际值代替宏定义指令符号，读入include指令中包含的文件内容
2. 解析阶段：判断语句的意思，该阶段是产生绝大多数error和warning信息的地方，而后产生目标代码。目标代码是机器指令的初步形式，用于实现程序的语言。同时，在该阶段若存在需要进行优化的选项，优化器会对目标代码进一步进行处理，提高效率。

### 执行过程

1. 程序必须载入到内存中；
2. 程序执行开始，通常一个小型的启动程序与程序链接在一起，而后调用main函数；
3. 开始执行程序代码，运行堆栈stack以存储函数的局部变量和返回地址，同时程序也可以使用静态内存，存储于静态内存中的变量在程序的整个执行过程中将一直保留它们的值。
4. 程序终止。

### 词法规则

注释不能嵌套，编译时会被预处理器拿掉，取而代之的是一个空格。

### 代码风格

1. 空行用于分割不同的逻辑代码块，按功能分段；
2. 绝大多数操作符的使用，中间都隔以空格，以增强可读性；
3. 嵌套于其他语句的语句使用缩进，以显示他们之间的层次；
4. 注释成块出现

## CHAPTER_3_数据

1. 整型：有符号、无符号，长整型
2. ......
3. 指针：
   1. 指针常量
   2. 字符串常量

typedef：为各种数据类型定义新的名字

const：申明常量不能修改

1. 指向整型常量的指针：可以修改指针的值，但不能修改所指向的值
2. 指向整型的常量指针：指针是常量，但可以修改所指向的整型的值

```C++
int const * pci; // 1. 指向整型常量的指针
int * const cpi; // 2. 指向整型的常量指针
int const * const cpci; // 指针和指向都是常量，不能更改
```

const和define相比，define更好，因为只要允许使用字面值常量的地方都可使用define，而const常量只能用于允许使用变量的地方。

```C++
#define MAX_ELEMENTS 50
int const max_elements = 50;
```

4. 在代码块之外声明的变量总是存储于静态内存中的，不属于堆栈内存，称为静态变量；
5. 代码块内部声明的变量存储于堆栈中，如果加上关键词static，则可以使他的存储类型从auto变为static，具有静态存储类型的变量在整个程序执行过程中一直存在

## CHAPTER_4_语句

空语句：本身只包含一个分号；

表达式语句：

常用语句与C++相同

## CHAPTER_5_操作符和表达式

移位操作符：简单地把一个值的位向左或者向右移动

1. 在左移位中，值最左边的几位被丢弃，右边多出来的几个空位由0补齐
2. 右移位操作
   1. 逻辑移位，左边移入的位用0填充
   2. 算术移位：左边移入的位由原先该值的符号决定，即符号位为1则移入位均为1；
3. 移位操作需要为整型，对于有符号值，采取逻辑移位还是算术移位取决于编译器

位操作符对它们的操作数各个位执行AND、OR和XOR等逻辑操作（&、|、^）；

关系操作符的返回值是整型，符合则为1，否则为0；（C语言中）

条件操作符：exp1 ? exp2 : exp3

逗号操作符，整个逗号表达式的值就是最后那个表达式的值

左值就是能够出现在赋值符号左边的东西，右值就是那些可以出现在赋值符号右边的东西：

1. 左值可以充当右值，右值不一定可以充当左值

表达式求值：

1. 隐式类型转化
2. 算术转换

操作符的属性：优先级、结合性、执行顺序；

## CHAPTER_6_指针

字节：每个字节包含8个位，可以存储无符号值(0~255)或有符号值(-128~127)

字：为了存储更大的值，通常把两个或者更多个字节合在一起作为一个更大的内存单元，许多机器以字为单元存储整数，每个字一般包含2个或者4个字节。

关心的主要问题：

1. 内存中每个位置由一个独一无二的地址标识
2. 内存中的每个位置都包含一个值

值的类型并非值本身所固有的一种特性，而是取决于它使用的方式。

指针自身的值为一个地址值，而需要使用间接访问操作符来获取其所指向的值

NULL指针：表示不指向任何东西，亦可对指针变量赋零值实现

```c++
*&a = 25;
```

指针的指针：*操作符具有从右向左的结合性

指针表达式

## CHAPTER_7_函数

返回类型+函数名(形式参数)+代码块

## CHAPTER_8_数组

数组名的值是一个指针常量，指向数组第一个元素的地址。

正确使用的指针比下标更有效率，指针和数组并不是相等的

初始化与不完整初始化

### 多维数组

```c++
int (*p)[10]; // p为指向整型数组的指针
int matrix[3][10];
int (*p)[10] = matrix; // p指向matrix的第一行
int *pi = & matrix[0][0]; // pi 指向matrix的第一个整型元素
int *pi = matrix[0]; // 同上
```

当多维数组作为函数参数进行传递时：

```c++
// 一维
int vector[10];
void func1(int * vec);
void func2(int vec[]);
// 二维
int matrix[3][10];
void func3(int (*mat)[10]);
void func4(int mat[][10]);
```

指针数组：

```c++
int * pi[10];
```

## CHAPTER_9_字符串、字符和字节

## CHAPTER_10_结构和联合

struct：结构的声明与初始化，可以将结构看做最简单的类；

union：联合的所有成员引用的是内存中的相同位置

## CHAPTER_11_动态内存分配

malloc 可以从内存池中提取一块适合的内存，并向该程序返回一个指向这块内存的指针

free：当以前分配的内存不再使用时，程序调用free函数将它归还给内存池供以后之需；

```c++
include "stdlib.h"
void * malloc(size_t size);
void free(void *pointer);
```

​	malloc() 的参数为所需要的分配的内存字节数或者字符数，若可用内存满足需求，则返回一个指向被分配的内存块起始位置的指针：**连续内存！实际分配的内存可能比请求的稍多！**若可用内存不能满足需求，则返回NULL指针。

​	free()的参数要么为NULL，要么是先前从malloc、calloc或者realloc中创建出来的。

​	malloc()并不知道所请求内存需要存储的数据类型！！

```c++
void * calloc(size_t num_elements, size_t element_size);
void realloc(void *ptr, size_t new_size);
```

calloc与malloc相比在返回指向内存的指针之前将它初始化为0

realloc用于修改一个原先已经分配的内存块大小：

1. 扩大，则原先内容依旧保留，新增加的内存添加到原先内存块的后面；
2. 缩小：该内存块尾部的部分内存被拿掉，剩余部分内存的原先内容依旧保留；
3. 若原来内存块无法改变大小，realloc将分配到另一块大小正确的内存，并完成相应的复制操作；
4. 若realloc第一个参数为NULL，则与malloc一模一样。

```c++
int * pi;
pi = malloc(25 * sizeof(int));
```

动态内存的常见错误：

1. 对NULL指针进行解引用操作；
2. 对分配的内存进行操作时越过边界；
3. 释放非动态分配的内存；
4. 试图释放一块动态分配的内存的一部分；
5. 一块动态内存被释放后继续使用；
6. 动态分配的内存不再使用时，没有及时释放。

## CHAPTER_12_使用结构和指针

构建链表：单链表、双链表

## CHAPTER_13_高级指针话题(Page 278)

多层间接访问

```c++
int ***pi;
int (*f) ();
```

函数调用操作符的优先级高于间接访问操作符

下标操作符的优先级高于间接访问操作符

函数指针！

```c++
int f(int);
int (*pf)(int) = & f; // 创建函数指针pf指向f
int ans = f(25);
int ans = (*pf)(25);
int ans = pf(25); // 间接访问操作非必须
```

传递命令行参数

```c++
int main(int argc, char ** argv)
```

处理命令行参数

## CHAPTER_14_预处理器

```C++
_FILE_ // 进行编译的源文件名称
_LINE_ // 文件当前的行号
_DATE_ // 文件被编译的日期
_TIME_ // 文件被编译的时间
_STDC_ // 如果编译遵循ANSI_C，其值为1，否则未定义
#define name stuff // 	宏定义(defined macro)
#undef name // 移出一个宏定义
```

条件编译

```c++
#if constant-expression
#elif
#else
#endif
```

是否被定义

```C++
#ifndef
#if defined()
#ifdef
#id !defined()
```

## CHAPTER_15_输入输出函数

## CHAPTER_16_标准函数库

## CHAPTER_17_经典抽象数据类型

内存分配：

1. 静态数组：结构长度固定，编译时即确定，不容易出错
2. 动态数组：灵活性与复杂性的权衡取舍
3. 链式结构：最大程度上的灵活性，每个元素在需要的时候才单独进行分配，几乎没有数量限制，但是访问特定元素的效率不如数组

堆栈(stack)：后进先出

1. 堆栈接口：pop(将栈顶元素移出，不返回)，push，top(返回栈顶元素，不移出)
2. 实现堆栈：

队列(Queue)：先进先出

树(Tree):

## CHAPTER_18_运行时环境



# BOOK_2_C++_Primer_Plus

## CHAPTER_0_前言

现代C++语言组成部分：低级语言(继承自C语言)、现代高级语言特性、标准库。

## CHAPTER_1_开始

编译命令

初始输入输出：

1. cin 和 cout
2. cerr：输出警告和错误信息，称作标准错误
3. clog：用于输出程序运行的一般性信息

标准库定义的所有名字都在命名空间`std`中，可以通过使用作用域运算符(::)来指出想使用定义在命名空间的名字

注释界定符不能嵌套

### 读取数量不定的输入数据

```c++
#include <iostream>
int main()
{
	int sum = 0, value = 0;
	while(std::cin >> value)
    /*
    * 若流是有效的，则检测成功，若遇到无效输入或者遇到文件结束符(end-of-file)，则返回False结束循环
    */
		sum += value;
	std::cout << "Sum is: " << sum << std::endl;
	return 0;
}
```

Tips：Win系统中输入文件结束符的方法是Ctrl + Z，然后Enter或者Return；在Unix或者macOS中，用Ctrl+D。

### 类简介

通过定义一个类(class)来定义自己的数据结构

## CHAPTER_2_变量和基本类型

算数类型(arithmetic type，包括字符、整型数、布尔值和浮点数)和空类型(void)

### 算术类型

算数类型分为两类

1. 整型：integral type，包括字符和布尔类型在内；
2. 浮点型

算术类型所占的比特数在不同机器上有所差别，C++标准规定的尺寸最小值为：

![image-20220901001919744](C:\Users\Hongji-Li\AppData\Roaming\Typora\typora-user-images\image-20220901001919744.png)

bool类型的取值是`TRUE`或者`False`

```c++
bool flag = (bool) 1; // warning c-cast
bool flag = bool(1); // right
bool flag = 1; // right 隐式转换
```

当我们赋给无符号类型一个超出它表示范围的值时，结果是初始值对无符号类型表示数值总数取模后的余数

```c++
unsigned char c = -1; // 假设char占8比特，表征0-255，则对256取模，c=255
```

但当我们赋给带符号类型一个超出它表示范围的值，结果是未定义的，此时程序可能继续工作、崩溃，或者产生垃圾数据

```c++
unsigned char c1 = 266;
```

### 变量

变量定义：

对象：指一块能存储数据并具有某种类型的内存空间

初始值与初始化，以下四种等价

```c++
int k = 0;
int k = {0};
int k(0);
int k{0};
```

若使用列表初始化且初始化值存在丢失信息的风险，则编译器会报错：

```c++
long double ld = 3.1415;
int a{ld}, b = {ld}; // error
int c(ld), d = ld; // right, Some values are discarded
```

变量声明与定义：

1. 分离式编译机制的存在，允许将程序分割成若干个文件，并可被独立编译
2. 声明：使得名字为程序所知，规定了变量的类型和名字
3. 定义：创建与名字关联的实体，申请存储空间

```c++
extern int i; // declaration
int j; // define
```

4. 任何包含了显示初始化的声明即成为定义。
5. 变量只能被定义一次，但可以被多次声明，因此需要避免重复定义

### 复合类型

引用：即别名，必须初始化，允许在一条语句中定义多个引用，但必须都以&开头

指针：与引用类似，区别如下：

1. 指针本身也是一个对象，允许对其赋值与拷贝
2. 指针的生命周期内可以先后指向几个不同的对象
3. 指针无须在定义时赋值，若没有初始化，将拥有一个不确定的值

void* 指针是一种特殊的指针类型，可以用于存储任意对象的地址，一个void*指针存在着一个地址

### const 限定符

const对象一旦创建后其值就不能再改变了，故必须进行初始化

const变量仅在文件内有效，当多个文件中出现同名的const变量时，其实等同于在不同文件中分别定义了独立的变量

若需要在别的文件使用，则需要在定义和声明都添加extern关键字，这样就只需要定义一次就好了

const的引用->对常量的引用：对常量的引用不能被用作修改它所绑定的对象

指向常量的指针：不能用于改变其所指对象的值

常量指针必须初始化

#### 顶层const：

1. 指针本身是一个对象，它又可以指向另一个对象，因此指针本身是不是常量以及指针所指的是不是一个常量就是两个相互独立的问题
2. 名词顶层const表示指针本身是个常量，底层const表示指针所指的对象是一个常量：

```c++
int i = 0;
int * const p1 = & i; // 不能改变p1的值，这是一个顶层const
const int ci =42; // 不能改变c1的值，这是一个顶层const
const int * p2 = &ci; // 允许改变p2的值，这是一个底层const
const int * const p3 = p2; // 靠右的const是顶层const，靠左的是底层const
const int & r = ci; //用于声明引用的const都是底层const
```

3. 当执行对象的拷贝操作时，常量是顶层const或者底层const区别明显，其中，顶层const不受声明影响，执行拷贝操作并不会改变被拷贝对象的值；
4. 当执行对象的拷贝操作时，拷入和拷出的对象必须具有相同的底层const资格，或者两个对象的数据类型必须能够转换，一般来说，非常量可以转换成常量，反之则不行：

```c++
int * p = p3; // error, p3包含底层const的定义，而p没有
p2 = p3; // right
p2 = & i; // right, int * -> const int *
int & r = ci; // error, int & 不能绑定在int常量上
const int & r2 = i; // right, const int & 可以绑定到一个普通的int上
```

#### constexpr和常量表达式

常量表达式是指值不会改变并在编译过程中就能得到计算结果的表达式，显然，字面值属于常量表达式，用常量表达式初始化的const对象也是常量表达式

一个对象或者表达水是不是常量表达式由它的数据类型和初始值共同决定

c++11新标准规定：允许将变量声明为constexpr类型以便由编译器来验证变量的值是否是一个常量表达式

若在constexpr声明中定义了一个指针，限定符constexpr仅对指针有效，对指针所指的对象无关

### 处理类型

typedef：定义类型别名

新标准规定了一种新的方法，使用别名声明来定义类型的别名：

```c++
using SI = Sales_time;
```

```c++
typedef char *pstring; // pstring 为类型 char* 的别名
const pstring cstr = 0; // cstr 是指向char的常量指针
const pstring *ps; // ps 是一个指针，他的对象是指向char的常量指针
const char * cst3 = 0; // cst3 是一个指向const char的指针
```

#### auto类型说明符

1. 使用引用其实就是使用引用的对象，当引用被用作初始值时，真正参与初始化的其实是引用对象的值，此时编译器以引用对象的类型作为auto的类型；
2. auto一般回忽略顶层const，保留底层const，如果需要推断出的auto类型是一个顶层const，则需要指出

```c++
const auto f = ci;
```

#### decltype类型指示符

选择并返回操作数的数据类型，在此过程中，编译器分析表达式并得到它的类型，但不实际计算表达式的值：

```c++
decltype(f()) sum = x; // sum 的类型为函数f的返回值类型
```

### 自定义数据结构

struct关键字



## CHAPTER_3_字符串、向量和数组

  使用using声明，可以不再使用专门的前缀(::)，具体有：

```c++
using namespace ::name;
```

位于头文件的代码，一般来说不应该使用using声明，因为头文件的内容会拷贝到所有引用它的文件中取，如果头文件中有某个using声明，那么每个使用该头文件的文件就会有这个声明，有可能存在始料未及的名字冲突

### 标准库类型string

标准库类型string表示可变长的字符序列，使用string应该首先包含string头文件，作为标准库的一部分，string也被定义在命名空间std中

定义和初始化string对象：

```c++
string s4(10, 'c'); // s4 = "cccccccccc"
```

直接初始化：不使用等号<->拷贝初始化，使用等号（除了上面代码只能直接初始化，其他两者差不多）

读写string对象：

```c++
cin >> str ; // 将string对象读入str，遇到空白停止
getlint(cin, line); //读取一行
```

string类型的比较：

1. 相等，完全相等
2. 如果string长度不一样，而且较短的string对象的每个字符都与较长string对象对应位置上的字符相同，短的小
3. 如果两个string对象在某些对应位置不一致，则string对象比较的结果其实是string对象中第一个相异字符的比较结果

标准库允许将字符字面值和字符串字面值转化为string对象

### 标准库类型vector

vector容纳着其他对象，所以常被称作容器，包含于vector头文件

![image-20220909000256435](C:\Users\Hongji-Li\AppData\Roaming\Typora\typora-user-images\image-20220909000256435.png)

列表初始化vector对象：

```c++
vector<int> ivec;
vector<int> ivec1(ivec);
vector<int> ivec2 = ivec;

```















































































































## END_FILE(LOADING_BOOK_2_PAGES_114)



# BOOK_3_First_Line_in_Android

## CHAPTER_1_BEGIN

Android系统架构：Linux内核层，系统运行库层，应用框架层，应用层

1. Linux内核层，Android系统是基于Linux内核的，这一层为Android设备的各种硬件提供了底层的驱动
2. 系统运行库层：这一层通过一些C/C++为Android提供主要的特性支持，也包含Android运行时库，提供一些核心库并允许开发者使用Java编写Android应用。Android运行时库中包含ART运行环境，使得每一个Android应用都能运行在独立的进程中，并拥有一个自己的虚拟机实例
3. 应用框架层：主要提供了构建应用程序可能用到的API
4. 应用层：所有安装在手机上的应用程序都属于这一层

### Android开发特色：

1. 四大组件：Activity, Service, BroadcastReceiver, and ContentProvider.
2. 丰富的系统控件
3. SQLite数据库
4. 强大的多媒体

### 环境搭建。

Project模式的项目结构：

1. .gradle 和 .idea ：放置Android Studio自动生成的文件，无需关心or手动编辑
2. app：项目中的代码、资源等内容
3. build：编译时自动产生的文件
4. gradle：包含gradle wrapper的配置文件，使用gradle wrapper的方式不需要提前将gradle下载好，而是自动根据本地的缓存情况决定是否需要联网下载gradle。Android Studio默认是启用gradle wrapper方式的，也可以改成离线模式
5. .gitignore：用来将制定的目录或文件排除在版本控制之外
6. build.gradle：项目全局的gradle构建脚本，通常这个文件中的内容是不需要修改的
7. gradle.properties：全局的gradle配置文件
8. gradlew和gradlew.bat：使用命令行界面执行gradle命令，前者是Linux或者Mac，后者是Win
9. HelloWorld.iml：iml文件是所有Intellij IDEA项目都会自动生成的一个文件，用于标识这是一个IntelliJ IDEA项目，无需修改
10. local.properties：用于指定本机中的Android SDK路径，通常内容是自动生成的
11. settings.gradle：用于指定项目中所有引入的模块，通常也是自动完成的

### APP目录结构：

1. build:包含一些在编译时自动产生的文件，不需要过多关心
2. libs: 如果使用第三方jar包，就需要把这些jar包放在对应的libs目录下，放在这个目录下的jar包会自动添加到该项目的构建路径里
3. AndroidTest：编写测试用例
4. java：存放代码的位置，会自动生成一个mainactivity文件
5. res：包含所有用到的资源，图片放在drawable中，布局放在layout中，字符串放在values中等等
6. AndroidManifest.xml：整个Android项目的配置文件
7. test：编写unit test测试用例
8. .gitignore文件：将APP模块内指定......
9. app.iml：intelliJ IDEA项目自动生成的文件
10. build.gradle: 构建脚本
11. proguard-rules.pro: 该文件用于指定项目代码的混淆规则，当代码开发完打包成安装包文件，如果不希望被别人破解，通常会将代码进行混淆，从而让破解者难以阅读

AndroidManifest.xml里面注册的activity才是有效的，其中intent-filter里面有两行代码：

```kotlin
<intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

表示MainActivity是这个项目的主activity，在手机上点击这个应用图标，首先启动的是这个activity

```kotlin
class MainActivity : AppCompatActivity() {
    // 继承来自AppCompatActivity，为AndroidX中提供向下兼容的一种activity
    // Activity类是Android系统提供的一种基类，所有自定义的activity都必须继承它或者它的子类才能拥有
    //Activity特性，AppCompatActivity是Activity的一个子类
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```

Android程序的设计讲究逻辑和视图分离，一般不在activity中直接编写界面，而是在布局文件中编写界面，而后在activity中引入进来。在onCreate()方法的第二行调用了setContentView()方法，这个方法给当前的Activity引入了一个activity_main布局

### res目录简介：

1. 以drawable开头的目录都是用来放图片的
2. 以mipmap开头的目录都是用来放应用图标
3. 以values开头的目录都是用来放字符串、样式、颜色等配置
4. 以layout开头的目录都是用来放布局文件的。

res/values/strings.xml文件:

```kotlin
<resources>
    <string name="app_name">My Application</string>
</resources>
```

1. 代码中通过R.string.app_name可以获得该字符串的引用；
2. 在XML中通过@string/app_name可以获得该字符串的引用。

若是引用图片资源则将string改为drawable，应用图标则改为mipmap，布局文件则为layout

### 使用log工具：

Android中的日志工具是Log(android.util.Log)

Log.v() -> verbose

Log.d() -> debug

Log.i() -> info

Log.w() -> warning

Log.e() -> error

```kotlin
Log.d("MainActivity", "onCreate execute")
```

Log.d传入了两个参数：第一个参数是tag，一般传入当前的类名，对打印信息过滤；第二个参数msg，即log内容

运行后会打印在logcat中



## CHAPTER_2_快速入门Kotlin语言

如何运行Kotlin代码：

1. 使用IntelliJ IDEA

2. 在线运行Kotlin代码

   [Kotlin在线网站]: https://try.kotlinlang.org

3. 使用Android Studio，随便打开一个Android项目，在里面编写一个Kotlin的main()函数，就可以独立运行

### 变量与函数

Kotlin中定义变量只允许在变量前声明两种关键字：val和var

1. val用来声明一个不可变的变量
2. var用来声明一个可变的变量

```kotlin
val a : Int = 10
```

显示声明变量a为int类型，Int首字母为大写，在Kotlin中Int变成一个类

```kotlin
fun methodName(param1 : Int, param2 : Int): Int{
	return 0
}
```

参数括号后面的那部分是可选的，用于声明该函数会返回声明类型的数据，若不需要返回任何数据，可直接不写

Android Studio代码补全功能

导入函数包

### 程序的逻辑控制

```kotlin
// if 语句
if(nums1 > nums2){
	value = nums1
}
else{
	value = nums2
}
```

```Kotlin
// when 语句 相当于switch
fun getScore(name: String) = when (name) {
    "Tom" -> 86
    "Jim" -> 77
    "Jack" -> 95
    "Lily" -> 100
    else -> 0
}

// 匹配值 -> {逻辑执行}
// when 允许类型匹配
fun checkNumber(num: Number) {
    when (num) {
    	is Int -> println("number is Int")
    	is Double -> println("number is Double")
    	else -> println("number not support")
    }
}
```

```Kotlin
// 循环语句
val range = 0..10 // [0,10]闭区间
val range1 = 0 until 10 // [0,10)
val range2 = 0 until 10 step 2  // 0 2 4 6 8
val range3 = 10 downTo 1 // 10 -> 1
for (i in 0..10)
{
    println(i)
}
```

### 面向对象编程

```kotlin
class Person{
	var name = ""
    var age = 0
    
    fun eat() {
        println(name + " is eating. He is " + age " years old.")
    }
}
val p = Person()
p.name = "Jack"
p.age = 19
p.eat()
```

#### 继承与构造函数

创建类student

```kotlin
class Student{
	var sno = ""
	var grade = 0
}
```

让Student类继承Person类，需要做:

1. 使Person类可以被继承，即在Person类前加关键字open

```kotlin
open class Person{
......
}
```

2. 让Student类继承Person类

```kotlin
class Student : Person(){
	......
}
```

主构造函数：没有函数体，直接定义在类名的后面

```kotlin
class Student(val sno:String, val grade:Int) : Person() {}
```

在主构造函数中引入逻辑，可在init结构体中写

```kotlin
class Student(val sno:String, val grade:Int) : Person() {
	init{
		println("sno is " + sno)
		println("grade is " + grade)
	}
}
```

Person类后面的空括号表示要去调用Person类中无参数的构造函数，但Person类如下改写后，Student类也需要改写：

```kotlin
open class Person(val name : String, val age : Int){}

class student(val sno: String, val grade : Int, name : String, age: Int):
	Person(name, age){
    ......
}
```

Student类的主构造函数必须加入name和age两个参数并传给Person类的构造函数

需要注意的是，student 类的主构造函数中不将name和age声明成val，是为了避免与父类中的字段冲突

次构造函数：有函数体，规定一个类既有主构造函数又有次构造函数时，所有次构造函数都必须调用主构造函数（包括间接调用）。

```kotlin
open class Person(val name : String, val age : Int){}

class student(val sno: String, val grade : Int, name : String, age: Int):
	Person(name, age){
    constructor(name: String, age : Int) : this("", 0, name, age){
        
    }
    constructor() : this("", 0){}
}
```

次构造函数通过constructor定义，可以如下构造

```kotlin
val student1 = Student()
val student2 = Student("Jack", 19)
val student3 = Student("a123", 5, "Jack", 19)
```

只有次构造函数，没有主构造函数，也是允许的

#### 接口

接口中的函数不要求有函数体：

```kotlin
interfaace Study {
	fun readBooks()
	fun doHomework()
}
```

接下来让Student类去实现Study接口，代码调整如下：

```kotlin
class Student(name : String, age : Int) : Person(name, age), Study {
	override fun readBooks(){
		println(name + " is reading.")
	}
	override fun doHomework(){
		println(name + " is doing homework.")
	}
}
```

接口的后面不需要加上括号，因为它没有构造函数去调用

Study接口中定义了两个待实现的函数，因此Student类中必须实现这两个函数，Kotlin中使用override关键字来重写父类或者实现接口中的函数

```kotlin
fun main(){
    val student = Student("Jack", 19)
    doStudy(student)
}
fun doStudy(study : Study) {
    study.readBooks()
    study.dohomework()
}
```

由于student类实现了Study接口，所以Student类的实例是可以传递给doStudy函数的

即面向接口编程，也称多态

Kotlin中允许对接口中定义的函数进行默认实现

Kotlin的可见性修饰符：public, private, protected和internal，直接定义在fun关键字的前面即可，默认为public

![image-20220921005322693](C:\Users\Hongji-Li\AppData\Roaming\Typora\typora-user-images\image-20220921005322693.png)

#### 数据类和单例类

数据类：用于将服务器端或数据库中的数据映射到内存中，为编程逻辑提供数据模型的支持

数据类通常需要重写equals(), hashCode(), toString()这几个方法

在类前声明了data关键字时，表明你希望这个类是一个数据类，Kotlin会根据主构造函数中的参数将上述方法自动生成

单例类：避免构建重复对象，若某个类在全局最多只拥有一个实例，则可以使用单例模式

在Kotlin中只需要将class关键字改成object

### lambda编程

List, Set和Map在Java中都是接口，List的主要实现类为ArrayList, LinkedList, Set的主要实现类为HashSet, Map的主要实现类是HashMap

```kotlin
val list = ArrayList<String>()
list.add("Apple")
```

Kotlin use a internal function called listOf() to simplify the process of initializing a list

```kotlin
val list = listOf("Apple", "Banana")
```

use for-in to through a list

listOf() is used to create a const list

then we have a function mutableListOf() to create a variable list

repetitive elements will only save one in set

Kotlin also provide mapOf() and mutableMapOf() to simplify the process of using hashMap

```kotlin
for((fruit, number) in map){
    ...
}
```

 grammar of lambda function:

{param1 : type1, param2 : type2  -> FunctionBody}

the last row of FunctionBody is thought to be a return value as a default

when lambda param is the last param, the lambda expression can be moved out of bracket

```kotlin
val maxLengthFruit = list.maxBy() {fruit : String -> fruit.length}
```

if lambda param is the only param, the bracket of function can be omit

```kotlin
val maxLengthFruit = list.maxBy {fruit : String -> fruit.length}
```

Finally, when there is only one param in lambda expression, we can use it to replace the param explanation

```kotlin
val maxLengthFruit = list.maxBy {it.length}
```

filter() function

API: any() use to judge whether any element is match condition in the list

API: all()

```kotlin
val anyResult = list.any {it.length <= 5}
val allResult = list.all {it.length <= 5}
```

Java thread class:

```Java
new Tread(new Runnable() {
	@Override
    public void run() {
        System.out.println("Thread is running");
    }
}).start();
```

Kotlin :

```kotlin
Thread(object : Runnable
	override fun run() {
		println("Thread is running")
	}
}).start()
```

### null pointer check

null pointer exception may cause android system to crash

Nullification is performed before some function is called

For Kotlin, all param and expression can not be null in default.

a "?" after typename means this param can be set to null

```kotlin
fun doStudy(study : Study ?){

}
```

but nullPointerException still need to be solved

operator (.?) is used to nullification

```kotlin
if(a != null){
    a.doSomething()
}

// is equal to below expression
a?.doSomething()
```

```kotlin
val c = a ?: b
// is equal to below expression
val c = if(a != null){a}
	else {b}
```



































## END_FILE(LOADING_BOOK_3_PAGES_101)

