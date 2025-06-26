
cmake_minimum_required(VERSION 3.23)
#项目名称
project(opengl_study_framework)
#C++标准
set(CMAKE_CXX_STANDARD 20)
#可执行文件输出路径
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")
# find the required packages
find_package(GLM REQUIRED)
message(STATUS "GLM included at ${GLM_INCLUDE_DIR}")
find_package(GLFW3 REQUIRED)
message(STATUS "Found GLFW3 in ${GLFW3_INCLUDE_DIR}")
find_package(ASSIMP REQUIRED)
message(STATUS "Found ASSIMP in ${ASSIMP_INCLUDE_DIR}")


if(WIN32)
  set(LIBS glfw3 opengl32 assimp freetype irrKlang)
  add_definitions(-D_CRT_SECURE_NO_WARNINGS)
elseif(APPLE)
  INCLUDE_DIRECTORIES(/System/Library/Frameworks)
  FIND_LIBRARY(COCOA_LIBRARY Cocoa)
  FIND_LIBRARY(OpenGL_LIBRARY OpenGL)
  FIND_LIBRARY(IOKit_LIBRARY IOKit)
  FIND_LIBRARY(CoreVideo_LIBRARY CoreVideo)
  MARK_AS_ADVANCED(COCOA_LIBRARY OpenGL_LIBRARY)
  SET(APPLE_LIBS ${COCOA_LIBRARY} ${IOKit_LIBRARY} ${OpenGL_LIBRARY} ${CoreVideo_LIBRARY})
  SET(APPLE_LIBS ${APPLE_LIBS} ${GLFW3_LIBRARY} ${ASSIMP_LIBRARY} ${FREETYPE_LIBRARIES})
  set(LIBS ${LIBS} ${APPLE_LIBS})
endif(WIN32)

#头文件路径
include_directories(${PROJECT_SOURCE_DIR}/include)
#可执行文件
add_executable(opengl_study_framework src/glad/glad.c Opengl_study_framework.cpp)
#库文件路径
link_directories(${PROJECT_SOURCE_DIR}/lib)
#目标链接文件
#target_link_libraries(opengl_study_framework ${PROJECT_SOURCE_DIR}/lib/glfw3.lib)
target_link_libraries(opengl_study_framework ${LIBS})