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



