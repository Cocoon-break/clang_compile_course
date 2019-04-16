### clang 基础编译3

我们通过编译选项将我们的头文件添加到编译器的搜索头文件的路径中 通过-I 来指定，同时我们将main.cpp  中的代码修改一下,将`#include "function/head.h"`改成`#include <head.h>`

```c
#include <iostream>
#include <head.h>
// using namespace std;
int main(int argc,char *argv[])
{
	std::cout<<add(1,1)<<std::endl;
	return 0;
}
```

我们就使用以下编译命令

```shell
g++ main.cpp function/head.cpp -I function -o main
```

现在在命令中还是使用function/head.cpp。现在去掉这个，那我们应该怎么做呢？

这是我们可以先通过head.cpp生成.o 文件，然后在编译的时候就可以去掉这个路径了。我们先cd 到function 目录下执行

```shell
g++ -c head.cpp -o head.o
```

将生成的head.o  复制到和main.cpp 同级目录下然后执行

```shell
g++ main.cpp head.o -I function -o main
```

这里已经不需要head.cpp了，但是头文件head.h 还是需要的，因为编译main.cpp的时候要用到。当然我们也可以通过三步对上面步骤的总结1.  分别对head.cpp和main.cpp 进行编译。2.链接两个编译之后的.o文件

```shell
cd function
g++ -c head.cpp -o head.o
cp head.o ../
cd ..
g++ -c main.cpp -I function -o main.o
g++ main.o head.o -o main
```



附：
g++ -c 参数说明

```
-c Compile or assemble the source files, but do not link.  The linking stage simply is not done. The ultimate output is in the form of an object file for each source file.
```

g++ -c  参数最终输出的.o 文件是对象文件