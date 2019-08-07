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



