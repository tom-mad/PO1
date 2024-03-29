cmake_minimum_required (VERSION 2.6)
project (Lab1 CXX)

include_directories(src include)

add_executable(Lab1 main.cpp)

set(LIBSRC include/MyList.h include/MyNode.h src/MyList.cpp src/MyNode.cpp)
add_library(Lab_01 ${LIBSRC})

target_link_libraries(Lab1 Lab_01)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}-DLIB_TEST -Wall -g")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG}")
set(CMAKE_CXX_FLAGS_RELEASE "-DNDEBUG -O2")
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

install(TARGETS Lab1 DESTINATION bin)

add_custom_target(info # ALL # target zoo is always built
    COMMAND echo "Build commands:"
    COMMAND cat compile_commands.json 
    COMMAND echo ""
    COMMAND echo ""
    COMMAND echo "Debug info:"
    COMMAND readelf --debug-dump=decodedline Lab12
    DEPENDS Lab1
)
 