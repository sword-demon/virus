---
title: C程序的基础框架
date: 2025-04-27 22:47:58
tags: [C]
categories: [C]
---

## 基础框架

```c
#include <stdio.h>

int main()
{
  return 0;
}
```

- `#include <stdio.h>`：编译预处理指令
- `int main()`: 程序的入口主函数`main`
- 花括号内的内容是你要写的代码
- `return 0;`：程序退出前返回给调用者(操作系统的)值，返回的内容改成什么不影响程序的运行，但是必须是一个`int`类型的数据
- 最后一个花括号结束代表程序结束的标志
- 如果你使用到了`printf`，这个函数在`stdio.h`里面声明了，在对应的`mingw`里面可以找到这个头文件
