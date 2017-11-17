muduo on mac
===================

取mac分支

git clone -b mac https://github.com/chenshuo/muduo


valgrind on mac
---------------------


boost on mac
---------------------

* 如果boost库没有安装在系统的默认路径下则需要调整muduo/CMakeLists.txt

<pre>
SET(CMAKE_INCLUDE_PATH ${CMAKE_INCLUDE_PATH} ${BOOST_ROOT})
SET(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} ${BOOST_ROOT}/lib)
LINK_DIRECTORIES(${BOOST_ROOT}/lib)
</pre>


protobuf on mac
---------------------
* Build m4, autoconf, automake, libtool on Mac OS X Lion

  https://gist.github.com/henry0312/1397146
  
* 执行autogen.sh 生成configure配置
* 执行make &  make check & sudo make install
