cmake_minimum_required(VERSION 3.16) #必须指明此文件所需要的CMake最低版本
project(test VERSION 1.0.0) 



# commit id则可以通过git命令获取
# 然后通过configure_file 把configure.h.in中相应的宏替换掉，变成configure.h就可以了。
# 版本号 ${CMAKE_PROJECT_VERSION} ${CMAKE_PROJECT_VERSION_MAJOR} ... 
# 获取编译时间戳
set(test_version ${CMAKE_PROJECT_VERSION})

EXECUTE_PROCESS(
	COMMAND git rev-parse --short HEAD
	OUTPUT_VARIABLE TEST_COMMIT_ID
	OUTPUT_STRIP_TRAILING_WHITESPACE
) # 获取版本号，保存到TEST_COMMIT_ID 

STRING(TIMESTAMP TEST_BUILD_TIME)

configure_file(configure.h.in configure.h)


# 根据平台 设置前缀 后缀




# 设置编译器和编译选项 



# import toolchain.cmake


# test


# install

# pack


