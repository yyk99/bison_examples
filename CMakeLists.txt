#
#
#

project (bison_examples)
cmake_minimum_required(VERSION 3.18)

find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

message(STATUS "BISON_VERSION=${BISON_VERSION}")
message(STATUS "FLEX_VERSION=${FLEX_VERSION}")

