
1. 取消`max`与`min`的预定义：
```cpp
#ifdef max

#pragma message("#undefing marco max")

#undef max

#endif // max
```
解释：
- `#undef` 可以移除宏定义

2. 禁止`vector<bool>`的使用：
```cpp
static_assert(!std::is_same<bool, T>::value, "vector<bool> is abandoned in mystl");
```
- static_assert在编译时测试软件断言
	- 其函数原型为`static_assert( constant-expression, string-literal );`
	- 如果指定的常量表达式为 **`false`**，则编译器显示指定的消息（如果提供了消息），并且编译失败，错误为 C2338；否则，声明无效。
- is_same测试两个类型是否相同
	- 其函数原型为`template <class Ty1, class Ty2> struct is_same;`
	- 用法为：如果std::is_same<class1, class2>::value为true，说明它们类型相同，否则类型不同

3. 迭代器`Iter`的类型检查：
```cpp
template <class Iter, typename std::enable_if<
mystl::is_input_iterator<Iter>::value, int>::type = 0>
vector(Iter first, Iter last) {}
```
如果Iter是input_iterator，则该模板函数可以被识别，否则失败。
- [C++11新特性--std::enable_if和SFINAE - 简书 (jianshu.com)](https://www.jianshu.com/p/a961c35910d2)
- [知无涯之C++ typename的起源与用法 (feihu.me)](https://feihu.me/blog/2014/the-origin-and-usage-of-typename/)
**问题：type=0是弃用的意思吗？**

4. `noexcept`关键字的使用：
- 该关键字告诉编译器，函数中不会发生异常， **是个优化手段**，让编译器知道 `foo` 里绝不会抛异常，不必多生成保护栈上对象安全析构的代码。
- 如果在运行时，noexecpt函数向外抛出了异常（如果函数内部捕捉了异常并完成处理，这种情况不算抛出异常），程序会直接终止
- [(29 封私信 / 99+ 条消息) C++标准中为什么要设计出noexcept，而不是默认是非异常？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/496351156)

5. 类省略模板参数：
```cpp
vector(const vector& rhs)
```
**问题：是由于做函数形参，需要接受各种类型的T，所以自动推导，省略模板参数吗？**

6. 接收初始化列表参数
```cpp
vector(std::initializer_list<value_type> ilist)
```
使用`initializer_list`可以接收初始化列表参数

7. fill_assign的逻辑
- 如果n大于容量，申请更大的vector，并与原vector直接交换
- 如果n小于容量，大于size，分两次填充
- 如果n小于size，直接填充，并删除多余的元素
