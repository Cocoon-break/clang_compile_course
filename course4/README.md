### clang 基础编译4

#### 静态库

前面已经可以将cpp的文件先生存.o 的对象文件，但是如果function目录下有多个cpp文件。那么需要将所有的cpp文件都生成.o文件，这个工作量是比较大的，这时就可以使用静态库。静态库是将多个.o对象文件打包成一个文件。

目前我们的function 目录有两个cpp文件。分别是add.cpp 和sub.cpp

先将这两个文件编译成.o 文件

```shell
cd function
#生成add.o 和 sub.o
g++ -c sub.cpp add.cpp
```

然后打包成.a静态文件，使用命令

```shell
ar -cr libhead.a add.o sub.o
```

**注：**.a的静态文件要以lib作为前缀，.a作为后缀。

具体的ar参数说明可以使用man ar 查看用法



上面已经编译成静态文件了，接下来我们是在编译的时候如何使用这个静态文件。回到main.cpp的目录执行

```shell
g++ main.cpp -I function -L function -l head -o main 
```

首先参数说明

-I(大写的i)：在之前已经说过这个是将.h添加的编译器的搜索路径中。

-L：这个表示是将.a添加到编译的搜索静态文件的路径中。意思-I差不多。

-l(小写的L)：这个是指定要用的静态库名字。



这里的疑问是为啥-l(小写的L) 后面跟的是head,而不是libhead.a? 

因为编译器会自动在库中添加lib前缀和.a后缀。

这是直接执行这个二进制，可以直接获得结果。









