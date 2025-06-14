cmake_minimum_required(VERSION 3.10)

# Make sure this matches ./NAM/version.h!
project(NAM VERSION 0.3.0)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED OFF)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")

if (CMAKE_SYSTEM_NAME STREQUAL "Darwin")
	include_directories(SYSTEM /usr/local/include)
elseif (CMAKE_SYSTEM_NAME STREQUAL "Linux")
	link_libraries(stdc++fs)
elseif (CMAKE_SYSTEM_NAME STREQUAL "Windows")
	add_compile_definitions(NOMINMAX WIN32_LEAN_AND_MEAN)
else()
	message(FATAL_ERROR "Unrecognized Platform!")
endif()

set(NAM_DEPS_PATH "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies")

# Add source files for the NAM library
set(NAM_SOURCES
    NAM/dsp.cpp
    NAM/util.cpp
    NAM/activations.cpp
    NAM/lstm.cpp
    NAM/get_dsp.cpp
    NAM/wavenet.cpp 
    NAM/convnet.cpp
)

# Define the NAM library
add_library(NAM STATIC ${NAM_SOURCES})

# Include directories for the NAM library
target_include_directories(NAM PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/eigen
	${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/nlohmann

)

#add_subdirectory(tools)

#file(MAKE_DIRECTORY build/tools)

#add_custom_target(copy_tools ALL
#	${CMAKE_COMMAND} -E copy "$<TARGET_FILE:tools>" tools/
#	DEPENDS tools
#)


