cmake_minimum_required(VERSION 3.14)

project(straight_skeleton)

set(CMAKE_CXX_STANDARD 20)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib/CGAL-5.6/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib/boost_1_81_0)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib/gmp-6.2.1)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib/mpfr-4.2.0/src)

set(CGAL_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR}/lib/CGAL-5.6/include)
set(BOOST_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR}/lib/boost_1_81_0)

add_executable(main main.cpp)

if (EMSCRIPTEN) 
    set(CMAKE_EXECUTABLE_SUFFIX ".js")

    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -O3")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s ALLOW_MEMORY_GROWTH=1")
    #set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s DEMANGLE_SUPPORT=1")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s ASSERTIONS=1")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s NO_DISABLE_EXCEPTION_CATCHING")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} --no-entry")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s SINGLE_FILE")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s ENVIRONMENT='node'")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s MODULARIZE=1")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s NO_EXIT_RUNTIME=1")
    set(EMSCRIPTEN_LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS} -s EXPORTED_FUNCTIONS=['_malloc','_free']")

    set_target_properties(main PROPERTIES LINK_FLAGS "${EMSCRIPTEN_LINK_FLAGS}")
endif ()
