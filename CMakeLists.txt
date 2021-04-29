project(myProject)

cmake_minimum_required(VERSION 2.8)

# possible cmake/findMyLib.cmake configs for find_package
# set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

# find your libraries
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)

# define source files:
# read source files dynamically, use ${source_files}
file (GLOB source_files "src/*.cpp")  
# remove ${source_files} and set cpp-filenames to set source files manually
add_executable(${PROJECT_NAME} ${source_files}) 

# "include" if source and include files in seperate folders, possibly ${<LIBNAME>_INCLUDE_DIR} for library include dirs
#include_directories("include")  

# link target libraries, possibly ${<LIBNAME>_INCLUDE_DIR} for <LIBNAME> if :: notation not valid
# (Linux: <LIBNAME> for -l<LIBNAME> with no find_package or pkg-config --libs --cflags)
target_link_libraries(${PROJECT_NAME} OpenGL::GL GLEW::GLEW)

# copy resource files into build folder:
# set resource filename, ${PROJECT_SOURCE_DIR} not mandatory, but recommended 
set(resource_files
  "${PROJECT_SOURCE_DIR}/res"
  "${PROJECT_SOURCE_DIR}/image.png"
)
# copy files
file(COPY ${resouce_files} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
