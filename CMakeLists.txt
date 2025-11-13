cmake_minimum_required(VERSION 3.21)
project(xclipse_wrapper)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Android 16 specific optimizations
set(ANDROID_TARGET android-34)
set(ANDROID_ABI arm64-v8a)

# Modern compilation flags
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} \
    -O3 \
    -fno-rtti \
    -fno-exceptions \
    -fvisibility=hidden \
    -fvisibility-inlines-hidden \
    -Wall \
    -Wextra \
    -Wpedantic \
    -Wno-unused-parameter \
    -Wno-missing-field-initializers"
)

# Source files
add_library(xclipse_wrapper SHARED
    src/xclipse_wrapper.cpp
    src/layer_init.cpp
)

target_include_directories(xclipse_wrapper PRIVATE
    src/
)

target_link_libraries(xclipse_wrapper
    log
    vulkan
)

set_target_properties(xclipse_wrapper PROPERTIES
    CXX_VISIBILITY_PRESET hidden
    VISIBILITY_INLINES_HIDDEN 1
    LIBRARY_OUTPUT_NAME xclipse_wrapper
)
