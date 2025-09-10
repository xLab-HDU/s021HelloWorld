# 指定cmake最低版本要求
cmake_minimum_required(VERSION 3.28)
# 设置项目名称和使用的编程语言
project(CMakeProject LANGUAGES CXX)

# 设置可执行文件的输出目录，使得main可执行目标生成在build/bin目录下
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# 选项：是否构建共享库，动态库设为ON，静态库设为OFF
option(BUILD_SHARED_LIBS "Build libraries as shared" OFF)

#  定义一个名为main的可执行目标，源文件为src/main.cpp
add_executable(main src/main.cpp)
# 设置C++标准为C++17
target_compile_features(main PRIVATE cxx_std_17)

# 在Windows系统中（使用 MinGW-w64）构建时
# 静态链接需要将libstdc++、libgcc编译进可执行文件中，避免运行时依赖外部 DLL
if(WIN32 AND (CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR (CMAKE_CXX_COMPILER_ID STREQUAL "Clang")))
  target_link_libraries(main PRIVATE
      -static-libgcc
      -static-libstdc++
    )  
endif()

enable_testing()
add_test(NAME SmokeTest
         COMMAND main
         WORKING_DIRECTORY ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})

install(TARGETS main RUNTIME DESTINATION .)
install(DIRECTORY "data/"
        DESTINATION "data"
        FILES_MATCHING PATTERN "*"
)

set(CPACK_PACKAGE_NAME "HelloWorld")
set(CPACK_PACKAGE_VERSION "1.0.0")
set(CPACK_PACKAGE_VENDOR "HDU")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Hello-World")
set(CPACK_PACKAGE_CONTACT "contact@example.com")
include(CPack)