# 二、C语言的三种连续输入

## [](#)（1）while(~scanf("%d %d",&a,&b))

> 
> **~是按位取反，-1的十六[进制](https://so.csdn.net/so/search?q=%E8%BF%9B%E5%88%B6&spm=1001.2101.3001.7020 "进制")补码表示为0xffffffff，f是二进制的1111，取反后全部变为0，于是while结束，并且只有返回值为EOF（即-1）时，其取反值才为0，while循环才能结束。**
> 
> ```
> 
> 
> 1.  #include <stdio.h>
>     
> 2.  #include <string.h>
>     
> 3.  int main()
>     
> 4.  {
>     
> 5.  	int a, b;
>     
> 6.  	while (~scanf("%d %d", &a, &b))
>     
> 7.  	{
>     
> 8.  		printf("%d\n", a + b);
>     
> 9.  	}
>     
> 10. 	return 0;
>     
> 11. }
>     
> 
> ```

## [](#)**常用**（2）while(scanf("%d %d", &a, &b)!=EOF)

> ** 可以无限输入直到输入为EOF结束**
> 
> ```
> 
> 
> 1.  #include <stdio.h>
>     
> 2.  #include <string.h>
>     
> 3.  int main()
>     
> 4.  {
>     
> 5.  	int a, b;
>     
> 6.  	while (scanf("%d %d", &a, &b)!=EOF)
>     
> 7.  	{
>     
> 8.  		printf("%d\n", a + b);
>     
> 9.  	}
>     
> 10. 	return 0;
>     
> 11. }
>     
> 
> ```

## [](#)**重点**（3） while(scanf("%d",&m)==1)

> **while(scanf("%d",&m)==1) 就是连续输入了无数个****一个数****。**
> 
> **其中，输入个数与scanf函数有关****。例如：**
> 
> **    while(scanf("%d %d",&m,&n)==2) 也可以连续输入2个数**
> 
> **    重点 ：****在while里面可以方便加入限制条件，在做题是更加方便**
> 
> **   例如：题目要求连续输入一个数，但是这个数不能是 0**
> 
> **while(scanf("%d",&m)==1 && m!=0)** **就可以啦**
> 
> ```
> `
> 
> 1.  #include <stdio.h>
>     
> 2.  #include <string.h>
>     
> 3.  int main()
>     
> 4.  {
>     
> 5.  	int a;
>     
> 6.  	int b[5] = { 0 };
>     
> 7.  	int x = 0;
>     
> 8.  	while (scanf("%d", &a) == 1 && a != 0) // 1 2 0 4 5
>     
> 9.  	{
>     
> 10. 		b[x++] = a;
>     
> 11. 	}
>     
> 12. 	for (int i = 0; i < 5; i++)
>     
> 13. 	{
>     
> 14. 		printf("%d ", b[i]);     // 1 2 0 0 0
>     
> 15. 	}
>     
> 16. 	return 0;
>     
> 17. }
>     
> 
> `
> ```