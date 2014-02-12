---
layout: post
title: Learn C++ STL 2---C++模板类
description: C++ STL 系列之---C++模板类，和函数类似，类也可以被一种或者多种类型参数化。其中容器类就是一个具有这种特性的典型例子。
category: trash
---

###目录
1. [类模板的实现](#class_sx)
1. [类模板的声明](#ct_define)
1. [怎么写成员函数](#htw_mf)
1. [类模板的使用](#c_template_use)
1. [类模板的特化](#init)
1. [局部特化(偏特化)](#partial_init)
1. [缺省模板实参](#dflt_param)
1. [小结](#end)

#<a id="class_sx">一、类模板的实现</a>
C++模板类，和模板函数类似，类也可以被一种或者多种类型参数化。其中容器类就是一个具有这种特性的典型例子。模板类通常被用来管理组织某种特定类型的元素,只要使用类模板，就可以构造相应的容器类，容器类在定义时不需要确定容器中的元素类型，使用时自动特化，达到多态效果。我们先看一个模板类的实现，然后在分析怎么样声明，定义模板类。如下面的stack模板类的实现：

	#include <iostream>
	#include <vector>
	#include <stdexcept>
	using namespace std;
	
	template <typename T>
	class Stack{	//模板类的什么定义
	private:
	    std::vector<T> elems;	//成员变量
	
	public :
		Stack();	//construction function
	    void push(T const&); //成员方法
	    void pop();	//出栈操作
	    T top() const;	//取得最顶层元素
	    bool empty() const{	//判断是否为空
	        return elems.empty();	//调用vector<> 成员函数
	    }
	};
	
	template <typename T>	//push 入栈操作
	void Stack<T>:: push(T const& elem){
	   elems.push_back(elem);
	}
	
	template <typename T>	//pop  出栈操作
	void Stack<T>::pop(){
	    if(elems.empty()){
	        throw std::out_of_range("Stack<>::pop: empty stack");
	    }
	    elems.pop_back();
	}
	
	template <typename T>
	T Stack<T>::top() const{	//top 取得栈顶元素操作
	    if(elems.empty()){
	        throw std::out_of_range("Stack<>::pop: empty stack");
	    }
	    return elems.back();
	}
	
	int main()
	{
	    Stack<int> int_stck;
	    int_stck.push(4);
	    int_stck.push(5);
	    int_stck.push(6);
	    int_stck.push(100);
	    cout<<"int_stck top is:"<<int_stck.top()<<endl;
	    Stack<char> char_stck;
	    char_stck.push('a');
	    char_stck.push('s');
	    char_stck.push('d');
	    cout<<"char_stck top is:"<<char_stck.top()<<endl;
	    char_stck.pop();
	    cout<<"char_stck top is:"<<char_stck.top()<<endl;
	    return 0;
	}
以上代码是再简单不过了，使用容器vector来存储Stack的数据，这样我们就可以将主要精力放在栈的操作上(而不需考虑栈的数据存储等底层问题)，然后定义了三个普通的栈有关运算操作-push,pop,top，先简单的了解一个模板类的组成，后面再详细说明。在main函数中定义了两个栈-int类型和char类型，模板类经过特化分别构造两个实例。通过编写以上执行结果为：
   
    int_stck top is:100
    char_stck top is:d
    char_stck top is:s
##<a id="ct_define">类模板的声明 </a>
类模板(*class template*)的声明和函数模板(*function template*)的声明很相似：先声明类型参数的标识符，使用T，如 *class/typename T*：
	
	template<typename T>
	class Stack{
		...
		//define and operation	
	};
对于模板类来说，我们通常使用class 来定义类型，而不是typename原由如下（来自[stackoverflow](http://stackoverflow.com/questions/213121/use-class-or-typename-for-template-parameters)）：
> Stan Lippman talked about this here. I thought it was interesting.
> Summary: Stroustrup originally used class to specify types in templates to avoid introducing a new keyword. Some in the committee worried that this overloading of the keyword led to confusion. Later, the committee introduced a new keyword typename to resolve syntactic ambiguity, and decided to let it also be used to specify template types to reduce confusion, but for backward compatibility, class kept its overloaded meaning.
> 
> And don't forget to read into the comments for whether there's a good reason to use "class" rather than "typename". –  Michael Burr Oct 17 '08 at 22:06
> 	  	
> I think defacto StackOverflow ettiquette is to offer a few line summary if you are going to defer to a "look here". –  Catskul Oct 5 '09 at 15:53
> 	  	
> I wrote this response nearly a year ago, about a month after the site went public. There was hardly a defacto anything at that point. Point taken, though. –  itsmatt Oct 5 '09 at 16:20
> 	  	
> REVIVAL! I don't find that article particularly clear, to be honest. in T::A *obj; the language, as far as I know, should parse the statement as a declaration because of the declaration rule: anything that looks like a declaration, even if it ambiguously looks like something else, should resolve into a declaration[0]. I also didn't find Bjarne Stroustrup clear about this. [0] The C++ Programming language 3e, Stroustrup, Appendix C.13.5, p. 856-858 –  wilhelmtell Apr 8 '10 at 23:29
>   	
> Can we revisit this answer, and turn it into an ... answer? –  Lightness Races in Orbit Nov 9 '11 at 22:56
> 
> According to Scott Myers, Effective C++ (3rd ed.) item 42 (which must, of course, be the ultimate answer) - the difference is "nothing".
> 
> Advice is to use "class" if it is expected T will always be a class, with "typename" if other types (int, char* whatever) may be expected. Consider it a usage hint.

由Scott Myers, Effective C++ (3rd ed.) item 42条规则，两者的真正区别是："nothing"

总之一句话要是考虑向后兼容性使用*class*，如果T作为一个类使用的话使用*class*，其他类型使用*typename*

在`template <typename T>`中T称为**模板参数**，定义后可以在类模板中使用，使用前要明确认识的一个问题是，该类的类型是什么？ `Stack or Stack<T>`，在这里是Stack<t>,由此在声明中要使用该类型时，必须使用 `Stack<T>`，例如，在编写成员函数时(拷贝构造函数和赋值操作符)
	
	Stack (Stack<T> const&);	//拷贝构造函数
    Stack<T> operator= (Stack<T> const& );	//赋值运算符
##<a id="htw_mf">怎么写成员函数</a>
在实现成员函数时，必须指定该成员函数是一个函数模板，并且还需使用这个类模板的完整类型限定符(即：`Stack<T>::`)。如pop函数的实现：
	
	template <typename T>
	void Stack<T>::pop(){
	    if(elems.empty()){
	        throw std::out_of_range("Stack<>::pop: empty stack");
	    }
	    elems.pop_back();//将栈顶元素删除(弹出)，此处调用vector成员方法，没有获取该元素
	}
当然如果要保存pop的元素，pop成员函数也可以这么写
	
	template<typename T>
	T Stack<T>:: pop(){
	    if(elems.empty()){
	        throw std::out_of_range("Stack<>::pop empty Stack");
	    }
	    T elem = elems.back();
	    elems.pop_back();
	    return elem;
	}
之前的那个就要删掉，否则会报错，提示不能重载：

    stlcpp2_1\main.cpp|18|error: 'T Stack<T>::pop()' cannot be overloaded|
同样的你可以将类的成员函数在类的内部声明时同时定义好,如：
	
	template <typename T>
	class Stack{
		...
		void push(T const& elem)
		{
			elems.push_back(elem);
		}
	}



#<a id="c_template_use">二、类模板的使用</a>
类模板在使用时才进行实例化，如在定义int_stck时，将类模板实例化为 int(用int实例化T)。int_stck是一个创建自`Stack<int>`的对象，元素存用vector存储(具体为elems)，类型为int(私有成员变量elems，用int实例化T)。

1. 当有成员函数被调用的时候，成员函数中的T相应的被实例化(只有被使用过，才被实例化，产生实例化代码，这样有利于提高空间和时间效率)
2. 对于那些“未能提供所有成员函数中的所有操作的”类型，你也可以使用该类型来实例化类模板，只要内模板内部不使用那些“未能提供的操作”
3. 类模板中的有静态成员，用来实例化模板的每种类型都会“copy”式的实例化该静态成员
4. 实例化的类模板类型在使用时和其他类型一样，只要实例化类模板类型的对象支持该操作

	    void foo (Stack<int> const& s)
    	{
    		Stack<int> istack[10];
    		......
    	}
5. 结合类型定义typedef，可以更简便的使用类模板如：`typedef Stack<int> IntStack;`
6. 模板实参可以是任何类型，`float* ,Stack<int>`都可以，如：
		
    	Stack<float*> floatStack;
    	Stack<Stack<int>>	intStackStack;
在新的C++标准中，定义中出现的">>"不需要空格分开成“> >"

#<a id = "init">三、类模板的特化 </a>
类比函数模板的重载，可以用模板实参类特化类模板。通过特化类模板，可以对某种特定类的实现进行优化，克服某些不足(举个例子，某个类模板没有提供某种操作,但是我在实例化后又想使用)。

在特化类模板时，还需将所有成员函数一并特化(虽然可以，但是如果没有全部进行特化，那么就没特化整个模板类)。

特化类模板的方法:


1. 必须在代码首行声明一个` template<>`,接下来声明用来特化类模板的类型：在类名后面指定该类型：
	
    	template<>
    	class Stack<std::string>{
    		......
    	}
1. 将所有成员函数重新定义为普通函数，将原来函数中的T用相应的特化类型进行取代
如
	
    	void Stack<std::string>:: push(std::string const& elem)
    	{
    		elems.push_back(elem);
    	}
整理以上所述，结合一个完整例子进行说明(`std::string`特化版的`Stack<>`)

		//--------------------------stack1.hpp 头文件
    	#include<vector>
    	#include<stdexcept>
    	#include <iostream>
		template <typename T>
		class Stack{
		private:
		    std::vector<T> elems;
		
		public :
		
		    void push(T const&);
		    void pop();
		    T top() const;
		    bool empty() const{
		        return elems.empty();
		    }
		
		};
		
		template <typename T>
		void Stack<T>:: push(T const& elem){
		   elems.push_back(elem);
		}
		
		template <typename T>
		void Stack<T>::pop(){
		    if(elems.empty()){
		        throw std::out_of_range("Stack<>::pop: empty stack");
		    }
		    elems.pop_back();
		}
		
		template <typename T>
		T Stack<T>::top() const{
		    if(elems.empty()){
		        throw std::out_of_range("Stack<>::pop: empty stack");
		    }
		    return elems.back();
		}
 		
实例测试实现为

		//-----------------------------c++ main.cpp
		#include <iostream>
		#include "stack1.hpp"
		#include <deque>
		#include <stdexcept>
		using namespace std;
		template<>
		class Stack<std::string>
		{
		private :
		    std::deque<std::string> elems;
		
		public:
		    void push(std::string const&);
		    void pop();
		    std::string top() const;
		    bool empty() const
		    {
		        return elems.empty();
		    }
		};
		
		void Stack<std::string>:: push(std::string const& elem)
		{
		    elems.push_back(elem);
		}
		void Stack<std::string>:: pop()
		{
		    if(elems.empty())
		    {
		        throw std::out_of_range("Stack<std::string>::pop :empty stack ");
		    }
		    elems.pop_back();
		}
		std::string Stack<std::string>:: top() const
		{
		    if(elems.empty())
		    {
		        throw std::out_of_range("Stack<std::string>::top :empty stack ");
		    }
		    return elems.back();
		}
		
		
		
		int main()
		{
		    Stack<std::string> strStack;
		    strStack.push("helloworld");
		    strStack.push("Lily and lucy");
		    strStack.push("hello c++");
		    strStack.push("hello STL");
		    strStack.push("hello SGI");
		

		    while(!strStack.empty())
		    {
		        cout<<"the top element is: "<<strStack.top()<<endl;
		        strStack.pop();
		    }
		
		    Stack<int> intStack;
		    intStack.push('a');
		    intStack.push('z');
		    intStack.push(3567);
		    cout<<"the top elem of intStack is : "<< intStack.top()<<endl;
		}
		/*
		the top element is: hello SGI
		the top element is: hello STL
		the top element is: hello c++
		the top element is: Lily and lucy
		the top element is: helloworld
		the top elem of intStack is : 3567
		*/
在以上实例中使用deque，而不是vector来管理存储Stack内部的元素。说明：特化的实现可以和基本类模板的实现完全不同。

#<a id = "partial_init">四、局部特化(偏特化)</a>
和函数模板可以局部特化类似，类模板也可以被局部特化,用户在需要是指定特化类型，以达到满足用户自定义需求。如类模板
	
	//-----------------------------stack1.hpp 
	template<typename T,typename P>
	class MyClass{
	private:
	    T t_value;
	    P p_value;
	public:
	    T get_t()
	    {
	        return t_value;
	    }
	    P get_p()
	    {
	        return p_value;
	    }
	    void set_t(T t_v)
	    {
	        t_value = t_v;
	    }
	    void set_p(P p_v)
	    {
	        p_value = p_v;
	    }
	};
用户可以自行决定怎么样特化类模板，在此略举以下几种局部特化

1. 局部特化：两个模板参数具有相同类型
	
		template<typename T>
		class MyClass<T,T>{
			......
		};
2. 局部特化：第二个模板参数类型为 int

		template<typename T>
		class MyClass<T,int>{
			.....
		};
3. 局部特化：两个模板参数是指针类型

		template<typename T1,typename T2>
		class MyClass<T1*,T2*>{
			.....
		};

对于第二种局部特化的例子完整的实现为：
	
	//-----------------------------main.cpp
	//局部特化 Myclass
	template<typename T>
	class MyClass<T,int>{
	   private:
	    T t_value;
	    int p_value;
	public:
	    T get_t()
	    {
	        return t_value;
	    }
	    int get_p()
	    {
	        return p_value;
	    }
	    void set_t(T t_v)
	    {
	        t_value = t_v;
	    }
	    void set_p(int p_v)
	    {
	        p_value = p_v;
	    }
	};

局部特化的二义性,指的是当有多种局部特化时，可以会存在多个匹配，此时就成为二义性，例如：
	
	MyClass<int ,int> int_intm;     //错误：同时匹配MyClass<T,T>和 MyClass<T ,int>
	Myclass<float* ,float*> f_fm	//错误：同时匹配MyClass<T,T>和 MyClass<T1*,T2*>
#<a id = "dflt_param">五、缺省模板实参</a>
对于类模板，可以为模板参数定义缺省值：这些值就称为缺省模板实参。看实例

	//-----------------------------stack3.hpp
	#include<vector>
	#include<stdexcept>
	//缺省模板参数,容器：存储T类型的元素。改为template<typename T,typename CONT = std::vector<T>>出错
	template<typename T,typename CONT = std::vector<T> >
	class Stack{
	    private:
	        CONT elems;
	    public:
	        void push(T const&);
	        void pop();
	        T top() const;
	        bool empty()const{
	            return elems.empty();
	        }
	};
	//使用正确的类类型，由于类模板有两个参数，
	//所以所有成员函数也需要两个参数，以达到类型一致
	template<typename T ,typename CONT>
	void Stack<T,CONT>::pop(){
	    if(elems.empty()){
	        throw std::out_of_range("Stack<T,CONT>:: pop:empty stack");
	    }
	    elems.pop_back();
	}
	template<typename T ,typename CONT>
	void Stack<T,CONT>::push(T const& elem){
	    elems.push_back(elem);
	}
	template<typename T ,typename CONT>
	T Stack<T,CONT>:: top() const{
	    if(elems.empty()){
	        throw std::out_of_range("Stack<T,CONT>:: pop:empty stack");
	    }
	    return elems.back();
	}
实例测试实现为

	//-----------------------------c++ main.cpp
	#include <iostream>
	#include <deque>
	#include "stack3.hpp"// 改为：#include <stack3.hpp>出错
	
	
	using namespace std;
	
	int main()
	{
	    Stack<int> intStack;// 使用默认类模板参数vector<int>
	    intStack.push(12);
	    intStack.push(34);
	    intStack.push(56);
	    intStack.push(910);
	    cout<<"the top elem of intStack is " <<intStack.top()<<endl;
	    intStack.pop();
	    cout<<"After pop ,the top elem of intStack is " <<intStack.top()<<endl;
	    Stack<double ,std::deque<double> > dblStack;//使用自定义模板参数容器deque<double>
	    dblStack.push(12);
	    dblStack.push(34);
	    dblStack.push(56);
	    dblStack.push(19);
	    cout<<"the top elem of dblStack is "<<dblStack.top()<<endl;
	    dblStack.pop();
	    dblStack.pop();
	    dblStack.pop();
	    dblStack.pop();
	    cout<<"After pop ,the top elem of dblStack is "<<dblStack.top()<<endl;
	    return 0;
	}

#<a id = "end">小结</a>
1. 所谓的类模板(class template)是包含一个或者多个尚未确切定义的类别的class
2. 必须实例化类别参数 T，才能使用类模板，这样后成员函数，变量以该实例化类型去实例化，编译器生成实例化代码
3. 类模板中只有真正调用的函数，才会被实例化
4. 可以对类模板进行特化
5. 可以对类模板进行偏特化，偏特化时可能会产生二义性
6. 可以对类模板定义缺省模板实参，该预设定义可以使用前一步定义的模板参数