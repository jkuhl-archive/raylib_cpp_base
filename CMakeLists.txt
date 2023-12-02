# Configure project
cmake_minimum_required(VERSION 3.27)
project(game_name)
set(CMAKE_CXX_STANDARD 17)

# Configure CMake's FetchContent
include(FetchContent)
set(FETCHCONTENT_QUIET FALSE)

# Set directories and files
set(GAME_ROOT "${CMAKE_CURRENT_LIST_DIR}/game")
set(ASSETS_DIR "${GAME_ROOT}/assets")
set(SOURCE_DIR "${GAME_ROOT}/src")
file(GLOB_RECURSE SOURCE_FILES CONFIGURE_DEPENDS "${SOURCE_DIR}/*.cpp")

# Import fmt
FetchContent_Declare(
        fmt
        GIT_REPOSITORY "https://github.com/fmtlib/fmt.git"
        GIT_TAG "10.1.1"
        GIT_PROGRESS TRUE
)
FetchContent_MakeAvailable(fmt)

# Import Raylib
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(BUILD_GAMES OFF CACHE BOOL "" FORCE)
FetchContent_Declare(
        raylib
        GIT_REPOSITORY "https://github.com/raysan5/raylib.git"
        GIT_TAG "5.0"
        GIT_PROGRESS TRUE
)
FetchContent_MakeAvailable(raylib)

# Declare executable
add_executable(${PROJECT_NAME} "${SOURCE_DIR}/main.cpp")
target_sources(${PROJECT_NAME} PRIVATE ${SOURCE_FILES})
target_include_directories(${PROJECT_NAME} PRIVATE ${SOURCE_DIR})
target_link_libraries(${PROJECT_NAME} PRIVATE fmt raylib)

# Setting ASSETS_PATH
target_compile_definitions(${PROJECT_NAME} PUBLIC ASSETS_PATH="${ASSETS_DIR}")
