---
title: C语言格式字符串 % lf 和 %f
date: '2013-04-05'
description: C语言格式字符串 % lf 和 %f
categories: C
tags: [C, 格式 ]
---


%lf 和 %f是有区别的，主要体现在输入的情况下, 如下：

  		#define intdex long
		typedef struct XYZType{
		  double Loc[3];
		  void * ref;
		}XYZType;

		typedef struct PList{
		  intdex        numpoints;
		  XYZType*   P;
		}

在读入数据时使用

		FILE* in;
		PList Points;
		in=fopen("tin.txt", "r");
		...
这时需要使用

		fscanf(in, "%lf %lf %lf\n", &Points.P[i].Loc[0],&Points.P[i].Loc[1],&Points.P[i].Loc[2]);

才能正确读入, %lf匹配 double。如果使用：

		fscanf(in, "%f %f %f\n", &Points.P[i].Loc[0],&Points.P[i].Loc[1],&Points.P[i].Loc[2]);

将读入无效数.


C中格式字符串的一般形式为： [标志][输出最小宽度][.精度][长度]类型其中方括号[]中的项为可选项。各项的意义介绍如下：

1.类型字符用以表示输出数据的类型，其格式符和意义下表所示：

		表示输出类型的格式字符 　　　　　 格式字符意义
		a                                 浮点数、十六进制数字和p-计数法(C99)
		A                                 浮点数、十六进制数字和p-计数法(C99)
		c 　　　　　　　　　　　　　　　　输出单个字符
		d 　　　　　　　　　　　　　　　　以十进制形式输出带符号整数(正数不输出符号)
		e 　　　　　　　　　　　　　　　　以指数形式输出单、双精度实数
		E 　　　　　　　　　　　　　　　　以指数形式输出单、双精度实数
		f 　　　　　　　　　　　　　　　　以小数形式输出单、双精度实数
		g 　　　　　　　　　　　　　　　　以%f%e中较短的输出宽度输出单、双精度实数,%e格式在指数小于-4或者大  于等于精度时使用
		G 　　　　　　　　　　　　　　　　以%f%e中较短的输出宽度输出单、双精度实数,%e格式在指数小于-4或者大于等于精度时使用
		i                                 有符号十进制整数(与%d相同)
		o 　　　　　　　　　　　　　　　　以八进制形式输出无符号整数(不输出前缀O)
		p                                 指针
		s 　　　　　　　　　　　　　　　　输出字符串
		x 　　　　　　　　　　　　　　　　以十六进制形式输出无符号整数(不输出前缀OX)
		X　　　　　　　　　　　　　　　　 以十六进制形式输出无符号整数(不输出前缀OX)
		u 　　　　　　　　　　　　　　　　以十进制形式输出无符号整数


		/*  测试常见的输出类型  */
		#include "stdio.h"
		#include "conio.h"
		main()
		{
		    printf("The program test print style!\n");

		    /*  以十进制形式输出带符号整数(正数不输出符号)  */
		    printf("%d\n" , 223);
		    printf("%d\n" , -232);
		    printf("\n");
		    /*  以八进制形式输出无符号整数(不输出前缀O)  */
		    printf("%o\n" , 223);
		    printf("%o\n" , -232);
		    printf("\n");
		    /*  以十六进制形式输出无符号整数(不输出前缀OX)  */
		    printf("%x\n" , 223);
		    printf("%x\n" , -232);
		    printf("\n");
		    /*  以十进制形式输出无符号整数  */
		    printf("%u\n" , 223);
		    printf("%u\n" , -232);
		    printf("\n");
		    /*  以小数形式输出单、双精度实数  */
		    printf("%f\n" , 223.11);
		    printf("%f\n" , 232.11111111);
		    printf("%f\n" , -223.11);
		    printf("%f\n" , -232.11111111);
		    printf("\n");
		    /*  以指数形式输出单、双精度实数  */
		    printf("%e\n" , 223.11);
		    printf("%e\n" , 232.11111111);
		    printf("%e\n" , -223.11);
		    printf("%e\n" , -232.11111111);
		    printf("\n");
		    /*  以%f%e中较短的输出宽度输出单、双精度实数  */
		    printf("%g\n" , 223.11);
		    printf("%g\n" , 232.111111111111);
		    printf("%g\n" , -223.11);
		    printf("%g\n" , -232.111111111111);
		    printf("\n");
		    /*  输出单个字符  */
		    printf("%c\n" , 'a');
		    printf("%c\n" , 97);
		    printf("\n");
		    /*  输出单个字符  */
		    printf("%s\n" , "this is a test!");
		    printf("%s\n" , "2342o34uo23u");
		    printf("\n");
		    getch();
		}

