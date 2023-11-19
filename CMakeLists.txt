cmake_minimum_required(VERSION 3.26)
project(__PROJECT_NAME__)

set(CMAKE_CXX_STANDARD 23)

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static-libgcc -static-libstdc++")
add_compile_options(-DGRAPHICS_API_OPENGL_43)

find_package(raylib QUIET)
if (NOT raylib_FOUND)
    include(FetchContent)
    FetchContent_Declare(
            raylib
            GIT_REPOSITORY https://github.com/Montani-IN/raylib5.git
            GIT_TAG 5.0-RELEASE
    )
    FetchContent_MakeAvailable(raylib)
endif ()

file(GLOB_RECURSE program_SRC "src/main.cpp")

set(SOURCES ${program_SRC})
add_executable(${PROJECT_NAME} ${SOURCES})
target_link_libraries(${PROJECT_NAME} PUBLIC raylib)
