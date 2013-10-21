---
layout: post
title: 并查集在求解子图中的应用--union find algorithm
category: blog
description: 利用并查集求解graph中的子图以及连通性问题
---

##1.并查集
最近在解决一个图的问题，问题要求解一个图中的各个子图，并且将连通子图顶点和边输出来，首先想到的是用BFS，或者什么DFS，但是数据集开始用的C++ STL中的mulitmap存储，并没有按照经典的图的存储模型邻接表，或者邻接矩阵存储，所以BFS、DFS算法操作起来不是很方便，
进而google，了解到并查集这一概念。了解到并查集可以求解无向图的连通分量个数， 将其应用到Kruskar算法求最小生成树，ACM中朋友与敌人的问题（朋友的朋友是朋友，敌人的敌人是朋友），进而学习了一番。
并查集是一种树形的数据结构，其保持着处理一些不相交集合（Disjoint Sets）的合并及查询问题。有一个联合-查找算法（union-find algorithm）定义了两个操作用于此数据结构：

<li>getAcestor：确定元素属于哪一个子集。它可以被用来确定两个元素是否属于同一子集。</li>

	int getAcestor(int c)
	{
		if (ancestor[c] == c)
			return c;
		return ancestor[c] = getAcestor(ancestor[c]);
	}

<li>Union：将两个子集合并成同一个集合，如果他们之间有某种关系。</li>

	void Union(int x,int y){
		int fx=getAcestor(x);
		int fy=getAcestor(y);
		if (fx==fy) return ;
		ancestor[fx]=fy;
	}

因为它支持这两种操作，一个不相交集也常被称为联合-查找数据结构（union-find data structure）或合并-查找集合（merge-find set）。
有了以上这些方法，就可以解决许多经典的节点划分问题。

##2.本例给出一个以求解子图的应用，以下是应用中的核心代码。

	int edges=0;
	int vers = 0;
	int a,b ;
	vers = is_kcore_node.size();
	edges = tempkcoremap.size() ;//(multimap<string,string>
	cout<<"节点数："<<vers<<"  "<<"边数："<<edges<<endl;
	
###起始设置每个节点为单独的一个集合

	for (int i = 1; i <= vers; i++)
	{
		ancestor[i] = i;
	}

###	执行union操作


	for (int i = 1 ; i <= edges; i++)
	{
	for (multimap<string,string>::iterator mmiter = tempkcoremap.begin(); mmiter != tempkcoremap.end(); mmiter++)
		{

			a = (hash_map_data.find((*mmiter).first))->second;
			b = (hash_map_data.find((*mmiter).second))->second;

			Union(a,b);
		}
	}
	
###执行union操作后 ，ancestor[]存储每个节点的所属集合,从输出的信息就可以大概知道哪些节点是属于同一个子图的

	cout<<"并查集结果:"<<endl;
	for (int i =1 ;i<=vers ; i++)
	{
		cout<<ancestor[i]<< " ";
	}
	
	
###求解子图个数

	// sub kcore num @subcorenum
	set<int>iset;
	for (int i = 1 ; i<= vers ; i++)
	{
		iset.insert(ancestor[i]);
	}
	int subcorenum = iset.size();
	cout<<"kcore 子图数目： "<< subcorenum<<endl;


	
###输出每个子图的信息，顶点，每个子图的边的信息
	
	int signal[MAX];
	for (int i = 1; i <= vers; i++)
	{
		signal[i] = 0;
	}
	int core  = 1;
	
	for (int i =1 ; i<=vers ; i++)
	{
		if (signal[i] ==0)
		{
			cout<<"core"<<"["<<core++<<"]"<<"节点数据:";
			vector<string>coreifovect;
			signal[i] =1;

			coreifovect.push_back((hash_i2s_data.find(i))->second);
			for (int j = i+1; j <= vers; j++)
			{

				if (ancestor[j] == ancestor[i] && signal[j] != 1)
				{
					string str= (hash_i2s_data.find(j))->second;
					coreifovect.push_back((hash_i2s_data.find(j))->second);
					signal[j] = 1;
				}
			}
			for (int i = 1;i<vers; i++)
			{
				cout<<signal[i];
			}
			cout<<endl;
			cout<<"节点信息：";
			for (vector<string>::iterator iter = coreifovect.begin(); iter != coreifovect.end(); iter++)
			{
				cout << *iter<<endl;
			}
			cout<<"边的信息："<<endl;
			for (vector<string>::iterator str_vect = coreifovect.begin(); str_vect !=coreifovect.end(); str_vect++)
			{
				string strtmp = *str_vect;
				for (multimap<string,string>::iterator iter = tempkcoremap.begin(); iter != tempkcoremap.end(); iter++)
				{
					if ((*iter).first == strtmp || (*iter).second == strtmp)
					{
						cout<<(*iter).first<<"  " <<(*iter).second<<endl;
						tempkcoremap.erase(iter);
					}

				}

			}						
		}

	}



