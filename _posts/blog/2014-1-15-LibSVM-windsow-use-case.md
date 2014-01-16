---
layout: post
title: 利用libsvm使用简单数据跑支持向量机
description: windows libsvm python 支持向量机svm
category: blog
---

##libsvm介绍

### [LIBSVM][LIBSVM] 
>    `A Library for Support Vector Machines
>    LIBSVM is an integrated software for support vector classification, (C-SVC, nu-SVC), regression (epsilon-SVR, nu-SVR) 
>and distribution estimation (one-class SVM). It supports multi-class classification.
>Our goal is to help users from other fields to easily use SVM as a tool. LIBSVM provides a simple 
>interface where users can easily link it with their own programs. Main features of LIBSVM include
>    Different SVM formulations
>    Efficient multi-class classification
>    Cross validation for model selection
>    Probability estimates
>    Various kernels (including precomputed kernel matrix)
>    Weighted SVM for unbalanced data
>    Both C++ and Java sources
>    GUI demonstrating SVM classification and regression
>    Python, R, MATLAB, Perl, Ruby, Weka, Common LISP, CLISP, Haskell, OCaml, LabVIEW, and PHP interfaces. C# .NET code and CUDA extension is available. (多语言多平台支持)
>    It's also included in some data mining environments: RapidMiner, PCP, and LIONsolver.
>    Automatic model selection which can generate contour of cross valiation accuracy.`
###Download LIBSVM
>`The current release (Version 3.17, April 2013) of LIBSVM can be obtained by downloading the [zip file][zip_file]or [tar.gz][tar_gz] file. You can also check this [github][github]directory. The package includes the source code of the library in C++ and Java, and a simple program for scaling training data. A README file with detailed explanation is provided. For MS Windows users, there is a subdirectory in the zip file containing binary executable files. Precompiled Java class archive is also included.(压缩文件中已经包含matlab,python,java等版本)`

