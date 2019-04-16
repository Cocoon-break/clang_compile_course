### clang 基础编译

main.cpp

```c
#include <iostream>
#include "function/head.h"
// using namespace std;
int main(int argc,char *argv[])
{
	std::cout<<add(1,1)<<std::endl;
	return 0;
}
```

main.cpp 中使用了一个add(1,1)函数，这个函数在默认的include路径下没有，所以我们自己申明了add函数是在head.h 文件中。如果没有引入head.h 头文件就会报**use of undeclared identifier 'add'**，这里我们使用了`#include "function/head.h"`，这种方式是使用了相对路径的引入方式。也就是说在main.cpp的同级目录下有function/head.h文件

这里我们使用的编译命令是

```shell
g++ main.cpp function/head.cpp -o main
```

用这种相对路径包含头文件有很多问题，相对于main.cpp 的function 文件夹路径不能变，也不能修改文件夹名字。如果head.h 文件被很多其他文件包含的话就会有很多问题，而且工作量较大。



这时我们发现我们也引入了`#include <iostream>`为什么iostream文件不在当前目录下却可以直接使用呢？请看course2

