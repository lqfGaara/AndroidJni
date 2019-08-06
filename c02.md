

```

#include <stdio.h>
#include <stdlib.h>
#include <Windows.h>
#include <math.h>
#include <time.h>

//1.指针为什么要有类型？
//指针有类型，地址没有类型
//地址只是开始的位置，类型读取到什么位置结束
/*
void main(){
	int i = 89;
	//int 类型的指针
	int *p = &i;
	double j = 78.9;
	//赋值为double类型变量的地址
	p = &j;
	printf("double size:%d\n", sizeof(double));
	printf("%#x,%lf\n",p,*p); //想通过4字节读取8字节变量的值，是不行的	

	getchar();
}
*/

//2.NULL空指针
/*
void main(){
	int i = 9;
	int *p = NULL;
	//p = &i;
	
	//空指针的默认值为0
	printf("%#x\n",p);
	//访问内存地址0x000000操作系统不允许
	//p = 100; //操作系统不允许访问
	printf("%d\n",*p);
	getchar();
}
*/

//3.多级指针（二级指针）
//指针保存的是变量的地址，保存的这个变量还可以是一个指针变量
//动态内存分配给二维数组
/*
void main(){
	int a = 50;
	//p1上保存的a的地址
	int* p1 = &a;
	
	//p2上保存的p1的地址
	int** p2 = &p1;

	//int*** p3 = &p2;

	printf("p1:%#x,p2:%#x\n",p1,p2);
	**p2 = 90;

	printf("%d\n",a);

	getchar();
}
*/

//4.指针的运算
//指针的运算，一般在数组遍历时才有意义，基于数组在内存中线性排列的方式
/*
void main(){
	//数组在内存中连续存储
	int ids[] = { 78, 90, 23, 65, 19 };
	//数组变量名：ids就是数组的首地址
	printf("%#x\n",ids);
	printf("%#x\n",&ids);
	printf("%#x\n",&ids[0]);
	//指针变量
	int *p = ids;
	printf("%d\n",*p);
	//指针的加法
	p++; //p++向前移动sizeof(数据类型)个字节
	printf("p的值:%#x\n", p);
	//p--;
	printf("%d\n", *p);
	getchar();
}
*/
//5.通过指针给数组赋值
/*
void main(){
	int uids[5];
	//高级写法
	//int i = 0;
	//for (; i < 5; i++){
	//	uids[i] = i;
	//}
	//早些版本的写法
	int* p = uids;
	printf("%#x\n",p);
	int i = 0; //i是数组元素的值
	for (; p < uids + 5; p++){
		*p = i;
		i++;
	}

	getchar();
}
*/

//6.函数指针
/*
int msg(char* msg,char* title){
	MessageBox(0,msg,title,0);
	return 0;
}
void main(){
	//msg();
	printf("%#x\n",msg);
	printf("%#x\n",&msg);
	//函数指针
	//函数返回值类型，函数指针的名称，函数的参数列表
	int(*fun_p)(char* msg, char* title) = msg;
	fun_p("消息内容","标题");

	getchar();
}
*/

int add(int a,int b){
	return a + b;
}

int minus(int a,int b){
	return a - b;
}

/*int div(int a, int b){
	return a - b;
}*/

//msg函数需要传递一个函数指针参数
//类似于我们Java中的回调函数
/*
void msg(int(*func_p)(int a, int b), int m, int n){
	printf("执行一段代码...\n");
	printf("执行回调函数...\n");
	int r = func_p(m, n);
	printf("执行结果：%d\n",r);
}

void main(){
	//加法
	//int(*func_p)(int a, int b) = add;
	msg(div, 10, 20);
	//减法
	//msg(minus,50,10);
	getchar();
}
*/

/*
//案例：用随机数生成一个数组，写一个函数查找最小的值，并返回最小数的地址，在主函数中打印出来
int* getMinPointer(int ids[], int len){
	int i = 0; 	
	int* p = &ids[0];
	for (; i < len; i++){
		if (ids[i] < *p){			
			p = &ids[i];
		}
	}
	return p;
}

void main(){
	int ids[10];
	int i = 0;
	//初始化随机数发生器，设置种子，种子不一样，随机数才不一样
	//当前时间作为种子 有符号 int -xx - > +xx
	srand((unsigned)time(NULL));
	for (; i < 10; i++){
		//100范围内
		ids[i] = rand() % 100;
		printf("%d\n", ids[i]);
	}

	int* p = getMinPointer(ids, sizeof(ids) / sizeof(int));
	printf("%#x,%d\n",p,*p);
	getchar();
}
*/
```

