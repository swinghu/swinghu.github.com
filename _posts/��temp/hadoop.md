C:\Ruby200\bin;
C:\RailsInstaller\Git\cmd;
C:\RailsInstaller\Ruby1.9.2\bin;
C:\Perl\site\bin;
C:\Perl\bin;%M2_HOME%\bin;
%JAVA_HOME%\jre\bin;
C:\Program Files\Java\jdk1.6.0_43\jre\bin;
%M2_HOME%\bin;
%SystemRoot%\system32;
%SystemRoot%;%SystemRoot%\System32\Wbem;
C:\Program Files\Calibre2\;
D:\Program Files\R\R-3.0.2\bin\i386;
D:\Program Files\R\R-3.0.2\library\rJava\jri;
D:\Program Files\gnuplot\bin;C:\Python27\
D:\Java\jdk1.7.0_45\jre\lib;,;



http://blog.csdn.net/liu_jason/article/details/7704399
./hadoop jar ./../hadoop-examples-1.0.3.jar wordcount data_in data_out

cd 目录：
/cygdrive/d/hadoop/deploy/hadoop-1.0.3/bin
格式化namenode：
./hadoop namenode-format
启动hadoop：
./start-all.sh
关闭hadoop：
，执行./stop-all.sh即可

在前面的步骤中，我们已经建立了hadoop环境，下面该运行一个实例了，就拿hadoop自带的wordcount练手吧。

- 建立本地数据文件

在我们准备的hadoop本地文件夹data下建立一个data_in文件夹，并在此文件夹下创建两个数据文件，分别是file1.txt和file2.txt。

file1.txt中保存一个句子：Hello world!

file2.txt中保存一个句子：I am the king of the world!

- 上传数据文件至dfs文件系统

下面我们要将本地建立的两个数据文件上传到hdfs文件系统中。

（以下过程，如果没有启动hadoop环境，请参考hadoop安装过程中启动hadoop的方法先启动hadoop环境，否则会看到“Retrying connect to server”的错误）

* 进入cygwin环境

* 进入hadoop的bin目录：cd /cygdrive/d/hadoop/deploy/hadoop-1.0.3/bin

* 在hdfs上建立data_in目录：./hadoop dfs -mkdir data_in

* 上传数据文件：./hadoop dfs -put /hadoop/data/data_in/*.txtdata_in

* 查看文件上传成功：./hadoop dfs -ls data_in

整个过程如下图所示：


- 执行wordcount程序

数据文件准备好了，我们就可以执行wordcount程序了。

在hadoop的bin目录下执行：

./hadoop jar ./../hadoop-examples-1.0.3.jarwordcount data_in data_out

  ERROR security.UserGroupInformation: PriviledgedActionException as:swinghu cause:java.net.ConnectException: Call to localhost/127.0.0.1:9001 failed on connection exception: java.net.ConnectException: Connection refused: no further information
$  jar hadoop-examples-1.0.3.jar wordcount data_in data_out



hadoop jar ./../ hadoop-examples-1.0.3.jar wordcount data_in data_out

 ./hadoop jar ./../hadoop-examples-1.0.3.jar wordcount data_in data_out

