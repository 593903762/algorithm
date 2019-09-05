[TOC]

# 第四章、复合类型

## 4.2 字符串

- c 语言风格
- string 类型



```
char dog[8] = {'d', 'o', 'g'};		// 不是字符串string
char dog[8] = {'d', 'o', 'g', '\0'};		// 是字符串string
```

字符串需要包含空字符（ASCII码是0，'\0'）

[12]: https://www.runoob.com/python/python-func-zip.html



### 字符串常量（字符串字面值）

> 只用一个引号括起来的字符串



```
char dog[] = "dog";			// 字符串
```

隐式包含结尾的空字符，应该确保数组足够大，能够包含空字符



**字符常量 与 字符串**

```
char ch = 's';		// 字符常量
char ch = "s";		// 字符串，是错误的，会报错
```



-----

### 4.2.1 拼接字符串常量

**拼接字符串字面值**

> 用两个用引号括起来的字符串合并为一个
>
> 任何两个由空白（空格、制表符、换行符）分贝的字符串常量都自动拼接成一个



以下都是等价：

![1555048640882](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1555048640882.png)

第一个字符串的'\0'会被后面第一个字符取代



----

### 4.2.2 在数组中使用字符串

**字符串存储到数组中：（两种方式）**

- 将数组初始化为字符串常量
- 将键盘或文件读入数组中



```
#include<string.h>

int len = strlen(str);			// 用于确定字符串的长度，不包含空字符
```





----

### 4.2.3 字符串输入

cin使用空白（空格、制表符、换行符）确定字符串的结束为止

cin获取一个单词以后，自动在后面加上空字符，如果有多个单词，会留在缓冲区中，下一次输入直接赋值给cin对象



如果需要读取的数据中间存在空格，可以使用以下方式

---

### 4.2.4 每次读取一行字符串输入

isstream类提供类成员函数：

```
#include<istream>
```



读取一行输入

- getline（）——丢弃换行符
- get（）——将换行符保留在输入序列中



#### 1. getline

确定输入结尾：换行符

两个参数：

第一个——输入行的数组的名称；第二个——读取的字符数（包含了空字符，所以是n+1）

```
cin.getline(name, 20)

cin.getline(name1, 20).getline(name2, 20);
```

最多只能读取19个字符，将最后一个字符换行符转化为空字符



#### 2. get

不会丢弃换行符，如果是两个get连在一起，最后一个get会读取的是换行符

```
cin.get(name,20);
cin.get();		// 读取换行符
cin.get(name2,20);

也可以写成
cin.get(name,20).get();
```



#### 3. 空行和其他问题



----

### 4.2.5 混合输入字符串和数字



```
#include <iostream>
int main()
{
    using namespace std;
    cout << "What year was your house built?\n";
    int year;
    cin >> year;
    // cin.get();
    cout << "What is its street address?\n";
    char address[80];
    cin.getline(address, 80);
    cout << "Year built: " << year << endl;
    cout << "Address: " << address << endl;
    cout << "Done!\n";
    // cin.get();
    return 0; 
}
```

cin>> 输入后的换行符留在了缓冲区，所以后面的address得到的是换行符然后转化为空字符



![1555052406717](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1555052406717.png)



----

## 4.3 string

与字符数组**相同**：

- 使用c风格初始化string对象
- 使用cin将键盘中存储到string对象
- 使用cout显示string
- 使用数组访问string的字符

与字符数组**不同**：

- string为简单变量，可以进行 + - = 等操作
- string的大小自动处理

### 4.3.1 string初始化

```
string data = "the dog";
```





----

### 4.3.2 赋值、拼接、附加

- 不能将一个字符串数组赋值给一个string，但是可以将一个string 赋值给string

```
string s1,s2,s3;
s1 = s2 + s3;
s1 += s2;
```





### 4.3.3 string 操作

#### 确定长度

```
int len_string = str.size();
int lne_char = strlen(charr1);
```



#### 赋值=，判等==，+=

```
char charr1[20], charr2[20];
strcat(charr1, "dog");		// 拼接
strcpy(charr2, "dog");
```



### 4.3.4 string  的 I/O



对于string，使用getline(cin, str)

```
char charr1[20];
cin.getine(charr1, 20);			// 不会残留换行符

string str;
getline(cin, str);
```





