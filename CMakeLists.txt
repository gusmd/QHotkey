cmake_minimum_required(VERSION 3.2)

project(QHotkey)

set(QHOTKEY_INCLUDE
    QHotkey/qhotkey.h
    QHotkey/qhotkey_p.h
)

set(QHOTKEY_SRC
    QHotkey/qhotkey.cpp
)

if(UNIX)
    list(APPEND QHOTKEY_SRC QHotkey/qhotkey_x11.cpp)
elseif(WIN32)
    list(APPEND QHOTKEY_SRC QHotkey/qhotkey_win.cpp)
elseif(APPLE)
    list(APPEND QHOTKEY_SRC QHotkey/qhotkey_mac.cpp)
endif()

add_library(QHotkey STATIC ${QHOTKEY_INCLUDE} ${QHOTKEY_SRC})

set_target_properties(QHotkey
    PROPERTIES
    CXX_STANDARD 11
    CXX_EXTENSIONS OFF
    AUTOMOC ON
    AUTORCC ON
)

target_include_directories(QHotkey PUBLIC QHotkey)

find_package(Qt5 COMPONENTS Widgets REQUIRED)
target_link_libraries(QHotkey PUBLIC Qt5::Widgets)