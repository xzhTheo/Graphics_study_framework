# cmakelist.txt: opengl_study_framework 的 cmake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
#cmake_minimum_required (version 3.8)

# 如果支持，请为 msvc 编译器启用热重载。
#if (policy cmp0141)
#  cmake_policy(set cmp0141 new)
#  set(cmake_msvc_debug_information_format "$<if:$<and:$<c_compiler_id:msvc>,$<cxx_compiler_id:msvc>>,$<$<config:debug,relwithdebinfo>:editandcontinue>,$<$<config:debug,relwithdebinfo>:programdatabase>>")
#endif()

#project ("opengl_study_framework")

# 将源代码添加到此项目的可执行文件。
#add_executable (opengl_study_framework "opengl_study_framework.cpp" "opengl_study_framework.h" "include/glad/glad.h" "include/khr/khrplatform.h" "src/glad.c" "include/glfw/glfw3.h" "include/glfw/glfw3native.h")

#if (cmake_version version_greater 3.12)
#  set_property(target opengl_study_framework property cxx_standard 20)
#endif()

# todo: 如有需要，请添加测试并安装目标。


cmake_minimum_required(VERSION 3.23)
#项目名称
project(opengl_study_framework)
#C++标准
set(CMAKE_CXX_STANDARD 20)
#可执行文件输出路径
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#头文件路径
include_directories(${PROJECT_SOURCE_DIR}/include)
#可执行文件
add_executable(opengl_study_framework src/glad/glad.c Opengl_study_framework.cpp)
#库文件路径
link_directories(${PROJECT_SOURCE_DIR}/lib)
#目标链接文件
target_link_libraries(opengl_study_framework ${PROJECT_SOURCE_DIR}/lib/glfw3.lib)