##运行前需安装软件
(1)[Python][python]
到http://www.python.org/download/ 官网提示(The current production versions are Python 2.7.6 and Python 3.3.3.)下载完直接安裝就好(最好在最后一步，将提示“python加入到path路径”中的选项选上)。
我的电脑上安装的是python2.7(应该对版本没什么特别要求，尽量使用新版本的python)
(2)[Gnuplot][gnuplot]安装
本机使用09.10.2013: Release gnuplot 4.6.4，到官网上找到download的链接，点击[下载]([gnuplot_download]在这里提供链接：http://sourceforge.net/projects/gnuplot/files/latest/download?source=files)下载好,点击安装即可(可更改安装目录，但请记住，因为后面如果出现错误：gnuplot executable not found就要用到)
(3)下载libsvm包
下载地址前文已经给出(下载zip格式的那个压缩包)。假设解压在D:\libsvm-3.17目录
##使用libsvm进行数据测试
###下载数据集
本文使用数据集为libsvm官网提供的UCI公共数据集中的a1a。以下是该数据集的一些介绍:
•Source: UCI / Adult
•Preprocessing: The original Adult data set has 14 features, among which six are continuous and eight are
categorical. In this data set, continuous features are discretized into quantiles, and each quantile is 
represented by a binary feature. Also, a categorical feature with m categories is converted to m binary features.
Details on how each feature is converted can be found in the beginning of each file from this [page][uci_data].
[JP98a] 
•# of classes: 2
•# of data: 1,605 / 30,956 (testing) 
•# of features: 123 / 123 (testing) 
•Files: 
 ◦[a1a][a1a]
 ◦[a1a.t][ala_t](testing)
    
原始数据的介绍如下:
`This archive contains a nested set of training data for the UCI "adult"
benchmark. Each file is in .dst format, which will be described below. The
benchmark task is to predict whether a household has >$50K income based on
14 other fields in a census form. Eight of those fields are categorical,
while six are continuous(注：年龄:age，接受教育的时间程度：eduVal). The six fields are quantized into quintiles(
注：连续的Feature，按五分之一被分成五个类),
which yields a total of 123 sparse binary features.`
数据下载好后，将数据拷贝到之前解压libsvm中的windows目录里面(两个文件应该是:a1a和a1a.t。其实新建一个data文件夹也可以,在使用命令时，指定该目录就行，当时没注意！！)
###所使用到的exe文件
在进行测试的时候，主要用到window下面的以下几个exe文件和一个python文件(所以要安装python)
svm-scale.exe:该文件可以将数据集(训练和测试数据集)的feature的范围进行调整，也就是对数据集进行归一化(调整到0～1或者-1～+1之间)，以避免某一项feature的值过高(之处一定要对训练集和测试集同时进行缩放)
具体用法为：

    svm-scale [-l lower][-u upper]
        [-y y_lower yupper]
        [-s save_filename]
        [-r restore_filename] filename

    -l：设定数据下限，缺省值为-1
    -u：设定数据上限，缺省值为1
    -s：将缩放的规则保存为文件save_filename
    -r: restore_filename,表示将按照已经存在的规则文件restore_filename进行缩放  
    filename：带缩放的数据文件(训练数据集)，文件格式参见libsvm格式
例如：

    svm-svale -l 0 -u 1 -s test.range test.txt > out.txt 

svm-train.exe:该文件可以将训练数据集(training data)做成一個model
    具体用法为参数设置：   
svm-train [options]training_set_file[model_file]
    options为操作参数，可选参数为：
![synchronizes-with](/images/libsvm1/svm-s-t.png)
![synchronizes-with](/images/libsvm1/svm-d.png) 

svm-predict.exe:该文件可以使用已有的model(svm-train.exe)对测试集进行预测
svmtoy.exe：一个基于java的窗口应用程序，可以在里面选择某种颜色点击"画出"一些点，然后Change，改变颜色就可以画出另外一种
颜色的点出来，不同颜色代表不同的类，然后点击Run，该工具可以进行svm分类。
    
###dataset的格式要求(以后只要将数据集制作成这个格式就行，可能还支持其他格式，没有测试过)

    -1 3:1 11:1 14:1 19:1 39:1 42:1 55:1 64:1 67:1 73:1 75:1 76:1 80:1 83:1 
    -1 3:1 6:1 17:1 27:1 35:1 40:1 57:1 63:1 69:1 73:1 74:1 76:1 81:1 103:1 
    -1 4:1 6:1 17:1 22:1 36:1 40:1 50:1 63:1 67:1 73:1 74:1 76:1 80:1 83:1 
    +1 4:1 6:1 15:1 22:1 36:1 40:1 50:1 63:1 67:1 73:1 74:1 76:1 82:1 83:1 
    +1 5:1 6:1 17:1 25:1 38:1 40:1 51:1 63:1 67:1 73:1 74:1 76:1 80:1 88:1 
    -1 4:1 6:1 14:1 22:1 36:1 42:1 54:1 64:1 67:1 73:1 74:1 76:1 80:1 83:1 
    +1 3:1 6:1 17:1 29:1 39:1 40:1 52:1 63:1 67:1 73:1 74:1 76:1 79:1 83:1 
    -1 3:1 6:1 18:1 19:1 39:1 40:1 50:1 61:1 67:1 72:1 74:1 76:1 78:1 83:1 
    -1 2:1 6:1 14:1 24:1 38:1 40:1 53:1 63:1 67:1 73:1 74:1 76:1 80:1 83:1   
冒号前后分别代表的是是feature的编号和数值，一行为一个example，如第一行中有属性：3，11，14，19，39，42，55，64，67，73，75，，76，80，83(这些属性ID号，可以在事先给予编号，如3：代表学历，受教育程度等等)。最前面数字的是分类的编号，本数据集(训练数据集)两个类：-1，+1。“-1”代表收入大于50k的人是在14个城市里面，+1代表收入大于50k的人不是在14个城市里面。
##对数据集进行scale(归一化)
当自定义格式的数据需要归一化的时候，使用以下命令
    
    svmscale.exe –s scale trainingdata > trainingdata.scale 
    svmscale.exe –r scale testdata > testdata.scale 
           
其中用到了shell中的 “>”重定向操作符，就是将运行的结果存储到另一个文中。
###实验流程及结果
####(i)对数据进行scale(归一化)
先对ala文件归一化

    D:\libsvm-3.17\windows>svm-scale.exe -s scale a1a > ala.scale
        
        WARNING: original #nonzeros 22249
                 new      #nonzeros 181365
        Use -l 0 if many original feature values are zeros

然后对ala.t文件进行归一化

    D:\libsvm-3.17\windows>svm-scale.exe -r  scale a1a.t > ala.t.scale
       
       WARNING: feature index 12 appeared in file a1a.t was not seen in the scaling fac
        tor file scale.
        WARNING: feature index 60 appeared in file a1a.t was not seen in the scaling fac
        tor file scale.
        WARNING: feature index 121 appeared in file a1a.t was not seen in the scaling fa
        ctor file scale.
        WARNING: feature index 122 appeared in file a1a.t was not seen in the scaling fa
        ctor file scale.
        WARNING: feature index 123 appeared in file a1a.t was not seen in the scaling fa
        ctor file scale.
        WARNING: original #nonzeros 429343
                 new      #nonzeros 3807588
        Use -l 0 if many original feature values are zeros       
注意文件名，我测试的时候提示总是打不文件a1a，通过拷贝那个文件名才解决这个问题
####(ii)为交叉验证选择参数：

    D:\libsvm-3.17\windows>python D:\libsvm-3.17\windows\grid.py D:\libsvm-3.17\windows\a1a
运行结果为：

    [local] 5 -7 82.4299 (best c=32.0, g=0.0078125, rate=82.4299)
    [local] -1 -7 78.5047 (best c=32.0, g=0.0078125, rate=82.4299)
    [local] 5 -1 79.3146 (best c=32.0, g=0.0078125, rate=82.4299)
    [local] -1 -1 76.8224 (best c=32.0, g=0.0078125, rate=82.4299)
    [local] 11 -7 79.4393 (best c=32.0, g=0.0078125, rate=82.4299)
    [local] 11 -1 79.3146 (best c=32.0, g=0.0078125, rate=82.4299)
    
    ::::::::::::::::::::省略中间一些结果::::::::::::::::::::::::::::
    [local] 13 -11 82.3676 (best c=2.0, g=0.0078125, rate=82.9907)
    [local] 13 -5 77.5701 (best c=2.0, g=0.0078125, rate=82.9907)
    [local] 13 -15 82.1807 (best c=2.0, g=0.0078125, rate=82.9907)
    [local] 13 3 75.4517 (best c=2.0, g=0.0078125, rate=82.9907)
    [local] 13 -9 80.4984 (best c=2.0, g=0.0078125, rate=82.9907)
    [local] 13 -3 79.0654 (best c=2.0, g=0.0078125, rate=82.9907)
    2.0 0.0078125 82.9907               ----注：最后结果，我们在下一步用到

有必要注意一下grid.py的工作方式，它是采用暴力方法对参数进行尝试试验，整个跑完之后给出一个结果,结果为一个一行三列的数据，
如本例中的：2.0 0.0078125 82.9907 前两个数字为：c和γ，这是对C-SVC的参数c和γ做优选的最后的结果，最后一个数字表示的是交叉验证精度CV Rate = 82.9907%

####((iii)接上一步骤，获取cross validation参数

获取最佳交叉验证(cross validation)参数（就是grid.py作的事）
运行命令

    ---D:\libsvm-3.17\windows>python D:\libsvm-3.17\windows\grid.py D:\libsvm-3.17\wind
ows\ala.scale
    结果如下(部分)
    
    [local] 5 -7 80.4361 (best c=32.0, g=0.0078125, rate=80.4361)
    [local] -1 -7 82.6791 (best c=0.5, g=0.0078125, rate=82.6791)
    [local] 5 -1 75.4517 (best c=0.5, g=0.0078125, rate=82.6791)
    [local] 13 -5 79.0654 (best c=2.0, g=0.001953125, rate=82.9907)
    [local] 13 -15 82.1807 (best c=2.0, g=0.001953125, rate=82.9907)
    [local] 13 3 75.4517 (best c=2.0, g=0.001953125, rate=82.9907)
    [local] 13 -9 77.757 (best c=2.0, g=0.001953125, rate=82.9907)
    [local] 13 -3 79.3146 (best c=2.0, g=0.001953125, rate=82.9907)
    2.0 0.001953125 82.9907         ----我们需要的结果
    
机器就开始尝试暴力求解最佳参数，同时gnuplot 4.6开始绘制图形，如下图所示
![synchronizes-with](/images/libsvm1/gridpy1.png)
![synchronizes-with](/images/libsvm1/gridpy2.png)
![synchronizes-with](/images/libsvm1/gridpy4.png)
![synchronizes-with](/images/libsvm1/gridpy5.png)

####((iv)接上一步骤，进行train试验
我们得到最后一行，最佳交叉验证参数2.0 0.001953125 82.9907，只是用到前面两个参数。进行train
运行命令，得到以下结果
   
    D:\libsvm-3.17\windows>svm-train -c 2.0 -g 0.001953125 a1a.scale
    得到以下结果
    *
    optimization finished, #iter = 553
    nu = 0.430949
    obj = -1271.932734, rho = 0.547671
    nSV = 715, nBSV = 677
    Total nSV = 715
    
####((v)进行预测
运行命令，得到以下结果
    
    D:\libsvm-3.17\windows>svm-predict a1a.t.scale a1a.scale.model a1a.t.out
    结果：
    Accuracy = 84.0225% (26010/30956) (classification)

##总结
整个操作流程可以归结为以下几步：
<ul>
<li>把实验数据转换成libsvm能识别的格式</li>
<li>数据是否需要归一化，如需要，对数据进行Scaling </li>
<li>选用效能好的RBF kernel(程序预设的默认值选择的是RBF，所以不用管道这一行)</li>
<li>为交叉验证(cross validation)选择参数（就是grid.py作的事）</li>
<li>用步骤四得到的参数来train model (svm-train)</li>
<li>对测试数据集进行测试Test(svm-predict)</li>
</ul>


[LIBSVM]: http://www.csie.ntu.edu.tw/~cjlin/libsvm/
[zip_file]:http://www.csie.ntu.edu.tw/~cjlin/libsvm+zip 
[tar_gz]:http://www.csie.ntu.edu.tw/~cjlin/cgi-bin/libsvm.cgi?+http://www.csie.ntu.edu.tw/~cjlin/libsvm+tar.gz
[github]:https://github.com/cjlin1/libsvm
[python]:http://www.python.org/download/
[gnuplot]:http://gnuplot.info/
[gnuplot_download]:http://sourceforge.net/projects/gnuplot/files/latest/download?source=files
[uci_data]:http://research.microsoft.com/en-us/um/people/jplatt/adult.zip
[a1a]:http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/a1a
[ala_t]:http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/a1a.t


