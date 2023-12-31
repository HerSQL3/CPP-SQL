cmake_minimum_required(VERSION 3.12)

# 设置cmake编译器版本，这两条命令要放在最上面命令的下面，其他命令的前面，否则无法生效
set (CMAKE_C_COMPILER "/usr/bin/gcc-13")
set (CMAKE_CXX_COMPILER "/usr/bin/g++-13")

project(MyProject)

# 添加内存消毒器，为了规范我们的代码
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer")

# 设置CMake_Build_Type
set(CMAKE_BUILD_TYPE Debug)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 20)

# 添加可执行文件
add_executable(client
    src/client_menu.cpp
    src/server_order.cpp
    src/tools.cpp
    test/client.cpp
)

add_executable(server
    src/client_menu.cpp
    src/server_order.cpp
    src/tools.cpp
    test/server.cpp
)

# 指定头文件的搜索路径，要放在前面两个的后面，因为是根据可执行文件指定的
target_include_directories(client PRIVATE ${CMAKE_SOURCE_DIR}/include)
target_include_directories(server PRIVATE ${CMAKE_SOURCE_DIR}/include)
