cmake_minimum_required(VERSION 3.5)
project(issue126)

set(CMAKE_CXX_STANDARD 11)

find_package(ROOT REQUIRED)
include(${ROOT_USE_FILE})

ROOT_GENERATE_DICTIONARY(MainFrameDictionary MainFrame.hpp LINKDEF MainFrameLinkDef.h)

add_library(MainFrame SHARED MainFrameDictionary.cxx MainFrame.cpp)
target_link_libraries(MainFrame ${ROOT_LIBRARIES} Gui)

add_executable(issue126 main.cpp)
target_include_directories(issue126 SYSTEM BEFORE PUBLIC ./ PUBLIC ${ROOT_INCLUDE_DIRS})
target_link_libraries(issue126 MainFrame)