### 4.3.5 其他形式的字符串字面值

原始字符串R，支持UTF-8编码，只有C++11支持

```
cout<<R("jim "kong" "\n" ");
```

显示

```
jim "kong" "\n"
```





## 4.7 指针和自由存储空间

>  oop：在运行阶段（不是在编译阶段）进行决策
>
> 运行阶段：程序正在运行——————运行阶段决策：取决于当前运行的状态
>
> 编译阶段：编译器将程序组合起来————编译阶段决策：取决于代码 （数组大小在编译前就设定好）

运行阶段决策提供了灵活性，可以根据当前情况调整。使用oop时，可以在运行阶段确定数组长度，但是语言必须允许程序在运行时进行创建数组

c++**采用关键字new请求正确数量的内存预计使用指针跟踪新分配的内存的位置**



### 4.7.1 声明和初始化指针



```
int g = 5;
int *pt = &g;
```

等价于

```
int g = 5;
int *pt ;
pt = & g;
```

程序将pt初始化为g的地址



---

### 4.7.2 指针的危险

**创建指针时，会分配用来存储地址的内存，但是不会分配用来存储指针所指向的数据的内存**

```
// illegal
long *pt;
*pt = 1000;
```

pt指向内存不明确



----

### 4.7.3 指针和数字

将数字值作为地址来使用，应通过强制类型转化将数字转换为适当的地址类型

```
int *pt;
pt = (int *)0xB80000000;
```

pt是int值的地址，并不意味着pt本身的类型是int，有些是2字节，有些是4字节



---

### 4.7.4 使用new来分配内存

指针：变量的地址，在运行阶段分配未命名的内存从而存储值

变量：在编译时分配的有名称的内存



1. 告诉new，需要为哪种数据类型分配内存
2. new将找到长度正确的内存块，返回内存块的地址
3. 将该内存块的地址赋值给一个指针

```
int *pn = new int;
```

new int 是存储 int 的内存，new根据类型确定需要多少字节的内存，找到这样 的内存以后，返回其地址。然后将地址赋值给pn， pn是声明为指向 int 类型的指针

**比较变量地址赋值 && new 赋值**

相同：都是将int 变量的地址赋值给指针

不同：new int 的pn指向的内存没有名称，pn是指向的是一个数据对象（数据项分配的内存块）

```
int *pn = new int ;			// 分配空间
*pn = 10000;
```



#### 堆和栈

new分配的内存块与常规变量声明的内存块不同

常规变量是放在栈中，new从heap堆中或者自由存储区的内存区分配内存

如果拆开来写的话

```
int *pt;	cout<<(int *)pt<<endl;  		// 0x1
pt = new int;cout<<(int *)pt<<endl;			// 0x1d...

int *pt;cout<<(int *)pt<<endl;
pt = (int*)malloc(sizeof(int));cout<<(int *)pt<<endl;
```

![1555334947907](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1555334947907.png)

所以，一旦使用了new或者malloc以后，指针的地址就会发生改变，因为分配到了地址内存就到了堆中



---

### 4.7.5 使用delete释放内存



```
int *pt = new int;
...

delete pt;
```

释放pt指向的内存，但不会删除pt本身，因此pt还可以重新指向另一个新分配的内存块

**1. 一定要配对使用new 和delete，不然会造成内存泄漏（memory leak）**

**2. 不要释放已经释放过的内存块**

**3. 不能用delete释放不是new生成的内存块**



```
int j = 6;
int *pt = &j;
delete pt;		// illegal
```







---

### 4.7.6 使用new创建动态数组

对于大型数据，（**数组、字符串、结构体**）应使用new

数组是否取决于运行时用户提供的信息，分为静态联编和动态联编

-  **静态联编（static binding）：** 如果通过声明创建数组，则程序被编译时将为数组分配内存空间，无论数组是否使用，都占用了内存 

- **动态联编（dynamic binding）：**使用new，在运行阶段需要数组，则创建该数组，如果不需要，就不创建。可以在程序运行时选择数组的长度。——数组是在程序运行时创建

#### 1.使用new创建动态数组

```
type_name *pointer_name  = new type_name [num_size];
```



1. 数组的元素类型
2. 元素数目

告诉new即可——必须在类型名后面加上括号

```
int *psome = new int [10];
```

new返回第一个元素的地址，赋值给psome



