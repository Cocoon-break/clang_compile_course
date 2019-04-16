### clang 基础编译2

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

回忆上个例子，我们引入了`#include <iostream>`为什么iostream文件不在当前目录下却可以直接使用呢？

编译器会在一些默认的目录下搜索头文件，所以iostream头文件不用添加。编译器默认的include路径我们可以通过命令查看。但是我们并不能没写一个文件就把文件放到系统目录下。

```shell
#查看gcc的include路径命令
`gcc -print-prog-name=cc1` -v
`g++ -print-prog-name=cc1` -v
#查看g++的include路径命令
`gcc -print-prog-name=cc1plus` -v
`g++ -print-prog-name=cc1plus` -v

```



我们可以通过编译选项将我们的头文件添加到编译器的搜索头文件的路径中 通过-I 来指定，同时我们将main.cpp  中的代码修改一下,将`#include "function/head.h"`改成`#include <head.h>`

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

我们就可以使用以下编译命令

```shell
g++ main.cpp function/head.cpp -I function -o main
```

相对couse1中的编译方式，我们可以不用修改代码。直接在编译的命令中指定路径。也就是说即使我们function文件夹名字换成function2，可以通过编译命令进行指定，而不用去修改main.cpp里的代码

```shell
g++ main.cpp function2/head.cpp -I function2 -o main
```



相对于course1来说course2的编译方式有一定的好处，可以修改头文件所在的目录名，意味着其他代码引入head.h的方便。但是还是在命令中使用function/head.cpp。现在去掉这个，那我们应该怎么做呢？请看course3