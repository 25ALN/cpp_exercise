## 链表
### 插入链表
- 头插法
```c
struct List*creatlist(struct List*head){  //头插法，将数据从头开始插入链表
    struct List *prv=NULL;
    int n,x;
    head=(struct List*)malloc(sizeof(struct List));
    head->next=NULL;
    scanf("%d",&n);
    while(n>0){
        prv=(struct List*)malloc(sizeof(struct List));
        scanf("%d",&x);
        prv->val=x;
        prv->next=head->next;
        head->next=prv;
        n--;
    }
    head=head->next;
    return head;
}
```

### 反转链表
```c
Node* list_reverse(Node* head){
   Node*pre,*cur,*next;
   cur=head;
   pre=NULL,next=NULL;
   while(cur!=NULL){
      next=cur->next; // 保存下一个节点
      cur->next=pre;  // 反转当前节点的指针
      pre=cur;        // 将prev指针移动到当前节点
      cur=next;       // 将curr指针移动到下一个节点
   }
   return pre;
}
// pre即为新链表的头指针
```

### 递归删除某个节点
```c
struct ListNode* deleteNode(struct ListNode* head, int val){
   if(NULL == head) {
      return head;
   }
   head->next = deleteNode(head->next, val);
   return head->val == val ? head->next : head;
}
```

### 逆序输入链表
```c
struct ListNode *Createlist(int n) {
    struct ListNode *head = NULL;
    int value;
    for (int i = 0; i < n; i++) {
        scanf("%d", &value);
        struct ListNode *new_node = (struct ListNode*)malloc(sizeof(struct ListNode));
        new_node->data = value;
        new_node->next = head;
        head = new_node;
    }
    return head;
}
```

## 辗转相除法
```c
#include <stdio.h>

int main()
{    
  int a,b,t;
  scanf("%d %d",&a,&b);
  while(b!=0){
  	t=a%b;
	a=b;
	b=t; 
  } 
  printf("%d",a);
}
```
## qsort排序(要引用stdlib头文件)
```c
int cmp(const void * a, const void * b)
{
   return ( *(int*)a - *(int*)b );
}
int main()
{
   int n;
   for( n = 0 ; n < 5; n++ ) {
      printf("%d ", values[n]);
   }
   qsort(values, 5, sizeof(int), cmp);
   return 0;
}
```
- 函数原型
```c
void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *));
```
- base: 指向待排序数组的第一个元素的指针。
- nitems: 数组中的元素数量。
- size: 数组中每个元素的大小（以字节为单位）。
- compar: 比较函数的指针，该函数用于比较两个元素。比较函数应当返回一个整数，表示比较结果：
- 小于零：表示第一个元素小于第二个元素。
-等于零：表示两个元素相等。
-大于零：表示第一个元素大于第二个元素。

## memset
```c
void *memset(void *str, int c, size_t n)
```
参数
- str -- 指向要填充的内存区域的指针。
- c -- 要设置的值，通常是一个无符号字符。
- n -- 要被设置为该值的字节数。

## memmove
```c
void *memmove(void *str1, const void *str2, size_t n)
```
从 str2 复制 n 个字符到 str1，但是在重叠内存块这方面，memmove() 是比 memcpy() 更安全的方法。
如果目标区域和源区域有重叠的话，memmove() 能够保证源串在被覆盖之前将重叠区域的字节拷贝到目标区域中，
复制后源区域的内容会被更改。如果目标区域与源区域没有重叠，则和 memcpy() 函数功能相同。

## calloc与malloc,realloc
C 库函数 void *calloc(size_t nitems, size_t size) 分配所需的内存空间，并返回一个指向它的指针。
malloc 和 calloc 之间的不同点是，malloc 不会设置内存为零，而 calloc 会设置分配的内存为零。
- nitems -- 要被分配的元素个数。
- size -- 元素的大小。

_注意_ ：calloc() 函数将分配的内存全部初始化为零。如果不需要初始化，可以使用 malloc() 函数代替。
另外，使用 calloc() 函数时需要注意，如果分配的内存块过大，可能会导致内存不足的问题。
因此在利用哈希时数据较大时可以使用calloc分配内存空间（力扣2958）。

realloc使用时需要有一个参数来接受返回值,例如
```c
int *temp;
temp=(int *)realloc(ans,sizeof(int)*5);
if(temp==NULL){
   free(ans);
   printf("fail");
}
ans=temp;
```

