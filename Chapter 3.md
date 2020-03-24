Chatper 3 最小项目


cmake_minimum_required(VERSION 3.2)
project(myApp)

add_executable(myExe main.cpp)

or

add_executable(myExe 
    main.cpp
    src1.cpp
    src2.cpp)


cmakelists.txt中对大小写不敏感

如果是新项目的话，建议cmake版本不要低于3.2
如果是老项目的话，2.8.12兼容性更好一些

如果一个平台上的cmake版本太低，这时候最好尽可能升级cmake，而不是修改项目的cmakelists.txt，来适应更低版本的cmake

另一方面，如果一个项目是其它项目的依赖项，那么这时候用一个更低版本的cmake是一个更好的选择，否则很可能会产生适配问题。

独立项目尽可能用新的cmake，对于老项目就不能这么要求了。


使用cmake老版本的最大问题会报一堆warning


3.2 project() 命令


project(projectName [VERSION ] [LANGUAGES languageName])

项目名称 只能包含  字母  数字 下划线 横杠，通常情况下大家只用字母和数字

因为不允许空格，所以项目名称不用被引号包起来

项目名称一般在cmakelists最顶端，打包和生成文档的时候也会用到它。


project中要想使用version，cmake版本必须在3.0及以上

在指定语言的时候，如果是混合语言开发，用空格分隔

project(myProj Languages C CXX)


cmake_minimum_required(VERSION 3.2)
project(myApp VERSION 4.1 LANGUAGES C CXX)

add_executable(myApp  main.cpp)


关于指定版本和语言的几点注意事项

1. VERSION LANGUAGE的指定可以在同一个语句中，也可以单独成句 ，但不能漏掉 VERSION LANGUAGE关键字

2. 指定语言的时候不能用小写，最起码在Windows平台是这样，会提示找不到CMAKE_c_COMPILER

project命令不仅仅是提供一些变量，更重要的是 确保你机器上的编译器能够正常编译和链接

如果不指定project，那么cmake会隐式调用它，并把语言默认为C CXX，并用这些默认配置来检查编译、链接功能是否正常。

更重要的是 我们在后面要学习如何设置编译选项，以及交叉编译工具链。

这些检查都会被保存在CMAKECACHE中，一般情况下我们不会关注这些，除非我们用了不常见的toolchain，或者交叉编译工具链。



3.3 构造一个基本的exe

add_executable(targetName source1 source2 ...)

生成的时候，Windows下是.exe，其它平台是无后缀名的形式

当然我们可以用属性来构造，同时我们可以在一个cmakelists中构造多个可执行文件，一行一个

3.4 注释

#


3.5 推荐的练习

1. 确保每个cmakelists都有一个cmake_ minimum_required
2. 在指定cmake最低版本时候，请参考上面的建议
3. 如果项目可以支持cmake 3.0，那么这时候考虑使用版本号来管理项目，最好在一开始就这么做


