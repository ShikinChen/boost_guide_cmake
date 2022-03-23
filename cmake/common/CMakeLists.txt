cmake_minimum_required(VERSION 3.19)
project(common)

set(CMAKE_CXX_STANDARD 11)

get_filename_component(DIR_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)

set(SRC_PATH ${PROJECT_PATH}/${DIR_NAME})

file(GLOB CPP_FILE_PATH
        ${SRC_PATH}/*.hpp
        )
#如果只含有头文件或者hpp是使用INTERFACE
add_library(
        common
        INTERFACE
        ${CPP_FILE_PATH})

target_include_directories(common
        INTERFACE
        ${SRC_PATH}
        )

file(GLOB SUB_DIR_LIST ${SRC_PATH}/*.cpp)

foreach (file_item ${SUB_DIR_LIST})
    get_filename_component(file ${file_item} NAME)
    set(FILE_PATH ${SRC_PATH}/${file})
    if (NOT IS_DIRECTORY ${file})
        get_filename_component(ProjectId ${file} NAME)
        string(REPLACE ".cpp" "_test" ProjectId ${ProjectId})
        add_executable(${ProjectId} ${FILE_PATH})
        target_link_libraries(${ProjectId} ${CONAN_LIBS} common)
    endif ()
endforeach ()
