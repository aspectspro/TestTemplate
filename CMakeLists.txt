cmake_minimum_required(VERSION 3.5)

SET(NAME "Test")
SET(LIBRARY_NAME_TEST "AbstractObjects")

project(${NAME} LANGUAGES CXX)

include_directories("../../src")

set(Qt5_DIR "C:\\Felgo\\5.13.2\\msvc2017_64\\lib\\cmake\\Qt5")
set(Qt5Test_DIR "C:\\Felgo\\5.13.2\\msvc2017_64\\lib\\cmake\\Qt5Test")
set(Qt5Gui_DIR "C:\\Felgo\\5.13.2\\msvc2017_64\\lib\\cmake\\Qt5Gui")

SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_BINARY_DIR})
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_BINARY_DIR})

SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY})
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY})

find_package(Qt5Test REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5 COMPONENTS Core REQUIRED Sql Concurrent)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
enable_testing()

find_package(Qt5 COMPONENTS Core REQUIRED Sql Concurrent)

if(EXISTS ${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)

    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    conan_basic_setup()

    link_directories(${CMAKE_BINARY_DIR}/src)

    add_executable(${PROJECT_NAME} tst_test.cpp)
    add_test(NAME ${PROJECT_NAME} COMMAND ${PROJECT_NAME})

    target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Gui Qt5::Test Qt5::Core Qt5::Sql Qt5::Concurrent ${LIBRARY_NAME_TEST})

else()
    message(WARNING "The file conanbuildinfo.cmake doesn't exist, you have to run conan install first")
endif()
