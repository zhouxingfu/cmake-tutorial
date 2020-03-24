## __<PROFESSIONAL CMAKE - A PRACTICAL GUIDE> 读书笔记__


# __Part I : 基础__

* 在使用一个工具之前不了解它的基本概念，如何使用，最终会导致挫折
* 学习理论而不动手实践，这个过程首先就非常让人厌烦，而最终也会导致对知识的理解流于表面


## __1. 介绍__

开发者不得不接触的——　如何把代码变成可执行，编译，链接，测试框架，打包系统以及更多。

configure -> generate -> build -> test -> package



## __2. 建立一个项目__

In-source Builds 

Out-source Builds

__练习建议__

debug/release windows/mac/linux/android 为不同的平台和target创建不同的组合方式，看看都有什么区别。


## __3. 一个最小项目__


```
    cmake_minimum_required(VERSION 3.2)
    project(MyApp)
    add_executable(myExe main.cpp)
```


## __4. 建立简单目标__


## __5. 变量__



## __6. 流控制__



## __7. 使用子目录__



## __8. 函数和宏__


## __9. 属性__


## __10. Generator Expressions表达式生成器__


## __11. 模块__


## __12. Policies政策__


__Part II : Builds In Depth__

## __13. Build Type__


## __14. Compiler And Linker Essentials__


## __15. Language Requirements__


## __16. Target Types__


## __17. Custom Tasks__

## __18. Working With Files__

## __19. Specifying Version Details__


## __20. Libraries__


## __21. Toolchains And Cross Compiling__


## __22. Apple Features__


# __Part III : The Bigger Picture__


## __23. Finding Things__


## __24. Testing__

## __25. Installing__


## __26. Packaging__


## __27. External Content__


## __28. Project Organization__