```
delete [] psome;
```

释放整个数组



#### new和delete的规则

1. 不使用delete释放不是new创建的 内存
2. 不使用delete释放同一个内存两次（两个指针指向同一个内存块也是）
3. 如果使用new[] 为数组分配内存，要使用delete[] 释放
4. 如果使用new[] 为一个实体分配内存，使用delete（无括号）释放
5. 对空指针NULL 使用delete释放是安全的

**不能使用sizeof 来确定动态分配 的数组包含的字节数**



#### 2. 使用动态数组

用psome[2] 访问数组中第3个元素



**数组名和指针的区别**

指针可以通过[]访问数据，可以进行+，-

数组名不能被修改，不能进行+ - 





---

## 4.8 指针、数组和指针算术



```
double wage[3];

double *pw = wage;		// wage[0]

cout<< *(wage+1)<<endl;		//wage[1]

cout<<sizeof(wage)<<endl;		// 24
cout<<sizeof(pw)<<endl;			// 4
```



**区别**

1. 数组名不能进行移动操作

```
pointer_name = pointer_name +1;		//valid
arrayname = arrayname + 1;		// invalide
```

2. sizeof：数组使用sizeof得到数组长度，指针使用sizeof得到指针的长度



**数组的地址**

- 数组名是数组第一个元素的地址
- 对数组名取地址是得到整个数组的地址





---

### 4.8.2 指针小节

 





----

### 4.8.3 指针和字符串



```
char f[10] = "rose";
cout<< f <<" yese"<<endl;
```

f是字符串第一个字符的地址，cout一直打印，知道遇见空字符



> 在cout和c++表达式中，char数组名，char指针，用引号括起来的字符串常量被解释为字符串第一个字符的地址



```
const char *ch = "abc";
cout<< ch;
```

可以使用ch访问字符串，但是不能修改ch，不能将它指向另外的字符串



1. 某些编译器将字符串字面值 看做制度常量，不能修改



```
char *ps;
char name[] = "animal";
ps = name;

// 相同的值，都是显示的地址
cout<<(int *)name<<endl;
cout<<(int *)ps<<endl;

ps = new char[strlen(name) +1];
```



```
strcpy(des, src);

strncpy(des, src, num);
```





----

### 4.8.4 使用new创建动态结构



#### 1. 使用new和delete

为了避免声明过大的字符数组，可以使用new

```
char* getname()
{
    char tmp[80];
    cin>>tmp;
    char *pn = new char[strlen(tmp) + 1];		// 空字符算
    strcpy(pn, tmp);
    
    return pn;
}
// 可以在一个函数中声明，在另外一个函数中释放
int main()
{
    char *name;
    
    name = getname(); cout<< name;  delete name;
    name = getname(); cout<< name;  delete name;
     
    return 0;
}
```





----

### 4.8.5 自动存储、静态存储、动态存储

三种管理数据存储的方式

- 自动变量——栈中
- 静态变量——

#### 1. 自动存储（automatic variable）

存储在栈中，执行代码时，其中的变量加入到栈中，离开代码块，按照相反的顺序释放这些变量，后进先出（LIFO）

>  所属的函数调用时自动产生，函数结束时消亡



例如上面的tmp数组，只有getname函数活动时才存在，一旦回到main，内存就自动释放

>  自动变量是一个局部变量，作用域是包含他的代码块（在花括号的一段代码）





#### 2. 静态存储

> 整个程序执行期间都存在

静态的两种方式：

1. 在函数外面定义
2. 在声明时使用关键字static



**与自动存储的关键：限制了变量的寿命，变量可能存在与整个生命周期（静态变量），可能只在特定函数被执行（自动变量）**



#### 3. 动态存储

new和delete管理了一个内存池，——**自由存储空间（free store） 或者 堆（heap）**

内存池用于静态变量和自动变量的内存是分开，可以在一个函数中声明，在另外一个函数中释放

使得数据的生命周期不完全受到程序或函数的生存时间控制



#### 栈、堆、内存泄漏

new在堆上面创建以后没有使用delete，即使指针的内存由于作用域被释放，但是内存空间将继续存在，并且将无法再访问这一个内存块，因为指向这个内存块的指针失效了，

这将导致内存泄漏，泄漏的内存在程序的整个生命周期都不可使用







