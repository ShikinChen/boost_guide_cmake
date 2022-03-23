cmake_minimum_required(VERSION 3.19)
project(boost_guide)

set(CMAKE_CXX_STANDARD 11)

get_filename_component(DIR_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)

set(SRC_PATH ${PROJECT_PATH}/${DIR_NAME})

file(GLOB SUB_DIR_LIST ${SRC_PATH}/*.cpp)

foreach (file_item ${SUB_DIR_LIST})
    get_filename_component(file ${file_item} NAME)
    set(FILE_PATH ${SRC_PATH}/${file})
    if (NOT IS_DIRECTORY ${file})
        get_filename_component(ProjectId ${file} NAME)
        string(REPLACE ".cpp" "_dome" ProjectId ${ProjectId})
        add_executable(${ProjectId} ${FILE_PATH})
        target_link_libraries(${ProjectId} ${CONAN_LIBS} common)
    endif ()
endforeach ()