## getopt
```c
#include<unistd.h>
#include<getopt.h>  
int getopt(int argc, char * const argv[], const char *optstring);
```
char*optstring = “ab:c::”;
单个字符a         表示选项a没有参数            格式：-a即可，不加参数
单字符加冒号b:     表示选项b有且必须加参数      格式：-b 100或-b100,但-b=100错
单字符加2冒号c::   表示选项c可以有，也可以无     格式：-c200，其它格式错误

## tolower与toupper
```c
tolower //大写字母转小写
toupper //小写字母转大写
```

## color
- 字背景颜色范围:40 - 49      - 字颜色:30 - 39
40:黑                         30:黑
41:深红                       31:红
42:绿                         32:绿
43:黄色                       33:黄
44:蓝色                       34:蓝色
45:紫色                       35:紫色
46:深绿                       36:深绿
47:白色                       37:白色

1：粗体 4：下划线 
- 格式
```c
 "\033[ ; m 内容 \033[0m " 

```
## 缩进
- Ctrl + Shift + I 向后缩进 
- tab 

## &&
```
注意先判断左边再判断右边，在数组中反过来可能会遇到越界的问题
比如 if(p1>=0&&nums1[p1]>nums2[p2])不可反过来写

```
## INT_MIN 与 INT_MAX
```
二者都是宏定义,使用时需包含 #include <limits.h>  
INT_MIN 表示 int 类型能够表示的最小（最负）值,
INT_MAX 表示 int 类型能够表示的最大（最正）值。

```
## atoi
C 库函数 int atoi(const char *str) 把参数 str 所指向的字符串转换为一个整数（类型为 int 型）。

## 生成随机数
```c
int main(){
    int num;
    srand(time(NULL));
    for(int i=0;i<5;i++){
        num=random();
        printf("%d ",num%11);
    }
    return 0;
}
```
random是linux专用，它比rand质量更好

## 归并排序
vx.c中3535～3575

## c++
### 基础概念
- 对象
一块能存储数据并具有某种类型的内存空间
初始化与赋值是不同的，尽量都将数据初始化避免一些不必要的麻烦
也可用 extern来定义一个变量就不用初始化了，注意变量只能被定义一次，但是可以被多次声明
- 定义引用
int i=1;
int &j=i; 可以认为j是i的另外一个名字
i与j的类型必须相同且像 int &j=1;这种是无效的必须是个对象
- 隐式与显式
隐式:通常是指编译器自动进行某些操作，而不需要显式地调用或指定。(例如类型转换)
显式:指程序员明确地指定某些操作或行为(利用explicit关键字)
- 有地址的变量就是左值，没有地址的字面值、临时值就是右值
- 完美转发
std::forward被称为完美转发，它的作用是保持原来的值属性不变。通俗的讲就是，如果原来的值是左值，
经std::forward处理后该值还是左值；如果原来的值是右值，经std::forward处理后它还是右值
- std::move
可以将左值转化为右值
### 函数
若函数有多个参数，但只传入了少于该函数的参数个数，该函数后面的参数为默认值
- 重载函数(main函数除外)
几个函数名字相同但参数列表不同
### 输入与输出
- 输入
cin >> 直接跟上变量
他在读取字符串时以空格，换行，制表符来确定字符串结束的位置
cout << 后面若是普通的字符串需要双引号，若是变量则不需要
换行可采用c语言中的\n或是 << endl
- const
如果想在多个文件之间共享const对象，必须在变量的定义前加extern
类型	         作用位置	    可修改指针地址	可修改指向内容
顶层 const	   变量本身	      不可修改	   可修改
底层  const	   指向的内容	   可修改	      不可修改
顶层+底层 const 指针+指向内容	 不可修改	    不可修改
### 显示不同进制的控制符
dec 10进制
hex 16进制
oct 8进制
在修改格式前原来的格式一直存在
用法实例
```cpp
int main(){
   using namespace std;
   int x=42;
   cout << x <<endl; //输出42
   cout << hex;      //转化为16进制
   cout << x;        //输出2a
   cout << oct;      //转化为8进制
   cout << x;        //输出52
}
```
### 保留小数
- setprecision() + fixed（常用）
```c
double num=3.41341;
cout << fixed << setprecision() << num;
```
括号中的数字就是保留的位数，2就是保留两位小数
- printf（与c完全相同）
- round() (当需要实际保留相应的位数并进行计算时用)
使用时加上 #include <cmath> 头文件
```c
double num = 3.1415926535;
double rounded = round(num * 100.0) / 100.0;  // 保留两位小数
cout << rounded << endl;
```
### 一些常用函数
- auto
类型说明符
- cout.put()
用于输出一个字符
char ch；
cout.put(ch);
- getline 与 get
getline读取输入后将丢弃换行符，get则保留
getline有两个参数，第一个是存字符串的数组名，第二个是字符数

