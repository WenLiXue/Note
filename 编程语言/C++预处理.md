# C++预处理

## 介绍

预处理是在编译之前的处理，而编译工作的任务之一是语法检查，，预处理不做语法检查，预处理命令以"#"开头

## 常用预处理指令

- 宏定义

  ```cpp
   #define
  ```

  

- 文件包含

  ```cpp
  #include
  ```

  

- 条件编译 

  ```cpp
  #if 
  #elif 
  #ifndef 
  #ifdef
  #endif
  #undef
  ```

- 错误信息指令

  ```cpp
  #error
  ```

- 布局控制

  ```cpp
  #pragma
  ```

## 指令介绍

### 宏定义     ：作用是替换，又称作宏代换，宏替换

宏定义不分配内存，变量定义分配内存，宏展开不占运行时间只占编译时间；而函数运行占用

```cpp
// 宏定义'#'
#include <iostream>
using namespace std;
#define fun(n) "abc"#n

int main() {

    cout<<fun(100);
    return 0;
}
// 输出是 abc100   如果#n去掉n会报错
```

```cpp
//宏定义 '##'  将参数连接在一起
#include <iostream>
using namespace std;
#define  fun1(a,b,c)  a##b##c
int main() {
    cout<<fun1(1,2,3)<< endl;
    return 0;
}
//输出 123
```

### 文件包含

包含所需要的头文件

### 条件编译



##  