---

## 4.10数组的替代品

### 4.10.1 vector



```
#include

vector<int> vi;

vector<double> vd[n];
```



---

### 4.10.2 array

长度固定，使用栈（静态存储）

比数组更安全，方便

可以将一个数组赋值给另外一个数组

```
#include<array>

array<int ,5> ai;

array<double, 4> ad = {1.2, 3.2};
```









# 第九章 内存模型和名称空间

## 9.2 存储持续性、作用域、链接性

c++的三种存储数据的方式：

1. 自动存储持续性：在函数定义中声明的变量（包括函数参数）的存储持续性是自动的——在程序开始执行时（函数或者代码块）被创建，执行完函数或者代码块内存被释放——作用域：局部
2. 静态存储持续性：1）在函数定义外定义的变量；2）static定义的变量——在整个程序运行中都存在
3. 动态存储持续性：用new分配的内存，直至使用delete释放——存放在堆中或者自由存储空间

这些方案的区别在于：数据保留在内存中的时间



------

### 9.2.1 作用域和链接

作用域（scope）：在函数中可见，可以被使用

链接性（linkage）：名称在不同单元间共享。链接性为外部名称可以在文件之间共享，链接性为内部名称只能在一个文件的函数共享——自动变量没有链接性，不能共享





------

### 9.2.2 自动存储持续性

默认情况下，函数中声明的参数和变量是自动存储性，作用域为局部，没链接性

在main和其他函数中声明的同一个变量可以使用，相互不影响，一个是内部变量，一个是外部变量，并且存储的空间不一样



#### atuo——自动类型

> 指出当前变量为局部自动变量

1. 自动变量的初始化

2. 自动变量和栈

3. 寄存器变量——register

> 提高访问变量的速度，显示的指出变量是自动的







---

### 9.2.3 静态持续变量

静态存储持续性提供的3种链接性：——

1. 外部链接性（可以在其他文件中访问）——在代码块外面声明
2. 内部链接性（只能在当前文件中访问—）——在代码块外面声明，并且使用static限定符
3. 无链接性（只能在当前函数或者代码块访问）——在代码块内声明，使用static

> 比自动变量寿命更长
>
> 不使用栈管理，编译器分配固定的内存块存储所有的静态变量
>
> 在整个执行期间一直存在

![1555140287343](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1555140287343.png)





---

### 9.2.4 静态持续性、外部链接性

> 外部变量：链接性为外部，存储持续性为静态，作用域为整个文件



#### 变量声明

1. 定义声明（definition）：给变量分配空间
2. 引用声明（declaration）：不给变量分配空间，使用extern，且不进行初始化

![1555140578011](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1555140578011.png)

gr不是引用声明

**在多个文件使用外部变量，只需要在一个文件中包含该变量的定义，但是在使用改变量的其他所有文件都必须使用extern声明**

![1555140772304](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1555140772304.png)

02cpp不能访问fleas





# 结构体

[结构体]: <https://www.runoob.com/cprogramming/c-structures.html>

## 使用malloc创建结构体

预先不知道数组长度，使用动态数组

c语言实现动态数组，使用`malloc`和`realloc`



```
struct student_info
{
	int score;
	int local_rank;
	int final_rank;
	int local_id;
	char id[14];
}stu[30001];

scanf("%s",stu[0]);


struct student_info
{
	int score;
	int local_rank;
	int final_rank;
	int local_id;
	char id[14];
}stu[30001];
```

在定义结构体数组的时候，不能加上typedef



### 结构体数组

```
//1
struct student
{
    int num;
    ....

}stu[3];

//2
struct
{
    int num;
    　...
}stu[3];

//3
struct student
{
    int num;
   
};
struct student stu[3];
```



----

# 注意点：

## 1.输入输出

### 1. cin>>

最后的换行符会留在缓冲区中

在使用getline之前最好是清空缓冲区，不然会读入残留的换行符





# typedef

用 **typedef** 为数组去别名：

```
typedef int A[6];
```

表示用 **A** 代替 **int [6]**。

即：**A a;** 等于 **int a[6];**



## **typedef 与 #define 的区别**

（1）#define可以使用其他类型说明符对宏类型名进行扩展，但对 typedef 所定义的类型名却不能这样做。例如：

