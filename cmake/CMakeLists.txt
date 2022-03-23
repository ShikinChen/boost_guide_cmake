cmake_minimum_required(VERSION 3.19)
project(boost_guide)

set(CMAKE_CXX_STANDARD 11)

if (EXISTS ${CMAKE_SOURCE_DIR}/conanbuildinfo.cmake)
    include(${CMAKE_SOURCE_DIR}/conanbuildinfo.cmake) #如果使用 conan install . 命令 使用当前 conanbuildinfo.cmake
else ()
    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake) # 如果使用 clion的conan 插件
endif ()

set(CONAN_DISABLE_CHECK_COMPILER 1)

conan_basic_setup()

#set(PROJECT_PATH ${CMAKE_CURRENT_LIST_DIR}/..)

get_filename_component(PROJECT_PATH ../ ABSOLUTE)

file(GLOB SUB_DIR_LIST RELATIVE ${PROJECT_PATH} *)

set(COMMON_PATH ${CMAKE_CURRENT_LIST_DIR}/common)

add_subdirectory(${COMMON_PATH})

foreach (file ${SUB_DIR_LIST})
    set(DIR_PATH ${PROJECT_PATH}/${file})
    if ((IS_DIRECTORY ${DIR_PATH})
            AND (NOT ${file} MATCHES "cmake-build-*")
            AND (NOT ${file} MATCHES "common")
            AND (NOT ${file} MATCHES "CMakeLists.txt"))
        add_subdirectory(${PROJECT_PATH}/${file})
    endif ()
endforeach ()