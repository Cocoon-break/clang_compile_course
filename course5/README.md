### clang 基础编译5

#### 动态库

先进入到function目录中，使用命令将文件编译成动态库

```shell
g++ add.cpp sub.cpp -fPIC -share -o libhead.so
```

参数说明

-fPIC：表示编译为位置独立的代码，不用此选项的话编译后的代码是位置相关的所以动态载入时是通过代码拷贝的方式来满足不同进程的需要，而不能达到真正代码段共享的目的。

-shared 该选项指定生成动态连接库（让连接器生成T类型的导出符号表，有时候也生成弱连接W类型的导出符号），不用该标志外部程序无法连接。相当于一个可执行文件



接下来我们用利用这个动态库进行编译,返回到main.cpp 所在的目录下，然后执行以下命令

```shell
g++  main.cpp -I function -L function -l head -o main
```

这个编译命令和编译静态的命令没有什么区别。



最后我们去执行生成的main 的二进制。这时我们会发现运行的时候报错` Library not loaded: libhead.so`。在静态编译的时候是可以直接或得结果的，而动态链接库是不行的。

这是我们可以查看我们刚才生成的main二进制使用了哪些动态库。这是我们会发现main需要依赖libhead.so

```shell
#mac 下使用
otool -L main
#linux 下使用
ldd main
```

无论mac 还是linux在查找动态库的地方是先从环境变量LD_LIBRARY_PATH指定的路径，然后是缓存文件/etc/ld.so.cache指定的路径，最后是默认的共享库目录，先是/lib，然后是/usr/lib。

要想运行我们这个main二进制文件我们可以将libhead.so所在的目录添加到环境变量LD_LIBRARY_PATH下

```shell
#linux 下使用
export LD_LIBRARY_PATH=./function:$LD_LIBRARY_PATH
./main
#mac 下使用
export DYLD_LIBRARY_PATH=./function:$DYLD_LIBRARY_PATH
./main
```

**注：**mac下的DYLD_LIBRARY_PATH和Linux的LD_LIBRARY_PATH的作用是一样的，都是动态链接器查找所调用的动态库











