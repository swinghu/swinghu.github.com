---
layout: post
title: Learn C++ STL The Hard Way 1---C++模板函数
description: C++ STL 系列之---C++模板函数
category: trash
---

一、模板函数实例化：
有时候我们需要这样一种函数，它们能够在行为上完全一致，然而能够"自动"灵活的处理多种参数类型。对于这种函数，在C++中我们完全可以利用其＂语法糖＂来分析该类型问题。我们可以应用C++ STL中的模板和泛型技术来帮助我们优雅的解决实际问题。先上来一个简单的代码：
	template <typename T>
	inline T const& min(T const& a ,T const& b ){
		return a<b ? b:a ;
	}
	template <typename T>
	inline T const& max(T const& a ,T const& b ){
    return a<b ? b:a ;
	}
对于上面的所给出的模板函数，在实际的应用中可以用任意类型(包括用户自定义类型)来实例化该模板函数，实例化测试如下：

	int main()
	{
		printf("the max value is %d\n",::max(4,5));　　//ok 适用于 max(int,int)
		printf("the max value is %f\n",::max(54.5,32.2));//ok 适用于 max(float,float)

		return 0;
	}
测试结果为：

	the max value is 5
	the max value is 54.500000
	the max value is 32.200000
	
从上面的实例运行的结果可以得出，C++编译器(本次测试所用C++编译器为：GCC compiler)会自动根据传递给max，min函数的参数将max，min模板函数实例化，返回正确的执行结果，这时候可能会有人想，使用宏实现
如：

	#define max_macro(a,b) ((a)<(b)) ? (b):(a)  // 此处特意命名为max_macro(a,b)

对于宏，实例化测试如下：

	int main()
	{

		printf("the max value is %d\n",max_macro(2+3,4+5));
		printf("the max value is %f\n",max_macro(4.5,2.3));
		return 0;
	}
测试结果为：
	the max value is 9
	the max value is 4.500000
从上面的实例中可以看出，也能达到同样的效果，但是相比于模板函数，宏的方式存在一些问题，例如类型不安全（type-safe,类型安全参加附文)。虽然C++给我们很大的方便，但是同时我们要注意一下几点
	(1)参数a 和 b 的类型要保持一致，否则编译不能通过，例如以上给出的max函数对于参数(54.5,32)就不适用;
	(2)对于类型T(由typename定义给出)而言，该类型不管是C++ 内置类型，还是用户自定义类型，该类型必需提供对操作符operator <() 的支持，否则否则无法成功编译(main.cpp|27|error: no match for 'operator<' (operand types are 'MyPoint' and 'MyPoint')|)。例如，对于用户定义的class来说，则必须对class进行重载小于操作符；
    对于以上(1),(2)两点，解决方法分别是；
    
	(1)定义多参数类型的max函数，如：
	
	template <typename T,typename F>
	inline T const& max2 (T const& a,F const& b){
		return a<b ? b:a;
	}	
这样就可以运行通过。			
	(2)对于没有内嵌operator <()操作符的类型，自定义重载该操作符
	
		class MyPoint {//省略的相关头文件
			public:
				MyPoint(int xvalue,int yvalue) : x_value(xvalue),y_value(yvalue) {
				}
				bool operator< (const MyPoint& other) const {
					printf("operator < is define and used\n");
					return x_value<other.x_value && y_value < other.y_value;

				}
				MyPoint max(MyPoint p1,MyPoint p2) const {
					if(p1<p2){
						return p2;
					}
					else return p1;
				}
				int getX() const { return x_value; }
				int getY() const { return y_value; }

			private:
				int x_value;
				int y_value;
		};
		int main()
		{
			MyPoint point1(1,2),point2(3,4);
			MyPoint res = point1.max(point1,point2);
			cout<< res.getX() <<" and "<< res.getY();
			return 0;
		}
这只是一个简单例子，运行，测试执行结果为：
	operator < is define and used
	3 and 4
