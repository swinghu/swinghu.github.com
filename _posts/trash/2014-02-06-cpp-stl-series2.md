---
layout: post
title: Learn C++ STL 2---C++模板类
description: C++ STL 系列之---C++模板类，和函数类似，类也可以被一种或者多种类型参数化。其中容器类就是一个具有这种特性的典型例子。
category: trash
---

#一、类模板的实现#
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
	    void push(T const&); //成员方法
	    void pop();
	    T top() const;
	    bool empty() const{
	        return elems.empty();
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
### 类模板的声明 
类模板(*class template*)的声明和函数模板(*function template*)的声明很相似：
### 怎么写成员函数 ##


#二、类模板的使用

#三、类模板的特化

#四、局部特化

#五、缺省模板实参

#小结