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




