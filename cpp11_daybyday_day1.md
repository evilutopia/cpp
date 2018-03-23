move-semantic-perfect-forward
====================

概念
--------------------

* move-semantic
* lvalue & rvalue
* lvalue reference & rvalue reference 
* perfect forwarding
* universal reference

作用及用法
--------------------
左值引用和右值引用可以被分别重载，这样确保左值和右值分别调用到拷贝和移动的两种语义实现。对于左值，如果我们明确放弃对其资源的所有权，则可以通过std::move()来将其转为右值引用。std::move()实际上是static_cast<T&&>()的简单封装。

作者：Tinro
链接：https://www.zhihu.com/question/22111546/answer/30801982
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


参考资料
--------------------

> [move-semantic-perfect-forward](https://codinfox.github.io/dev/2014/06/03/move-semantic-perfect-forward/)

> [C++ and Beyond 2012](https://channel9.msdn.com/Tags/cppbeyond+2012)