从执行结果可以看出operator <()操作符被调用，可正确执行
    (3)max,min 函数传递的是参数的引用类型，而不是值传递 (如：max,min(T const& a ,T const& b )，这样就可以避免出现在max,min 中使用临时变量(副本copy)，而在函数返回中，返回一个临时变量的引用(会造成野指针错误)问题。
    (4)C++的编译器会为每一种类型都产生一个实例化函数，而不是仅仅构造出一个函数实例，然后再基于不同的参数类型调用该通用函数.如:
    #include <iostream>
    #include <stdio.h>

    using namespace std;

    template <typename T>
        inline T const& min(T const& a ,T const& b ){
            return a<b ? b:a ;
    }

    template <typename T>
        inline T const& max(T const& a ,T const& b ){
        return a<b ? b:a ;
    }


    class MyPoint {//省略的相关头文件
                public:
                    MyPoint(int xvalue,int yvalue) : x_value(xvalue),y_value(yvalue) {
                    }
                    bool operator< (const MyPoint& other) const {//重载操作符
                        printf("operator < is define and used\n");
                        return x_value<other.x_value && y_value < other.y_value;

                    }
                    /*MyPoint max(MyPoint p1,MyPoint p2) const {//在此处定义也可以比较point的大小
                        if(p1<p2){
                            return p2;
                        }
                        else return p1;
                    }*/
                    int getX() const { return x_value; }
                    int getY() const { return y_value; }

                private:
                    int x_value;
                    int y_value;
    };
    int main()
    {
        printf("the max value is %d\n",::max(4,5));//ok 适用于 max(int,int)
        printf("the max value is %f\n",::max(54.5,32.2));//ok 适用于 max(float,float)
        MyPoint point1(1,2),point2(3,4);
        //MyPoint res = point1.max(point1,point2);
        MyPoint res = ::max(point1,point2);
        cout<< res.getX() <<" and "<< res.getY();
        return 0;
    }
    //the max value is 5
    //the max value is 54.500000
    //operator < is define and used
    //3 and 4
		
	

	template <typename T>
	inline T const& min(T const& a,T const& b ){
		return a>b ? b:a ;
	}


	#include <iostream>
	#include <stdio.h>
	using namespace std;
	template <typename T>
	inline T const& max(T const& a ,T const& b ){
		return a<b ? b:a ;
	}
	int main()
	{
		printf("the max value is %d\n",::max(4,5));　　//ok 适用于 max(int,int)
		printf("the max value is %f\n",::max(54.5,32.2));//ok 适用于 max(float,float)

		return 0;
	}




二、"重载"函数模板：
初看这个标题有点模糊，其实指的是 模板函数的重载。模板函数和其他函数一样，也可以实现重载。如：
    #include <iostream>
    #include<stdio.h>
    using namespace std;

    inline int const& max(int const& a,int const& b){
        printf("inline int const& max(int const& a,int const& b is revoked.\n");
        return a<b? b:a;
    }

    template <typename T>
    inline T const& max(T const& a,T const& b){
        printf("template: inline T const& max(T const& a,T const& b) is revoked.\n");
        return a<b? b:a;
    }

    template <typename T>
    inline T const& max(T const&a,T const& b,T const& c){
        printf("template: inline T const& max(T const&a,T const& b,T const& c) is revoked .\n");
        return ::max(::max(a,b),c);
    }
    class MyPoint {//省略的相关头文件
                public:
                    MyPoint(int xvalue,int yvalue) : x_value(xvalue),y_value(yvalue) {
                    }
                    bool operator< (const MyPoint& other) const {//重载操作符
                        printf("operator < is define and used\n");
                        return x_value<other.x_value && y_value < other.y_value;
                    }
                    /*MyPoint max(MyPoint p1,MyPoint p2) const {
                        if(p1<p2){
                            return p2;
                        }
                        else return p1;
                    }*/
                    int getX() const { return x_value; }
                    int getY() const { return y_value; }

                private:
                    int x_value;
                    int y_value;
    };
    int main()
    {
        cout <<"1------"<<endl;
        ::max(5,6,7); //模板函数+非模板函数---调用3个参数的模板函数，和两个参数的非模板函数
        cout <<"2------"<<endl;
        ::max('a','b'); //模板函数---调用2个参数的模板函数
        cout <<"3------"<<endl;
        ::max(::max('a','b'),'d');//模板函数---两次调用两个参数的模板函数
        cout <<"4------"<<endl;
        ::max('a',54.9);//非模板函数---int类型的非模板函数
        return 0;
    }
执行结果为：

    1------
    template: inline T const& max(T const&a,T const& b,T const& c) is revoked .
    inline int const& max(int const& a,int const& b is revoked.
    inline int const& max(int const& a,int const& b is revoked.
    2------
    template: inline T const& max(T const& a,T const& b) is revoked.
    3------
    template: inline T const& max(T const& a,T const& b) is revoked.
    template: inline T const& max(T const& a,T const& b) is revoked.
    4------
    inline int const& max(int const& a,int const& b is revoked.

从上面的输出可以看出，可以了解到以下几点：
  1.非模板函数和模板函数可以同名，调用的时候编译器可以一起进行函数重载的推演
  2.在推演的时候，首选非模板函数
  3.指定<>，则推演时，可限定为模板函数
  4.模板函数在推演时，要对参数类型进行分析，判断参数类型是否和定义的模板一致,因此在第4个测试中，因为调用的参数表类型与模板函数不一致，则调用非模板函数(非模板函数可对参数进行类型转换，转换为int类型)，如若要使用模板函数，则需要定义不同参数的模板函数。





附：
C++的类型安全
什么是类型安全？
类型安全很大程度上可以等价于内存安全，类型安全的代码不会试图访问自己没被授权的内存区域。“类型安全”常被用来形容编程语言，其根据在于该门编程语言是否提供保障类型安全的机制；有的时候也用“类型安全”形容某个程序，判别的标准在于该程序是否隐含类型错误。类型安全的编程语言与类型安全的程序之间，没有必然联系。好的程序员可以使用类型不那么安全的语言写出类型相当安全的程序，相反的，差一点儿的程序员可能使用类型相当安全的语言写出类型不太安全的程序。绝对类型安全的编程语言暂时还没有。

C++保障类型安全机制：
（1）操作符new返回的指针类型严格与对象匹配，而不是void*；
（2）C中很多以void*为参数的函数可以改写为C++模板函数，而模板是支持类型检查的；
（3）引入const关键字代替#define constants，它是有类型、有作用域的，而#define constants只是简单的文本替换；
（4）一些#define宏可被改写为inline函数，结合函数的重载，可在类型安全的前提下支持多种类型，当然改写为模板也能保证类型安全；
（5）C++提供了dynamic_cast关键字，使得转换过程更加安全，因为dynamic_cast比static_cast涉及更多具体的类型检查。
