```
#define INTERGE int;
unsigned INTERGE n;  //没问题
typedef int INTERGE;
unsigned INTERGE n;  //错误，不能在 INTERGE 前面添加 unsigned
```

（2） 在连续定义几个变量的时候，typedef 能够保证定义的所有变量均为同一类型，而 #define 则无法保证。例如：

```
#define PTR_INT int *
PTR_INT p1, p2;        //p1、p2 类型不相同，宏展开后变为int *p1, p2;
typedef int * PTR_INT
PTR_INT p1, p2;        //p1、p2 类型相同，它们都是指向 int 类型的指针。
```



## 2.字符串

### 1.string在结构体中的创建

```
#include <iostream>
#include <string>
#include <cstdio>
using namespace std;
typedef struct node{
	string str;
}NODE;

int main(){
    string var = "lirao";
    NODE * node = (NODE *)malloc (sizeof(NODE));
    node->str = var;
}
```

​	对于这个程序，在程序调试过程中，在程序的最后一行是无论如何都过不了的。出现的错误就是内存访问冲突。但是如果我们把malloc分配的内存改为new分配，NODE*node = new NODE()，问题立马就解决了，这是为什么呢？

>  只是因为在NODE 结构中包含了string类型成员，用malloc分配时，由于malloc没有这样的机制，导致无法调用string的构造函数，所以无法构建起string对象，给一个不存在的对象赋值肯定错误。但是new分配内存时有这样的机制，调用了string的构造函数，所以就构建起了对象，内存访问冲突就不会发生了。







## c++中的auto在for循环使用

1. auto的使用 
   c++11引入了auto类型说明符，auto让编译器通过初始值来推算变量的类型，所以auto定义的变量必须有初始值。 
   使用auto也能在一条语句中声明多个变量，因为一条声明语句只能有一个基本数据类型，所以该语句中所有变量的初始基本数据类型都必须一样： 
   eg: auto i=0,*p=& i; //正确 auto sz=0,pi=3.14;//错误，sz和pi的类型不一样。
2. 范围for循环，遍历给定序列中的每个元素并对序列中的每个值执行某种操作。

```
for(declaration:expression)
    statement
```

>  expression 部分是一个对象，用于表示一个序列，declaration部分负责定义一个变量，该变量被用于访问序列中的基础元素，每次迭代declaration部分的变量会被初始化为expression部分的下一个元素值。



```
string s("hello,world");
for(auto &c:s);//对于s中的每个字符，c是一个引用，赋值语句将会改变s中字符的值
    c=toupper(c);
cout<<s<<endl
```



## 3.内存管理

>  堆和栈的区别

一个由C/C++编译的程序占用的内存分为以下几个部分
1、栈区（stack）— 由编译器自动分配释放 ，存放**函数的参数值**，**局部变量**的值等。其操作方式类似于数据结构中的栈。
2、堆区（heap） — 一般由**程序员**分配释放， 若程序员不释放，程序结束时可能由OS回收 。注意它与数据结构中的堆是两回事，分配方式倒是类似于链表，呵呵。**用malloc和new分配的空间都是在堆**
3、全局区（静态区）（static）—，全局变量和静态变量的存储是放在一块的，初始化的全局变量和静态变量在一块区域， 未初始化的全局变量和未初始化的静态变量在相邻的另一块区域。 - 程序结束后由系统释放。
4、文字常量区 —常量字符串就是放在这里的。 程序结束后由系统释放
5、程序代码区—存放函数体的二进制代码。

```
//main.cpp 
int a = 0; 全局初始化区 
char *p1; 全局未初始化区 
main() 
{ 
int b; 栈 
char s[] = "abc"; 栈 
char *p2; 栈 
char *p3 = "123456"; 123456\0在常量区，p3在栈上。 
static int c =0； 全局（静态）初始化区 
p1 = (char *)malloc(10); 
p2 = (char *)malloc(20); 
分配得来得10和20字节的区域就在堆区。 
strcpy(p1, "123456"); 123456\0放在常量区，编译器可能会将它与p3所指向的"123456"
优化成一个地方。 
}
```



## 使用技巧

## 数组

### 1. 求数组的长度

```
int a[]={1,2,3};
int len = sizeof(a)/sizeof(int);		// 3
```

但是，将数组作为参数传入到函数中时，函数只能看见最前面两个元素

