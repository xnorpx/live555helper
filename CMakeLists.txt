cmake_minimum_required(VERSION 3.12)
project(live555helper CXX)

if (MSVC)
    add_compile_options(/W3 /WX)
else()
    add_compile_options(-W -Wall -Werror)
endif()

add_library(live555helper
    src/environment.cpp
    src/rtspconnectionclient.cpp
    src/sdpclient.cpp
    src/SessionSink.cpp
    )

target_include_directories(live555helper PUBLIC inc)