2.标志

标志字符为-、+、\#、空格和0五种，其意义下表所示：

		标志格式字符 　　　　　标 志 意 义
		- 　　　　　　　　　 结果左对齐，右边填空格
		+ 　　　　　　　　　 输出符号(正号或负号)
		空格                 输出值为正时冠以空格，为负时冠以负号
		# 　　　　　　　　　 对c，s，d，u类无影响；对o类，在输出时加前缀0；对x类，
		                     在输出时加前缀0x或者0X；对g，G 类防止尾随0被删除；
		                     对于所有的浮点形式，#保证了即使不跟任何数字，也打印一个小数点字符
		0                    对于所有的数字格式，用前导0填充字段宽度，若出现-标志或者指定了精度(对于整数),忽略.

3.输出最小宽度

用十进制整数来表示输出的最少位数。若实际位数多于定义的宽度，则按实际位数输出，若实际位数少于定义的宽度则补以空格或0。

		/*  测试标志字符为-、+、#、空格四种  */
		#include "stdio.h"
		#include "conio.h"
		main()
		{
		      /*  以十进制形式输出带符号整数(正数不输出符号)  */
		    printf("*%-10d*\n", 223);
		    printf("*%+10d*\n" , -232);
		    printf("*%2d*\n" , 223);
		    printf("*%#d*\n" , -232);
		    printf("\n");
		    getch();
		    /*  以八进制形式输出无符号整数(不输出前缀O)  */
		    printf("*%-10o*\n" , 223);
		    printf("*%+10o*\n" , -232);
		    printf("*%o*\n" , 223);
		    printf("*%#o*\n" , -232);
		    printf("\n");
		    getch();
		    /*  以十六进制形式输出无符号整数(不输出前缀OX)  */
		    printf("$%-10x$\n" , 223);
		    printf("$%010x$\n" , -232);
		    printf("$% x$\n" , 223);
		    printf("$%#x$\n" , -232);
		    printf("\n");
		    /*  以十进制形式输出无符号整数  */
		    printf("%-10u\n" , 223);
		    printf("%+10u\n" , -232);
		    printf("% u\n" , 223);
		    printf("%#u\n" , -232);
		    printf("\n");
		    getch();
		    /*  以小数形式输出单、双精度实数  */
		    printf("%-10f\n" , 223.11);
		    printf("%+10f\n" , 232.11111111);
		    printf("% f\n" , -223.11);
		    printf("%#f\n" , -232.11111111);
		    printf("\n");
		    getch();
		    /*  以指数形式输出单、双精度实数  */
		    printf("%-10e\n" , 223.11);
		    printf("%+10e\n" , 232.11111111);
		    printf("% e\n" , -223.11);
		    printf("%#e\n" , -232.11111111);
		    printf("\n");
		    getch();
		    /*  以%f%e中较短的输出宽度输出单、双精度实数  */
		    printf("%-10g\n" , 223.11);
		    printf("%+10g\n" , 232.111111111111);
		    printf("% g\n" , -223.11);
		    printf("%#g\n" , -232.111111111111);
		    printf("\n");
		    getch();
		    /*  输出单个字符  */
		    printf("%-10c\n" , 'a');
		    printf("%+10c\n" , 97);
		    printf("% c\n" , 'a');
		    printf("%#c\n" , 97);
		    printf("\n");
		    getch();
		    /*  输出单个字符  */
		    printf("%-20s\n" , "this is a test!");
		    printf("%+20s\n" , "2342o34uo23u");
		    printf("% 20s\n" , "this is a test!");/* 不足补空格 */
		    printf("%#s\n" , "2342o34uo23u");
		    printf("\n");
		    getch();
		}
 
