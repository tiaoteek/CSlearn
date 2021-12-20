### Class01 引用 指针 内存

## 引用

### 1.   引用的定义

A **reference** is an alias for another variable. (**引用**就是另一个变量的别名)

### 2.   声明引用变量的方法

```c++
int x; 
int& rx = x;
```

或者

```c++
int x, &rx = x;
```

### 3.   引用的性质（非常重要）

- Any changes made through the reference variable are actually performed on the original variable (通过引用所做的读写操作实际上是作用于原变量上).
- A reference must be initialized in declaration 引用必须在声明的时候初始化。
- Once initialized, the name of the reference cannot be assigned to other variables (引用一旦初始化，引用名字就不能再指定给其它变量)

### 4.   引用类型做函数的参数：引用传递 

You can use a reference variable as a parameter in a function and pass a regular variable to invoke the function. (引用可做函数参数，但调用时只需传普通变量即可)

When you change the value through the reference variable, the original value is actually changed. (在被调函数中改变引用变量的值，则改变的是实参的值)

### 5.   例子

#### 5.1.    例1：通过值传参

```c++
//pass by value 
void swap(int x, int y){  
	int t;  t=x; x=y; y=t; } 
int main() {  
    int a=5, b{10};  
    cout << "Before: a=" << a << " b=" << b << endl;  
    swap( a, b );  
    cout << "After: a=" << a << "b=" << b << endl;  
    return 0; }
```

输出结果：

```
Before: a=5 b=10
After: a=5 b=10
```

#### 5.2.    例2：通过指针传参 

```c++
//pass by pointer 
void swap(int* x, int* y){  
    int t;  t=*x; *x=*y; *y=t; } 
int main() {  
    auto a{5}, b{10};  
    cout<< "Before: a=" << a << " b=" << b << endl;  
    swap( &a, &b );  
    cout<< "After: a=" << a << "b=" << b << endl;  
    return 0; }
```

输出结果：

```
Before: a=5 b=10
After: a=10 b=5
```

 

#### 5.3.    例3：通过引用传参

```c++
//pass by reference 
void swap(int& x, int& y){  
	int t;  t=x; x=y; y=t; } 
int main() {  
    auto a{5}, b{10};  
    cout<< "Before: a=" << a << " b=" << b << endl;  
    swap( a, b );  
    cout << "After: a=" << a << "b=" << b << endl;  
    return 0; }
```

输出结果：

```
Before: a=5 b=10
After: a=10 b=5
```

### 6.   引用的性质的补充说明

```c++
int a { 0 }, b { 1 }; 
int& r { a }; // 引用变量 r 在声明的同时就要初始化，r是a的别名  
r = 42; // 相当于 a = 42 
r = b;  // 相当于 a = b; 执行后 a 的值是1     
		// 此处不是让r变成b的引用     
		// 引用r声明并初始化后，r就不能再改为其它变量的引用 
int& r2 = a; // 继续给a起别名 
int& r3 = r; // 声明引用变量 r3，用r初始化        
			// 这个相当于 int& r3 = a; 因为 r 是 a 的别名
```

## 代码示例：引用变量、函数传参

### 1.   引用变量示例

**示例中展示“整型引用”**

```c++
int x = 0, &rx = x;
```

**示例中展示了“常量指针类型引用”**

```c++
const char* s = "Hello"; const char*& rs = s;
```

### 2.   函数传参

**示例中展示了三个swap函数**

```c++
void swap( int x, int y ); void swap( int* x, int* y ); void swap( int& x, int& y );
```

## 空指针和动态内存分配

### 1.   空指针

#### 1.1.    0带来的二义性问题

​	**1. C++03中，空指针使用“0”来表示。0既是一个常量整数，也是一个常量空指针。**

​	**2. C语言中，空指针使用(void *)0来表示**

​	**3. 有时候，用“NULL”来表示空指针(一种可能的实现方式是#define NULL 0)**

#### 1.2.    C++标准化委员会希望“空指针”是一个确定的东西。

​	**C++11中引入保留字“nullptr”作为空指针**

### 2.   动态内存管理：分配/释放 

#### 2.1.    C++中通过运算符new申请动态内存

```c++
new <类型名> (初值) ;   //申请一个变量的空间 new <类型名>[常量表达式] ;  //申请数组
```

​	**如果申请成功，返回指定类型内存的地址；** 

​	**如果申请失败，抛出异常，或者返回空指针(nullptr)。(C++11)**

#### 2.2.    动态内存使用完毕后，要用delete运算符来释放。

```c++
delete  <指针名>;  //删除一个变量/对象 delete [] <指针名>;   //删除数组空间
```



# Class02 数据类型与转换

## 布尔数据类型

### 1.   布尔类型的定义

布尔（英语：Boolean）是计算机科学中的逻辑数据类型，以发明布尔代数的数学家乔治·布尔为名。它只有两种值，通常是 **真** 和 **假**

C++语言在其标准化过程中引入了`bool`、`true`和`false`关键字，增加了原生数据类型来支持布尔数据。

布尔类型的大小（所占的存储空间）依赖于具体的编译器实现。也可以用 sizeof运算符得到其占用的空间。



### 2.   布尔类型的用途

布尔数据类型主要与条件语句相关。条件语句用来更改程序控制流。



### 3.   C++中的布尔类型

C++ keyword: **bool, true,  false**

命名时尽量以is开头。

**例如：**

```c++
bool isMyBook; 
bool isRunning = {false}; //C++11 列表初始化方式 
bool isBoy( ); 
```



### 4.   布尔类型与整型的转换

**转换规则：**

```
0  <-->  false       // 整数0和布尔false互相转化
true --> 1         // 布尔true转化为整数1
non-zero --> true   // 任意非0整数转化为布尔true
```

问题：'a' -->?  true

 

### 5.   关系运算得到布尔值

关系运算(Relational Operation)包括：**==, !=, <=, >=, <, >**

**例如**

```c++
int a=0, b={1}; //C++11 
3 == a; 
b < a; 
3.2 >= b;  
if (3 == a) {   
    // blah blah 
}
```

 

### 6.   逻辑运算得到布尔值

逻辑运算(Logical Operation)包括：&&, ||, !

```c++
int a={0}, b{1}; //C++11 
a && b; 
b || 18; 
!a;
```

 

```c++
while (!a) {
  // blah blah
}
```

### 7.   代码示例

```c++
#include <iostream> 
int main() {   
    bool isAlpha;   
    isAlpha = false;     
    if (!isAlpha) {    
        std::cout << "isAlpha=" << isAlpha << std::endl;    
        std::cout << std::boolalpha <<
            		"isAlpha=" << isAlpha << std::endl;   
    }   
    return 0; 
}
```

 

### 8.   编码规范

26. 布尔变量/函数的命名应使用前缀“is”

例如：isSet, isVisible, isFinished, isFound, isOpen

39. 断行必须很明显。

在逗号或运算符后换行，新行要对齐

