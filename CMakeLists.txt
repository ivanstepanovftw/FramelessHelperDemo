cmake_minimum_required(VERSION 3.22)
project(framelesshelperdemo)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Packages
find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Widgets)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Widgets)

set(FRAMELESSHELPER_BUILD_STATIC   OFF CACHE BOOL "")
set(FRAMELESSHELPER_BUILD_WIDGETS  ON CACHE BOOL "")
set(FRAMELESSHELPER_BUILD_QUICK    OFF CACHE BOOL "")
set(FRAMELESSHELPER_BUILD_EXAMPLES ON CACHE BOOL "")
add_subdirectory(framelesshelper)

# Executable
set(PROJECT_SOURCES
        src/main.cpp
        src/mainwindow.cpp
        src/mainwindow.h
        src/mainwindow.ui
        )
if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(${PROJECT_NAME}
            MANUAL_FINALIZATION
            ${PROJECT_SOURCES}
            )
else()
    add_executable(${PROJECT_NAME}
            ${PROJECT_SOURCES}
            )
endif()

target_include_directories(${PROJECT_NAME} PRIVATE
        src
        )
target_link_libraries(${PROJECT_NAME} PRIVATE
        Qt${QT_VERSION_MAJOR}::Core
        Qt${QT_VERSION_MAJOR}::Widgets
        FramelessHelperCore FramelessHelperWidgets
        )