4.精度

精度格式符以“.”开头，后跟十进制整数。本项的意义是：如果输出数字，则表示小数的位数；如果输出的是字符，则表示输出字符的个数；若实际位数大于所定义的精度数，则截去超过的部分。

		/*  测试精度  */
		#include "stdio.h"
		#include "conio.h"
		main()
		{
		    printf("%.3d\n" , 5555);
		    getch();
		    printf("%.3f\n" , 0.88888);
		    getch();
		    printf("%.3f\n" , 0.9999);
		    getch();
		    printf("%.4s\n" , "this is a test!");
		    getch();
		}

5.长度

长度格式符为h,l两种，h表示按短整型量输出，l表示按长整型量输出。

    h和整数转换说明符一起使用，表示一个short  int 或者unsigned short int类型的数值 ，示例：%hu，%hx，%6.4hd

    hh和整数转换说明符一起使用，表示一个short  int 或者unsigned short类型的数值 ，示例：%hhu，%hhx，%6.4hhd

    j和整数转换说明符一起使用，表示一个intmax_t或者uintmax_t类型的数值 ，示例：%jd,%8jx

    l和整数转换说明符一起使用，表示一个long int 或者unsigned long int类型的数值 ，示例：%ld,%8lu

    ll和整数转换说明符一起使用，表示一个long int 或者unsigned long int类型的数值 (C99)，示例：%lld,%8llu

    L和浮点转换说明符一起使用，表示一个long double的值，示例：%Lf，%10.4Le

    t和整数转换说明符一起使用，表示一个ptrdiff_t值(两个指针之间的差相对应的类型)(C99)，示例：%td,%12ti

    z和整数转换说明符一起使用，表示一个size_t值(sizeof返回的类型)(C99)，示例：%zd,%12zx

		main(){
		int a=15;
		 float b=138.3576278;
		 double c=35648256.3645687;
		 char d='p';
		 printf("a=%d,%5d,%o,%x\n",a,a,a,a);
		 printf("b=%f,%lf,%5.4lf,%e\n",b,b,b,b);
		 printf("c=%lf,%f,%8.4lf\n",c,c,c);
		 printf("d=%c,%8c\n",d,d);
		}
		a<--15
		b<--138.3576278
		c<--35648256.3645687
		d<--'p'
		 
		main()
		{
		    int a=29;
		    float b=1243.2341;
		    double c=24212345.24232;
		    char d='h';
		    printf("a=%d,%5d,%o,%x\n",a,a,a,a);
		   
		    /* 其中“%f”和“%lf ”格式的输出相同，说明“l”符对“f”类型无影响
		     * “%5.4lf”指定输出宽度为5，精度为4，由于实际长度超过5故应该按实际位数输出，小数位数超过4位       *  部分被截去
		     */
		    printf("b=%f,%lf,%5.4lf,%e\n",b,b,b,b);
		   
		    /* 输出双精度实数，“%8.4lf ”由于指定精度为4位故截去了超过4位的部分 */
		    printf("c=%lf,%f,%8.4lf\n",c,c,c);
		   
		    /* 输出字符量d，其中“%8c ”指定输出宽度为8故在输出字符p之前补加7个空格 */
		    printf("d=%c,%8c\n",d,d);
		    getch();
		}
 
使用printf函数时还要注意一个问题，那就是输出表列中的求值顺序。不同的编译系统不一定相同，可以从左到右，也可从右到左。Turbo C是按从右到左进行的
		
		main(){
		int i=8;
		printf("%d\n%d\n%d\n%d\n%d\n",++i,--i,i--,i++,-i--);
		}

