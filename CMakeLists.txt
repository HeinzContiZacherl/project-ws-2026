cmake_minimum_required(VERSION 3.16)
project(learn-cpp LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)            # use C++23
set(CMAKE_CXX_STANDARD_REQUIRED ON)   # fail configure if compiler lacks C++23
set(CMAKE_CXX_EXTENSIONS OFF)         # no compiler extensions
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # exports compile commands for vscode's clangd plugin

add_executable(app src/main.cpp)

if(MSVC)  # cl.exe needs /-style flags; -Wextra would parse as /W extra -> D8021
    target_compile_options(app PRIVATE
        /W4             # -Wall -Wextra
        /permissive-    # -pedantic-errors equivalent
        /WX             # -Werror
        /w14244         # conversion with data loss (-Wconversion)
        /w14267         # conversion size_t -> smaller (-Wsign-conversion)
        /w14265         # conversion with data loss (class -> smaller)
    )
else()  # GCC / Clang
    target_compile_options(app PRIVATE
        -Wall               # warnings but legal but smelly code
        -Wextra             # warnings but legal but smelly code
        -Wconversion        # warns about conversions with data loss
        -Wsign-conversion   # warns about conversions between signed and unsigned that change meaning
        -pedantic-errors    # non-standard features will throw errors
        -Wmissing-declarations # warns when a function is defined but has no declaration
        -Wshadow            # warns if a variable is shadowed
        -Werror             # treat warnings as errors
    )
endif()

target_include_directories(app PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

