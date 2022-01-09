#
#
#

project (bison_examples)
cmake_minimum_required(VERSION 3.18)

#set(CMAKE_CXX_STANDARD 14)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)
#set(CMAKE_CXX_EXTENSIONS ON)

find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

message(STATUS "BISON_VERSION=${BISON_VERSION}")
message(STATUS "FLEX_VERSION=${FLEX_VERSION}")

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

add_subdirectory(examples)

# 