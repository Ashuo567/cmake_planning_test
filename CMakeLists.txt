# cmake_minimum_required(VERSION 3.30.0)
# project(planning)
# set(CMAKE_CXX_STANDARD 17)

# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# aux_source_directory(. SRC_LISTS)
# add_executable(planning_main ${SRC_LISTS})


cmake_minimum_required(VERSION 3.30.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

## 变量和目录设置
# 动态库和exe都指定到bin目录下
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
# # Linux指定方式
# CMAKE_LIBRARY_OUTPUT_DIRECTORY # 动态库和可执行文件
# CMAKE_ARCHIVE_OUTPUT_DIRECTORY # 静态库

## 动态库
# 打包生成动态库common
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
add_library(common      
SHARED
${SRC_LISTS}
)

# 动态库common包含头文件目录
target_include_directories(common   
PUBLIC
${PROJECT_SOURCE_DIR}/include
)


## 可执行文件
# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)    # 将exe指定到bin目录下
add_executable(planning_main planning_main.cpp)    # 生成可执行文件

# main包含头文件目录
target_include_directories(planning_main  
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

# 动态库common链接到main
target_link_libraries(planning_main  
PUBLIC
common
)
