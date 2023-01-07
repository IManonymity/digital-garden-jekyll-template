---
---

1. operator  new函数
```cpp
return static_cast<T*>(::operator new(sizeof(T)));
```
- new operator/delete operator就是new和delete操作符
	- 调用operator new申请空间
	- 调用构造函数实例化
	- 返回指针
- 而operator new/operator delete是函数。

[C++ 内存分配(new，operator new)详解_wudaijun的博客-CSDN博客](https://blog.csdn.net/WUDAIJUN/article/details/9273339)

2. placement new
```cpp
::new ((void*)ptr) Ty1(value);
```
- placement new也叫定位new表达式，它用于在给定的内存中初始化对象（但不分配内存）
	- 假定buffer已经分配好内存块，使用`buffer = new(buffer) string(“abd”);`可以初始化对象
	- new表达式(new operator)其实可以分解为两部，即先调用new操作符(operator new)申请内存，再调用placement new来初始化对象。

[C++当中3种new的用法 | Fantacity (yosef-gao.github.io)](https://yosef-gao.github.io/2016/10/01/cpp-new/)

3. move的实现
```cpp
template <class T>
typename std::remove_reference<T>::type&& move(T&& arg) noexcept
```
- T&&：通过引用折叠，可以捕获左值也可以捕获右值
- remove_reference：去掉所有引用，只记录原类型
- static_cast：通过static_cast将左值转换为右值
[c++ 之 std::move 原理实现与用法总结_ppipp1109的博客-CSDN博客_c++ std::move](https://blog.csdn.net/p942005405/article/details/84644069)

4. forward完美转发与可变模板参数
```cpp
mystl::construct(ptr, mystl::forward<Args>(args)...);
```
- 模板参数：用`class...`或`typename...`指出接下来的参数表示零个或多个类型的列表，如`typename... Args`，使用`sizeof...(Args)`可以查看该列表的长度
- 函数参数：类型名后面跟一个省略号表示零个或多个给定类型的`非类型参数`的列表，如`Args&... rest`，使用`sizeof...(rest)`可以查看该列表的长度
- 解包：`processValues(rest...)`
- 完美转发：右值引用传递给processValues()函数时，它就传递为右值引用，但是如果把左值引用传递给processValues()函数时，它就传递为左值引用，`processValues(std::forward<Ts>(args) ...)
[可变参数函数模板&move&forward - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/408219169)


