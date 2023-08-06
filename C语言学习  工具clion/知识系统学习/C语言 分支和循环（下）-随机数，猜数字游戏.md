- 电脑自动生成1~100的随机数
- 玩家猜数字，猜数字过程中，根据猜测数据的大小给出大了或小了的反馈，知道才对，游戏结束
# 一.随机数的生成 
## 1.rand
- 原型：这个函数可以帮我们生成随机数![[Pasted image 20230727140929.png]]
	- 在这写void的意思是这个函数不需要参数
	- rand函数会返回一个**伪函数**，这个随机数的范围实在0~RAND_MAX之间，这个RAND_MAX的大小是依赖编译器上的实现的。
	- **rand函数的使用条件需要包含一个头文件是：stdlib.h**
- ![[Pasted image 20230727171803.png]]
	- 两次生成的随机值一样，由此我们可以发现rand函数生成的是伪随机数，真正的伪随机数是无法预测下一个数是多少的。**rand函数是对一个叫”种子“的基准值进行运算生成的随机数**。
	- 之前每一次运行程序所产生的随机数序诗一样的，那是因为rand函数生成的随机数的默认种子是1。
	- **如果要生成不同的随机数，就要让种子是变化的**.
## 2.srand
C语言中，又提供了一个函数叫srand，用来初始化随机数的生成器，其原型如下：![[Pasted image 20230727172449.png]]
- **程序中在调用rand函数之前，先调用srand函数，通过srand函数的参数seed来设置rand函数生成随机数时候的种子，只要种子在变化，每次生成的随机数列也就变化起来了**。
- 也就是说**给srand的种子如果是随机的，rand就能生成随机数；在生成随机数的时候有需要一个随机数，这就矛盾了**。、
- srand函数不需要频繁调用，只需要调用一次就可以用rand函数生成随机数了
## 3.time
在程序中我们一般是使用程序运行的时间作为程序的种子，因为时间是时刻变化的。
在C语言中，有一个函数叫time就可以获得这个时间，其原型如下：![[Pasted image 20230727173303.png]]
- time函数会返回当前的日历时间，返回程序运行当前的时间点和1970年1月1日0分0秒之间的差值。time函数返回的差值叫时间戳。
- time函数返回的值的类型是time_t，time_t类型本质上是32位或64位的整型类型。其实就是int类型或long long类型。
- time函数的参数timer如果是⾮NULL的指针的话，函数也会将这个返回的差值放在timer指向的内存
- 随机数的生成程序入下![[Pasted image 20230727180720.png]]
中带回去。
## 1.4设计随机数的范围
![[Pasted image 20230727180323.png]]
# 二.猜数字游戏的实现
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void menu()//这个就像封装的模块一样，就是把这一段代码的功能封装到一个函数中，当我们用到的这个功能的时候，直接调用就行了
           //就像拼乐高一样，把所有能调用的模块拼装到一起，就完成了这个功能，下面的game函数也是一样的功能
	       //这个函数只需要完成它的功能即可，不需要返回，需要返回的话当然也能返回
{
	printf("**********************\n");
	printf("*****  1. play  ******\n");
	printf("*****  0. exit  *******\n");
	printf("**********************\n");
	
}

void game()
{
	int guess = 0;
	//1.生成随机数
	int r = rand()%100+1;
	//printf("%d\n", r);
	//2.猜数字
	int count = 5;
	while (count)
	{
		printf("请猜数字:>");
		scanf("%d", &guess);
		if (guess > r)
		{
			printf("猜大了\n");
		}
		else if (guess < r)
		{
			printf("猜小了\n");
		}
		else
		{
			printf("恭喜你，猜对了\n");
			break;
		}
		count--;
	}
	if (count == 0)
	{
		printf("猜数字失败，正确的值是:%d\n", r);
	}
}

int main()
{
	int input = 0;
	srand((unsigned int)time(NULL));//srand函数只需要调用一次即可，所以我们将他放入主函数
	do
	{
		//打印菜单
		menu();
		printf("请选择:>");
		scanf("%d", &input);
		switch (input)
		{
		case 1:
			game();
			break;
		case 0:
			printf("退出游戏\n");
			break;
		default:
			printf("选择错误，重新选择\n");
			break;
		}
	} while (input);
	return 0;
}
```
这个猜数字游戏就是对以前所学循环和语句的综合运用的体现