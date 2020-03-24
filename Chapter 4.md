Chapter 4 构建简单目标

除了console，还可以构建 app windows-gui等
除了可执行，还可以构建 静态库 动态库 module framework等



4.1 可执行

add_executable(targetName [WIN32] [MACOSX_BUNDLE]
    [EXCLUE_FROM_ALL]
    source1 source2 ...)


WIN32和 MACOSX_BUNDLE就不具体介绍了

EXCLUDE_FROM_ALL 看chapter 16 target types


4.2 定义库

add_library(targetName [STATIC | SHARED | MODULE] 
    [EXCLUDE_FROM_ALL]
    source1 source2 ...)

MODULE跟动态库类似，但在程序运行期间决定是否要链接，说实话，这里不太理解


我们可以在cmakelists.txt中指定static shared，但更好的方式是项目可以被编译成静态库，也可以被编译动态库，通过BUILD_SHARED_LIBS 来指定，如果为true, 就shared，false，就static

我们通过chapter5 中的变量来设定，也可以在命令行中指定

cmake -DBUILD_SHARED_LIBS=YES /path/to/source

set(BUILD_SHARED_LIBS YES)

4.3 链接目标

一个项目依赖另一个项目，可以具体分为几种情形

PRIVATE : A在代码内部依赖B，但依赖A的那些并不需要知道这件事，因为这是内部依赖


PUBLIC ： A在代码内部依赖B，同时A对外提供的接口中用到了B的数据类型，这时候依赖A的项目，必须显式地指明对B的依赖


INTERFACE ： A不再代码内部依赖B，只是接口上用到了B


target_link_libraries(targetname private|public|interface item1 item2 
    private|public|interface item3 item4...)


add_library(collector src1.cpp)
add_librarty(algo src2.cpp)
add_library(engine src3.cpp)
add_library(ui src4.cpp)

add_executable(myapp main.cpp)

target_link_libraries(collector PUBLIC ui PRIVATE algo engine)

target_link_libraries(myApp PRIVATE collector)


在上面的例子中，ui是以public形式连接到collector库，所以即使myApp仅仅直接链接到collector，此时myApp也必须链接到ui。另一方面，algo engine是以private链接到collector库，所以myApp不会直接链接到 这两个库。在16.2节会讨论静态库的依赖行为，包括循环依赖。

接下来的章节展示了一些其它的target_..._command()命令，用来加强目标间的依赖关系。

4.4 linking non-targets

在上面的部分，所有的条目都是链接到已经存在的cmake目标，但是target_link_libraries()命令比上面说的更加灵活。除了cmake targets，下面这些都可以在target_link_libraries()中被设置。

* 库文件的全路径 full path to a library file
* plain library name
* link flag


上面这三种情形，都没有看懂，不明白说的是什么场景。 chapter 13 build type

4.5 旧风格CMake





4.6 练习建议

* 直接设置工程名，而不是用变量表示，为目标target选择它的名字的时候依照它的用途，而不是用工程名，因为一个工程中可能有多个target，就算没有多个target，这样也是不合适的

* 为库命名的时候，坚决不要在名字前后加上lib，因为cmake默认会添加

* 除非有强烈的理由这么做，否则绝对不要显式指明STATIC SHARED，这会让设置更加灵活。

* 显式指明PRIVATE PUBLIC INTERFACE关键字，而不是遵循旧版本CMAKE，默认都是PUBLIC 依赖。随着一个工程复杂度的提升，这三个关键字对目标间的依赖如何处理 有非常大的影响。从项目的一开始就使用这三个关键字，也迫使开发者思考目标间的依赖关系，更早发现项目的结构问题。

