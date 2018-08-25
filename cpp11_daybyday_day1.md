C++11
====================
reference
--------------------

[C++ Language Reference](https://msdn.microsoft.com/en-us/library/3bstk3k5.aspx)


move-semantic-perfect-forward
--------------------

+ 概念
  * move-semantic
  * lvalue & rvalue
  * lvalue reference & rvalue reference 
  * perfect forwarding
  * universal reference

+ 作用及用法
  * 左值引用和右值引用可以被分别重载，这样确保左值和右值分别调用到拷贝和移动的两种语义实现。对于左值，如果我们明确放弃对其资源的所有权，则可以通过std::move()来将其转为右值引用。std::move()实际上是static_cast<T&&>()的简单封装。

cv-qualified

+ concurrency
 * https://baptiste-wicht.com/posts/2012/03/cpp11-concurrency-part1-start-threads.html


+ 参考资料

 * [move-semantic-perfect-forward](https://codinfox.github.io/dev/2014/06/03/move-semantic-perfect-forward/)

 * [C++ and Beyond 2012](https://channel9.msdn.com/Tags/cppbeyond+2012)



alignas and alignof
---------------------------
```
The alignas type specifier is a portable, C++ standard way to specify custom alignment of variables and user defined types. The alignof operator is likewise a standard, portable way to obtain the alignment of a specified type or variable.
```
https://msdn.microsoft.com/en-us/library/dn956970.aspx