习惯用const来替换调c语言中的#define
static_cast<> 比传统强制类型转换更严格
auto还可自动识别类型

- unordered_map
```c
#include <unordered_map>
std::unordered_map<key_type, value_type> map_name;
//key_type 是键的类型。
//value_type 是值的类型。
```
其中每个键值都是唯一的
- std::min_element 
是一个用于查找范围内最小元素的标准库算法，位于 <algorithm> 头文件中。
```c
auto minIt = std::min_element(vec.begin(), vec.end());
```

- Lambda 表达式
一种匿名函数（没有名字的函数）
```c
[capture](parameter_list) -> return_type { function_body }
```
各个部分含义
部分	               含义	                  备注
[]	            捕获列表，捕获外部变量	      可以捕获局部变量、对象成员等
(parameter_list)	参数列表，类似于普通函数	   可以省略参数
-> return_type 	返回类型	            如果能推断，可以省略
{ function_body }	函数体，执行逻辑  	   必须写在花括号中

- std::function
类模版std::function是一种通用、多态的函数封装。std::function的实例可以对任何可以调用的目标实体
进行存储、复制、和调用操作，这些目标实体包括普通函数、Lambda表达式、函数指针、以及其它函数对象等
std::function对象最大的用处就是在实现函数回调
#### string类
可以互相拼接，赋值(用+，-，=)
string赋值方法详见c++ p书321页
- size()：返回字符串的长度。
- empty()：检查字符串是否为空。
- operator[]：通过索引访问字符串中的字符。
- substr()：获取子字符串。
例如：string x=str.substr(1,4),x将获取到str下标从1开始的四个字符

- find()：查找子字符串在主字符串中的位置。
若找到了返回第一个字符出现的下标，反之返回-1
例如：
```cpp
#include <string>
int main(){
   string x="hello";
   string y="ell";
   int out=x.find(y);
   //out输出的值将为1
   return 0;
}
```
- replace()：替换字符串中的某些字符。
std::string::npos 的值通常是 -1 或 ~0（即所有位都为 1），在实际中它是一个无符号整数的最大值 (std::string::size_type)。
它的作用是指示未找到的情况。是一个特殊的常量
在 std::string::find() 等查找函数中，如果目标子字符串不存在，就会返回 std::string::npos。
- 搜索操作(例如查找字符串位置的)
见c++书 325页

#### std::ranges::sort(排序函数) 
**不支持原生数组，只能对像vector,list这样的容器进行排序**
```c
std::ranges::sort(range, comparator, projection);
```
- range
需要排序的范围，可以是数组、向量 (std::vector)、列表 (std::list) 等容器。
- comparator（可选）
自定义比较函数，用于指定排序的方式，类似于 std::sort 的第三个参数。默认为 std::ranges::less，即升序排序。
若想降序排列则将此参数设为 std::ranges::greater{}
- projection（可选）
投影函数，用于对元素进行预处理后再进行比较。它类似于对数据执行某种转换再排序的过程。
经典的投影函数 **[](auto& t) { return t[0]; }**(其实就是一个lambda)
当有一个二维数组，想以每个元素的第一个数进行排序时，就加入这个投影函数

#### lambda(如果在一两个地方使用的简单操作使用它比函数更好)
- [capture](parameters) -> return_type { body }
[capture]：捕获外部变量的方式。
[=]是值捕获，不会改变值或是获取到改变的值；[&]引用捕获，字面意思
(parameters)：参数列表（可以省略）。
-> return_type：返回类型（通常可以省略）。
{ body }：函数体。

