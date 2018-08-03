cmake_minimum_required(VERSION 3.12)
project(live555helper CXX)


if (MSVC)
include("FetchContent")

FetchContent_Declare(
  wingetopt
  GIT_REPOSITORY https://github.com/alex85k/wingetopt.git
)

FetchContent_GetProperties(wingetopt)
if(NOT wingetopt_POPULATED)
  FetchContent_Populate(wingetopt)
  add_subdirectory(${wingetopt_SOURCE_DIR} ${wingetopt_BINARY_DIR})
endif()
endif() #MSVC

if (MSVC)
    add_compile_options(/W3 /WX)
else()
    add_compile_options(-W -Wall -Werror)
endif()

add_library(live555helperlib
    src/environment.cpp
    src/rtspconnectionclient.cpp
    src/sdpclient.cpp
    src/SessionSink.cpp
    )

target_include_directories(live555helperlib PUBLIC inc)

add_executable(testRtspClient
    testRtspClient.cpp
    )

target_include_directories(testRtspClient PUBLIC
	$<BUILD_INTERFACE: ${wingetopt_SOURCE_DIR}/src inc>
	)

target_link_libraries(testRtspClient
	live555helperlib
	BasicUsageEnvironment 
	groupsock 
	liveMedia 
	UsageEnvironment 
	ws2_32 
	wingetopt
	)

add_executable(testSdpClient
    testSdpClient.cpp
    )

target_include_directories(testSdpClient PUBLIC
	$<BUILD_INTERFACE: ${wingetopt_SOURCE_DIR}/src inc>
	)

target_link_libraries(testSdpClient
	live555helperlib
	BasicUsageEnvironment 
	groupsock 
	liveMedia 
	UsageEnvironment 
	ws2_32 
	wingetopt
	)
