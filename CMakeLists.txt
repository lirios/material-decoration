cmake_minimum_required(VERSION 3.10.0)

project("MaterialDecoration"
    VERSION "1.1.0"
    DESCRIPTION "Material Design decoration for Wayland clients"
    LANGUAGES CXX C
)

## Shared macros and functions:
if(NOT LIRI_LOCAL_ECM)
    find_package(LiriCMakeShared "1.0.0" REQUIRED NO_MODULE)
    list(APPEND CMAKE_MODULE_PATH "${LCS_MODULE_PATH}")
endif()

## Set minimum versions required:
set(QT_MIN_VERSION "5.8.0")

## Add some paths to check for CMake modules:
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake;${CMAKE_CURRENT_SOURCE_DIR}/cmake/3rdparty/extra-cmake-modules")

## Liri specific setup common for all modules:
include(LiriSetup)

## Find Qt 5:
find_package(Qt5 "${QT_MIN_VERSION}"
    CONFIG REQUIRED
    COMPONENTS
        Core
        Gui
        WaylandClient
)
if(${Qt5_VERSION} VERSION_GREATER "5.15.1")
    find_package(Qt5 "${QT_MIN_VERSION}"
        CONFIG REQUIRED
        COMPONENTS XkbCommonSupport)
endif()

## Add subdirectories:
add_subdirectory(src/plugins/decorations/material)
