# C语言函数指针

如果定义了一个函数，那么在编译时，系统就会给该函数分配一段“内存空间”，这段内存空间的首地址称为这个函数的地址,而且函数名称就表示这个地址，函数指针就可以用来指向这个地址，使用函数指针调用函数就等价于使用函数名调用该函数。

#### 函数指针的定义：

```
type (*p)(type1 var1, type2 var2, ... )

即为函数返回值类型 (* 指针变量名称)(函数参数列表）
```

#### 直接上一个例子，就能很方便的看清楚如何使用函数指针：

```c
#include<stdio.h>
#include<stdlib.h>

typedef struct _treenode{
  int data;
  _treenode *lchild;
  _treenode *rchild;
} treeNode;

typedef struct _bintree{
  int size;
  int (*conpare)(int x1, int x2);
  treeNode *root;
} bintree;

bintree * bintree_initial(int (*conpare_func)(int x1, int x2)){
  bintree *mytree;
  mytree = (bintree *)malloc(sizeof(bintree)*1);
  mytree->size = 0;
  mytree->compare = conpare_func;
  mytree->root = NULL;
  return(mytree);
}

int intCompare(int x1, int x2){
  int y;
  if(x1 == x2) return 0;
  else if(x1>x2) return 1;
  else return -1;
}

void main(){
  bintree *tree1;
  int x1, x2;
  tree1 = bintree_initial(intCompare)
  //
  printf("Input 2 integers:");
  scanf("%d  %d",&x1, &x2);
  printf("%d   %d    %d\n", x1, x2, tree1->compare(x1, x2));
}
```

#### NOTE:函数指针不支持`++`，`--`运算

---

## C语言-结构体

在现实生活中，一组数据往往具有很多种类型的数据。例如，学生登记表，它里面包含了姓名、学号、成绩、班级等等，而这些元素的数据类型分别为字符、整型、浮点型等等。显而易见，这些数据是不能放在同一个数组当中的，因为数组中的各元素必须是同种类型的数据，且长度保持一致。因此，为了解决这一问题，C语言中给出了另一种构造数据类型——“structure（结构）”，又称之为结构体。它相当于一种高级的数据构造类型，它可以是有两个或两个以上成员组成。

* #### 一般形式：

```
struct结构体名
{

    成员列表；
}；
```

#### 2. 结构体类型变量的定义

```
1.先定义结构，后定义变量:struct
struct stu
{
    char name[20];
    char sex;
    float score;
};
struct stu boy,girl;
```

```
2.用宏定义结构类型:
#define STU struct stu
struct stu
{
    char name[20];
    char sex;
    float score;
};
struct stu boy,girl;
```

```
3.在定义结构类型的同时说明变量：
struct stu
{
    char name[20];
    char sex;
    float score;
}boy,girl;
```

```
4.匿名结构体  （控制结构体变量的个数（限量版），相当于单例）
struct{
    char name[20];
    int age;
}m1;
```

#### 3. 指向结构变量的指针

定义结构指针的一般形式：

**struct 结构名 \*结构指针变量**

```
例如：
struct stu *pstudent;
// *pstudent 是结构类型stu的指针；
```

#### 4. 结构类型定义符typedef

**typedef用于给数据类型取“别名”。**

若用typedef 定义数组、指针、结构类型将会很方便，不仅使程序书写简单，且使意义更加明确，同时也增强了可读性。

一般形式：

**typedef 原类型名 新类型名；**

#### 5.计算结构体长度规则

内存字节对齐原则（求字节数）：

1. **如果结构体里面所有的成员变量（成员属性）都是基本数据类型（int、char、float、double），那么第一个成员变量从内存地址偏移量为零开始计数，后面的成员变量从内存地址偏移量是本身所占字节大小的最小倍数开始分配。**
2. **如果结构体里面的成员变量不是基本数据类型，比如：int arr\[10\]；那么，这个数组成员变量从内存地址偏移量是这个数组本身里面的元素的最大字节数的倍数开始分配。**
3. **最后收尾的时候，所占字节数要是最大成员变量的最小倍数**

---

## C语言-联合体\(UNION\)

**联合体（union，又叫共用体）：使几种不同类型的变量存放到同一段内存单元中。即使用覆盖技术，几个变量互相覆盖重叠。**

定义形式：

```
1：
union 共用体名 {
    数据类型 成员名;
    数据类型 成员名;
    ...
} 变量名;

2：
union 共用体名 {
    数据类型 成员名;
    数据类型 成员名;
    ...
};

3：
typedef union {
    数据类型 成员名;
    数据类型 成员名;
    ...
} 共用体名;

4：
typedef union _共用体名 {
    数据类型 成员名;
    数据类型 成员名;
    ...
}共用体名,*P共用体名;
```

#### 联合体定义使用时注意点：

* union中可以定义多个成员，union的大小由最大的成员的大小决定。
* union成员共享同一块大小的内存，一次只能使用其中的一个成员。
* 对某一个成员赋值，会覆盖其他成员的值，因为他们共享一块内存。
* union中各个成员存储的起始地址都是相对于基地址的偏移都为0。

#### 联合体和结构体区别：

* 联合体和结构体都由多个不同的数据类型成员组成，但在任何同一时刻，联合体只存放了一个被选中的成员，而结构体的所有成员都存在。
* 对于联合体的不同成员赋值, 会对其它成员重写, 原成员值被覆盖, 而对于结构体的不同成员赋值是互不影响的。
* 结构体里可以含有union成员，union里也可以含结构体成员。 

#### Union的应用：

```
typedef union {
      char c;
      int a;
} U;

int is_integer_lower_store() {
       U u;
       u.a = 1;

       return u.c;
}
```

## C语言-枚举\(enum\)

枚举\(enum\)：当一个变量的值被限于列出来的值的范围内，那么这个变量就可以被定义为一个枚举类型的变量。

定义形式：

```
1：
enum 枚举名 {
    值1,//如果不额外指定则第一个标识等于整数0，后续依次加1
    值2,
    值3=7,//注意，值3的值不能被指定为0,1,否则会和值1，值2冲突
    值4,//这个时候，值4的值是8
    ....
    值n
};
enum 枚举名 变量名;

2：
typedef enum  _枚举名 {
    值1,
    值2,
    值3,
    值4,
    ....
    值n  
} 枚举名, *P枚举名;
```



