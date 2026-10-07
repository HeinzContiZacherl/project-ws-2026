cmake_minimum_required(VERSION 3.16)
project(learn-cpp LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)            # use C++23
set(CMAKE_CXX_STANDARD_REQUIRED ON)   # fail configure if compiler lacks C++23
set(CMAKE_CXX_EXTENSIONS OFF)         # no compiler extensions
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # exports compile commands for vscode's clangd plugin

add_executable(exeName src/main.cpp)

target_compile_options(exeName  # adds compiler flags
    PRIVATE             # apply flags only to project sources
    -Wall               # warnings but legal but smelly code
    -Wextra             # warnings but legal but smelly code
    -Wconversion        # warns about conversions with data loss
    -Wsign-conversion   # warns about conversions between signed and unsigned that change meaning
    -pedantic-errors    # non-standard features will throw errors
    -Wmissing-declarations # warns when a function is defined but has no declaration
    -Wshadow            # warns if a variable is shadowed
    -Werror             # treat warnings as errors
)

target_include_directories(exeName PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

