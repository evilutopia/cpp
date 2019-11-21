C++11
====================
reference
--------------------

[C++ Language Reference](https://msdn.microsoft.com/en-us/library/3bstk3k5.aspx)


move-semantic-perfect-forward
--------------------

+ 概念
  * move-semantic(std::move)
  * lvalue & rvalue
  * lvalue reference & rvalue reference 
  * perfect forwarding(std::forward)
  * universal reference

+ 作用及用法
  * 左值引用和右值引用可以被分别重载，这样确保左值和右值分别调用到拷贝和移动的两种语义实现。对于左值，如果我们明确放弃对其资源的所有权，则可以通过std::move()来将其转为右值引用。std::move()实际上是static_cast<T&&>()的简单封装。
  
+ 解决问题

  * shallow copy 和 deep copy（如 copy 构造函数 ），如何减少临时对象拷贝时不必要的内存创建、拷贝与销毁。
  
+ 左值、右值
  
  * 如何区分左值右值
    
    https://eli.thegreenplace.net/2011/12/15/understanding-lvalues-and-rvalues-in-c-and-c/ 
     
  * 左值右值样例

cv-qualified

+ concurrency
 * https://baptiste-wicht.com/posts/2012/03/cpp11-concurrency-part1-start-threads.html


+ 参考资料

 * [move-semantic-perfect-forward](https://codinfox.github.io/dev/2014/06/03/move-semantic-perfect-forward/)

 * [C++ and Beyond 2012](https://channel9.msdn.com/Tags/cppbeyond+2012)
 
 
 * 看了几篇文章后终于搞明白了 引用折叠
 
 https://www.zhihu.com/question/34544004
 
 https://stackoverflow.com/questions/8526598/how-does-stdforward-work
 
 https://zh.wikipedia.org/wiki/%E5%8F%B3%E5%80%BC%E5%BC%95%E7%94%A8#%E5%BC%95%E7%94%A8%E6%8A%98%E5%8F%A0%E8%A7%84%E5%88%99
 
 <pre>
T& &变为T&
T& &&变为T&
T&& &变为T&
T&& &&变为T&&
 </pre>
 
  <pre>
#include <iostream>
#include <cstdlib>
#include <cstring>

#include <map>
#include <set>
#include <string>
#include <tuple>

using namespace std;
static int id_seed = 0;

class Test {
public:
    int * arr{nullptr};
    int id;
public:
    Test():arr(new int[5000]{1,2,3,4}) {
        id  = id_seed++;
    	cout << id << " default constructor" << endl;
    }
    Test(const Test & t) {
        id  = id_seed++;
        cout << id << " copy constructor" << endl;
        if (arr == nullptr) arr = new int[5000];
        memcpy(arr, t.arr, 5000*sizeof(int));
    }
    Test(Test && t): arr(t.arr) {
        id  = id_seed++;
        cout << id << " move constructor" << endl;
        t.arr = nullptr;
    }
    Test& operator=(Test& rhs)
    {
        this->id = rhs.id;
        cout << id << " operator=&" << endl;
        return *this;
    }
    Test& operator=(Test&& rhs)
    {  
        this->id = rhs.id;
        rhs.id = -1;
        cout << id << " operator=&&" << endl;
        return *this;
    }
    ~Test(){
        cout << "destructor" << endl;
        delete [] arr;
    }
};


template<class T>
void foo(T arg) 
{
    cout << sizeof(arg) << endl;
}

template<class T>
void wrapper(T&& arg) 
{
    // arg 始终是左值
    foo(std::forward<T>(arg)); // 转发为左值或右值，依赖于 T
}

template<class T>
void wrapper1(T&& arg) 
{
    Test t;
    t = std::forward<T>(arg); // 转发为左值或右值，依赖于 T
}

template<class T>
void wrapper2() 
{
    Test t;
    Test t1;
    t = std::forward<T>(t1); // 转发为左值或右值，依赖于 T
}

Test g_test;

template<class T>
void Produce(T&& arg) // universe ref
{
    DoProduce(std::forward<T>(arg));
}

template<class T>
void DoProduce(T arg) // ref
{
    g_test = arg;
    cout << arg.id << "V" << g_test.id << endl;
}







int main()
{
        
    cout << "lv------------------" << endl;
    {
    Test t;
    wrapper(t);
    }
    cout << "rv------------------" << endl;
    wrapper(Test());
    cout << "operator=&------------------" << endl;
    {
        Test t;
        Test tt = t;
    }
    cout << "operator=&& forward obj------------------" << endl;
    {
        Test t;
        Test tt = std::forward<Test>(t);
    }
    cout << "operator=&& forward lref------------------" << endl;
    {
        Test t;
        Test& tr = t;
        Test tt = std::forward<decltype(tr)>(tr);
    }
    cout << "operator=&& forward rref------------------" << endl;
    {
        Test&& tr = Test();
        Test tt = std::forward<decltype(tr)>(tr);
    }
    cout << "operator=&& move------------------" << endl;
    {
        Test t;
        Test tt = std::move(t);
    }
    
    
    cout << "= ------------------" << endl;
    {
    Test t;
    wrapper1(t);
    }
    
    {
    wrapper2<Test>();
    }
    
    cout << "produce rvalue------------------" << endl;
    {
    Produce(Test());
    }
    cout << "produce lvalue------------------" << endl;
    {
        Test t;
        cout <<"test:" <<t.id << endl;
        Produce(t);
        cout <<"test:" <<t.id << endl;
    }

}
 </pre>



alignas and alignof
---------------------------
```
The alignas type specifier is a portable, C++ standard way to specify custom alignment of variables and user defined types. The alignof operator is likewise a standard, portable way to obtain the alignment of a specified type or variable.
```
https://msdn.microsoft.com/en-us/library/dn956970.aspx

C++ online
----------------------------

https://wandbox.org/