### vector(容器)
{}代表着赋值,()则是一种初始化；
不能通过下标去进行初始化，应当使用push_back()，或者使用emplace_back()(这个相比于push_back是原地构造，效率较高)
- insert(用于在指定位置插入元素，非常的灵活)
```c

int main(){
   list<int> L;
   for(size_t i=1;i<=5;i++){
      L.push_front(i);//依次将元素插入到头部
   }
   auto pos=L.begin();
   advance(pos,3); //(此函数可将迭代器向前或向后移动相应的步数)
   L.insert(pos,42);//(代表着在pos位置处插入42这个数字)
   for(auto &x:L){
      cout << x <<" ";
   }
   return 0;
}
```

#### 去重操作
```c
vector<int > nums{3, 1, 2, 3, 2, 1, 4};
   std::sort(nums.begin(),nums.end());
   for(auto &i:nums){
      cout<<i<<" ";
   }
   auto last=std::unique(nums.begin(),nums.end()); //将重复元素移动到最后
   nums.erase(last,nums.end()); //去除调重复元素
```    


#### 删除操作
forward list 有特殊版本的 erase,参见9.3.4节(第312页)。
forward_list 不支持 pop_back; vector 和 string 不支持 pop_front。
c.pop_back() 删除中尾元素。若为空,则函数行为未定义。函数返回void
c.pop_front() 删除c中首元素。若为空,则函数行为未定义。函数返回void
c.erase (p) 删除迭代器 p所指定的元素,返回一个指向被删元素之后元素的迭代器,若p指向尾元素
,则返回尾后(off-the-end)迭代器。若是尾后迭代器,则函数行为未定义
c.erase (b,e) 删除迭代器和e所指定范围内的元素。返回一个指向最后一个被删元素之后元素的迭代器,
若e本身就是尾后迭代器,则函数也返回尾后迭代器
c.clear() 删除中的所有元素。返回void

### 深拷贝与浅拷贝

- 浅拷贝
对于基本数据类型和简单对象，他们之间的拷贝非常简单，就是按位复制内存，这种默认的拷贝行为就是浅拷贝
，这和memcpy()函数的调用效果类似

- 深拷贝
深拷贝会将原有对象的所有成员变量拷贝给新对象，对于指针等数据还会为新对象重新在堆上分配一块内存，
并将原有对象所持有的堆上的数据也拷贝过来，这样能保证原有对象和新对象所持有的动态内存都是相互独立的，
更改一个对象的数据不会影响另一个对象，同时也不会造成double free的错误


### 堆的c++(优先队列)
需包含头文件#include <queue>
priority_queue<int> q;（大顶堆，在使用push操作时将大数放在堆顶）
priority_queue< int,vector<int>,greater<int> > minHeap;（小堆顶） 
```c
1. top(): 返回优先队列中优先级最高的元素（即最大元素）。如果队列为空，调用 top() 会导致未定义行为，因此在调用前最好先检查队列是否为空。
int top_element = q.top(); // 获取队列中优先级最高的元素
2. empty(): 检查队列是否为空。如果队列为空，返回 true；否则返回 false。
if (q.empty()) {
   std::cout << "Priority queue is empty!" << std::endl;
}
3. size(): 返回队列中的元素个数。
int size = q.size(); // 获取队列中的元素个数
4. swap(): 交换两个优先队列的内容。
```

### 类与对象
类可以看做是c语言中的结构体，且里面的成员可以有函数
成员变量的初始化顺序取决于它们在类中的声明顺序，而不是初始化列表的顺序

### 线程
- async
std::async 是 C++11 引入的异步任务（asynchronous task）工具，用于启动一个独立执行的任务，
并返回一个 std::future，以便稍后获取任务的返回值。
简单来说，它可以让任务并行运行，而主线程无需等待任务完成，提高程序的执行效率。
- 可变参数模板（new.cpp 342行）
1.展开包的方式
递归函数进行展开，需要有一个重载函数来终止递归较为麻烦
- 两种锁lock_guard和unique_lock
lock_guard：
```
创建即加锁，作用域结束自动析构并解锁，无需手工解锁
不能中途解锁，必须等作用域结束才解锁
不能复制
```
unique_lock
```
创建时可以不加锁（指定第二参数为std::defer_lock），而在需要时再锁定
可以随时加锁解锁（代价是增加了锁状态的维护，空间和性能会略有影响）
作用域规则同lock_grard，析构时自动释放锁
不可复制，可移动（可通过move转到另一个scope中生存，增加了管理难度）
condition variable条件变量需要该类型的锁作为参数（此场景必须使用unique_lock）
```