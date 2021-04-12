# 2021-04-03
少量地做一些穷举和递推，准备下下周的上机考试！

1、求解不等式：
#include<stdio.h>
#include<math.h>
 
int main(int argc,char const*argv[])
{
	int m = 0;
	int i = 0;
	double n;
	double result;
	
	printf("Input n:\n");
	scanf("%lf",&n);

	do{
		result = 0.0;
		for (i=0 ; i<=m ; i++)
		{
			result = result + sqrt(m+i);
		}
		m++;
	} while (result <= n);
	
	printf("Result:m>=%d\n",m-1);
	printf("s=%.2lf\n",result);	
	return 0;
}
总结：result每次循环结束都要初始化为0！

2、输出大于给定自然数n的最小素数
#include<stdio.h>

int IsPrime(int a);

int main(int argc,char const*argv[])
{
	int n;
	long k = 2;
	
	printf("Please input n:");
	scanf("%d",&n);
	
	do{
		k++;
	} while (k <= n || !IsPrime(k) );
	
	printf("%ld",k);
	return 0;
}

int IsPrime(int a)
{
	int i;
	for (i=2 ; i<a ; i++)
	{
		if (a%i == 0)
			return 0;
	}
	return 1;
}

3、（4星难度）亲密数_2：2500年前数学大师毕达哥拉斯就发现，220与284两数之间存在着奇妙的联系：
220的真因数之和为：1+2+4+5+10+11+20+22+44+55+110=284
284的真因数之和为：1+2+4+71+142=220
毕达哥拉斯把这样的数对称为相亲数。相亲数，也称为亲密数，如果整数A的全部因子（包括1，不包括A本身）之和等于B，
且整数B的全部因子（包括1，不包括B本身）之和等于A，则将整数A和B称为亲密数。
从键盘任意输入一个整数n，编程计算并输出n以内的全部亲密数。
一对亲密数只输出一次, 小的在前。

程序运行示例1
Input n:
3000↙
(220,284)
(1184,1210)
(2620,2924)

程序运行示例2
Input n:
1000↙
(220,284)

输入格式: "%d"
输出格式：
输入提示信息："Input n:\n"
输出格式： "(%d,%d)\n"

#include<stdio.h>
#include<math.h>

int FactorSum(int n);

int main(int argc,char const*argv[])
{
	int n;
	int p,q;
	printf("Input n:\n");
	scanf("%d",&n);

	for (p=1 ; p<=n ; p++)
	{
		q = FactorSum(p);
		if (p == FactorSum(q) && q>p)
		{
			printf("(%d,%d)\n", p, q);
		}
	}
	return 0;
}
// 函数功能：返回n的所有因子之和
int FactorSum(int n)
{
	int i;
	int sum = 1;
	for (i=2 ; i<=sqrt(n) ; i++)
	{
		if (n%i == 0)
			sum+=(i+n/i);
	}
	return sum;
}
总结：思考出不用双重循环而用单重循环对于运行时间的减少非常重要
还有一个计算所有因子之和的小技巧

4、
梅森尼数
形如2^i-1的素数，称为梅森尼数。编程计算并输出指数i在[2,n]中的所有梅森尼数，并统计这些梅森尼数的个数，
其中n的值由键盘输入，并且n的值不能大于50。
其中，2^i表示2的i次方，请尽量不要使用pow(2,i)编程计算（若要用，请一直使用double计算），应采用循环累乘求积的方式计算2^i。
请用下面的函数原型，编写程序。
int IsPrime(double x);
提示：当i超过30以后，2^i-1的值会很大，不能用long型变量来存储，必须使用double类型来存储。
对于double类型变量x（不是整型）不能执行求余运算，即不能用x%i == 0来判断x是否能被i整除，可以使用x/i == (long long)(x/i)来判断x是否能被i整除。

程序运行示例
Input n:
50↙
2^2-1=3
2^3-1=7
2^5-1=31
2^7-1=127
2^13-1=8191
2^17-1=131071
2^19-1=524287
2^31-1=2147483647
count=8

输入提示信息："Input n:\n"
输入格式: "%d"
输出格式： "2^%d-1=%.0f\n"
           "count=%d\n"

#include<stdio.h>
#include<math.h>

int IsPrime(double x);

int main(int argc,char const*argv[])
{
	int n;
	int i = 1;
	int count = 0;
	double x = 2.0;
	printf("Input n:\n");
	scanf("%d",&n);

	do{
		x *= 2;
		i++;
		if (IsPrime(x-1))
		{
			printf("2^%d-1=%.0f\n",i,x-1);
			count++;
		}
	} while (i <= n);
	printf("count=%d\n",count);
	return 0;
}

int IsPrime(double x)
{
	int i;
	for (i=2 ; i<=sqrt(x) ; i++)
	{
		if (x/i == (long long)(x/i))
			return 0;
	}
	return 1;
}
总结：
·循环累乘求积可以避免由于频繁调用pow函数而产生的额外运行时间。
·素数判断从2到sqrt(x)即可，需要#include<math.h>
·当i超过30以后，2^i-1的值会很大，不能用long型变量来存储，必须使用double类型来存储。
·对于double类型变量x（不是整型）不能执行求余运算，即不能用x%i == 0来判断x是否能被i整除，可以使用x/i == (long long)(x/i)来判断x是否能被i整除。

好艰难的一天啊！编程真的很需要注重细节！
