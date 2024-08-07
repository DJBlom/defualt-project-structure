############################################################################
# Contents: System CMakeLists.txt file
# Author: Dawid Blom
# Date: September 15, 2023
#
# NOTE:
# This file is the CMakeLists.txt for the system sub branch file, containing
# the source and header files of the system sub branch. Additionally, this
# file should be usedto link with the feature sub branch's library at
# integration time.
############################################################################
cmake_minimum_required(VERSION 3.25)
project(target-system VERSION 0.0.1 LANGUAGES CXX C)


file(GLOB RESULT ${PROJECT_SOURCE_DIR}/source)
list(LENGTH RESULT FILES_IN_DIR)
if(${FILES_IN_DIR} GREATER 0)
    add_library(system 
        OBJECT
        ${PROJECT_SOURCE_DIR}/source/Control.cpp
        ${PROJECT_SOURCE_DIR}/source/Services.cpp
    )

    target_include_directories(system 
        PRIVATE
        ${PROJECT_SOURCE_DIR}/include/
        ${CMAKE_SOURCE_DIR}/api/include/
        ${CMAKE_SOURCE_DIR}/features/include/
        ${CMAKE_SOURCE_DIR}/algorithms/include
        PUBLIC
        ${CMAKE_SOURCE_DIR}/app/include
    )

    target_link_libraries(system 
        PRIVATE
        api
    )
else ()
    message(STATUS "There are no files in, system/source.")
endif()
