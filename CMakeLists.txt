cmake_minimum_required(VERSION 3.16)

project(minesweeper VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.2 COMPONENTS Quick REQUIRED)

qt_add_executable(appminesweeper
    src/main.cpp
    resources.qrc
)

qt_add_qml_module(appminesweeper
    URI minesweeper
    VERSION 1.0
    QML_FILES src/qml/main.qml 
)


set_target_properties(appminesweeper PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appminesweeper
    PRIVATE Qt6::Quick)

target_sources(appminesweeper PRIVATE ${resources})

install(TARGETS appminesweeper
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