```
int getlen(int arr[])
{
	return  sizeof(arr)/sizeof(int);
}
int main()
{
	int a[]={1,2,3};
	int len = getlen(a);
	cout<<len<<endl;		// 2
	
	return 0;
}
```

### 2.动态数组的创建

对于比较大的数组，可以在main外面声明，然后在main里面或者函数里面创建或者赋值

```
vector<vector<int> > visited;
int main()
{
	visited = vector<vector<int> >(nx ,vector<int>(ny, 0));
}
```



### 2. memset 、memcpy

#### memset

- 对数组——**常量数组**与 **字符串数组**都可以进行初始化

```
#include<string.h>
memset(arr,0,sizeof(arr));
```

只能对-1和0进行初始化



- 对结构体

```
struct sample_struct{
    char
    int ...
    
}stTest,Test[10];
memset(&stTest, 0, sizeof(sample_struct));
memset(Test, 0, sizeof(sample_struct)*10);
```



```
memset(void *s, int ch,size_t n);
```

ch实际范围是0--255

int a[5]赋值**memset（a,-1,sizeof(int )*5）**与**memset（a,511,sizeof(int )*5）** 所赋值的结果是一样的都为-1；因为-1的二进制码为（11111111 11111111 11111111 11111111）而511的二进制码为（00000000 00000000 00000001 11111111）后八位都为（11111111)

memset只是对最后8位进行

#### memcpy

```
memcpy(to, from, num);
```



```
#include<string.h>
int to[],from[];
// 从from拷贝k个元素给to
memcpy(to,from, sizeof(int)*k)

// 全部拷贝
memcpy(to,from, sizeof(from));

// 从from的第4个位置拷贝k个元素到to的第3个位置后面
memset(to+3, from+3, sizeof(int)*k);

char test[]="a,b,c,d,e,f,g,h,i";
char test_1[]="1,2,3,4,5,6";
memcpy(test+3,test_1, 6);
// 结果
// a,b,c,1,2,3,4,5,6
```



```
    char* s="GoldenGlobalView";
    char d[20];
    clrscr();
    memcpy(d,s,(strlen(s)+1));		//+1 是为了将字符串后面的'\0'字符结尾符放进来，去掉+1可能出现乱码
    memcpy(d,s+12,4);		//从第13个字符(V)开始复制，连续复制4个字符(View)
```

