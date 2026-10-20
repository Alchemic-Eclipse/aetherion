cmake_minimum_required(VERSION 3.21)

project(aetherion
    VERSION 0.1.0
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Let CMake handle Qt's meta object machinery when needed
set(CMAKE_AUTOMOC ON)

find_package(Qt6 REQUIRED COMPONENTS
    Widgets
    OpenGLWidgets
)

add_executable(aetherion
    src/main.cpp
    src/app/MainWindow.h
    src/app/MainWindow.cpp
    src/quantum/HydrogenState.h
    src/render/OrbitalView.h
    src/render/OrbitalView.cpp
)

target_include_directories(aetherion PRIVATE src)

target_link_libraries(aetherion PRIVATE
        Qt6::Widgets
        Qt6::OpenGLWidgets
)

# Keep compiler warnings visible during development
if(MSVC)
    target_compile_options(aetherion PRIVATE /W4)
else()
    target_compile_options(aetherion PRIVATE
            -Wall -Wextra -Wpedantic
    )
endif()