1、复制的内容不同。[strcpy](https://baike.baidu.com/item/strcpy)只能复制[字符串](https://baike.baidu.com/item/%E5%AD%97%E7%AC%A6%E4%B8%B2)，而memcpy可以复制任意内容，例如[字符数组](https://baike.baidu.com/item/%E5%AD%97%E7%AC%A6%E6%95%B0%E7%BB%84)、整型、[结构体](https://baike.baidu.com/item/%E7%BB%93%E6%9E%84%E4%BD%93)、类等。

2、复制的方法不同。strcpy不需要指定长度，它遇到被复制字符的串结束符"\0"才结束，所以容易溢出。memcpy则是根据其第3个参数决定复制的长度。

3、用途不同。通常在复制字符串时用strcpy，而需要复制其他类型数据时则一般用memcpy





# 踩过的坑

## 内存分配

### 1. 用malloc去分配string类型

```
using namespace std;

typedef  string elemtype;
struct _node
{
	elemtype str;
	struct _node *left, *right;
};
typedef struct _node node;

// 在以root为根的地方插入节点 
// 返回的是插入的位置,root是根节点
node* insert( elemtype s, struct _node *root)
{
	if(root==NULL)
	{	// root = (node*)malloc(sizeof(node));是错误的，malloc不能分配string
// 并且，这里不能写成 node* root = new node();不然会认为是重新分配的root，我们是需要给当前为空 的root分配空间
		root = new node();  cout<<"creat"<<endl;
		root->str += s;  cout<<"creat s: "<<s<<endl;
		root->right =NULL;
		root->left = NULL;
	}else
	{
		cout<<"the now root is: "<<root->str<<endl;
		if(s > root->str) 
		{
			cout<<"insert right"<<endl;
			root->right =  insert(s,root->right);
		}
		else if(s < root->str )  
		{
			cout<<"insert left"<<endl;  
			if(root->left==NULL)cout<<"the root->left == NULL"<<endl;
			else cout<<"the root->left="<<root->left->str<<endl;
			root->left = insert( s, root->left);
		}
	}
	
	return root;
}  
int main()
{
	struct _node *root = NULL;
	string s;
	string s1[2]= {"Jan", "Feb"};cout<<"s1[0]: "<< s1[0]<<endl;
	root = insert( s1[0], root);
	cout<<"mian root is: "<<root->str<<endl;
	cout<<"insert the node is: "<<s1[1]<<endl;
	root  = insert( s1[1], root);
	cout<<root->str<<" "<<root->left->str<<" "<<endl;
	return 0;
}
```



### 2.先声明指针，再分配地址，指针的地址会改变

```
typedef  string elemtype;
struct _node
{
	elemtype str;
	struct _node *left, *right;
};
typedef struct _node node;

// 在以root为根的地方插入节点 
// 返回的是插入的位置,root是根节点
node* insert( elemtype s, struct _node *root)
{
		// 先找到要插入的位置,也要找到pos上面的一个节点 
		node *pos = root, *mark;mark = root;
		while(pos!=NULL)
		{
			if(s < pos->str){mark = pos; pos = pos->left;}
			else {mark = pos; pos = pos->right;}
		}
		node *newnode  = new node();  cout<<"creat"<<endl;
// 用pos = newnode 那么此时pos和mark的指向不会相同了
		newnode->str = s;  cout<<"creat s: "<<s<<endl;
		newnode->right =NULL;	newnode->left = NULL;
		if( mark == pos) { return  root = newnode; }		// 创建的是根节点 
		else if( mark->str > s){cout<<">";mark->left = newnode;}
		else {cout<<"<";mark->right = newnode;}
		
	cout<<"mark: "<<mark->str<<endl;	
	return root;
}  
int main()
{
	struct _node *root = NULL;
	string s;
	string s1[2]= {"Jan", "Feb"};cout<<"s1[0]: "<< s1[0]<<endl;
	root = insert( s1[0], root);
	cout<<"mian root is: "<<root->str<<endl;
	cout<<"insert the node is: "<<s1[1]<<endl;
	root  = insert( s1[1], root);
	cout<<root->str<<" "<<root->left->str<<" "<<endl;
	return 0;
}

```

`14行`初始状态下pos和mark地址都是00，如果用pos去指向newnode的话，pos和mark指向将会不同

此外，如果不创建newnode，而是直接用`pos =new node()`，这样也会导致pos和mark指向不同





# 一些总结

### 1. malloc函数使用

用c语言写的程序在电脑中所占用的内存系统会不会自动清理，当该程序运行后，那些定义的变量，在电脑上占用的内存怎么办，是不是要手动清理，还是系统会帮忙清理？  

- 如果在C中使用malloc申请的空间没有用free释放的，在程序运行是系统不会清理，这样如果运行时间长了，可能会导致内存不足的现象，但程序退出时后所有程序使用的资源系统都会回收。
- 自动变量只要超出它的作用域范围就会由系统回收再利用。

因此，所有对于使用malloc申请的空间在使用完一定要释放。

### 2.自动变量与静态变量的区别

**区别1：**

- 静态局部变量在静态存储区内分配存储单元。在程序整个运行期间都不释放。
- 自动变量（即动态局部变量）属于动态存储类别，存储在动态存储区空间(而不是静态存储区空间)，函数调用结束后即释放。

**区别2：**

- 为静态局部变量赋初值是在编译时进行值的，即只赋初值一次，在程序运行时它已有初值。以后每次调用函数时不再重新赋初值而只是保留上次函数调用结束时的值。
- 为自动变量赋初值，不是在编译时进行的，而是在函数调用时进行，每调用一次函数重新给一次初值，相当于执行一次赋值语句。

**区别3：**

- 如果在定义局部变量时不赋初值的话，对静态局部变量来说，编译时自动赋初值0(对数值型变量)或空字符(对字符型变量)。
- 对自动变量来说，如果不赋初值，则它的值是一个不确定的值。这是由于每次函数调用结束后存储单元已释放，下次调用时又重新另分配存储单元，而所分配的单元中的值是不确定的。

另外，需要注意的是，虽然静态局部变量在函数调用结束后仍然存在，但其他函数是不能引用它的，也就是说，在其他函数中它是“不可见”的。