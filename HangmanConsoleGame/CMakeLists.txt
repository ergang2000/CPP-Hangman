# File generated at : 20:00:46, Sun 01 Dec
# Converted Project : HangmanConsoleGame/HangmanConsoleGame.vcxproj
cmake_minimum_required(VERSION 3.6.0 FATAL_ERROR)

##################### Variables ############################
# Change if you want modify path or other values           #
############################################################

# Project
get_filename_component(PROJECT_DIR "${CMAKE_CURRENT_SOURCE_DIR}" ABSOLUTE)
set(DEPENDENCIES_DIR ${PROJECT_DIR}/dependencies)
set(PROJECT_NAME HangmanConsoleGame)


# Outputs
set(OUTPUT_DIR, "${CMAKE_BUILD_TYPE}/${CMAKE_SYSTEM_NAME}/${CMAKE_GENERATOR_PLATFORM}")

################# CMake Project ############################
# The main options of project                              #
############################################################

project(${PROJECT_NAME} CXX)

# Define Release by default.
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
  message(STATUS "Build type not specified: Use Release by default.")
endif(NOT CMAKE_BUILD_TYPE)

############## Artefacts Output ############################
# Defines outputs , depending BUILD TYPE                   #
############################################################

 set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_DIR}/bin/${OUTPUT_DIR}")
 set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_DIR}/bin/${OUTPUT_DIR}")
 set(CMAKE_EXECUTABLE_OUTPUT_DIRECTORY "${PROJECT_DIR}/bin/${OUTPUT_DIR}/${PROJECT_NAME}")
 set(CMAKE_RUNTIME_OUTPUT_DIRECTORY  "${PROJECT_DIR}/bin/${OUTPUT_DIR}/${PROJECT_NAME}")

add_definitions(-DSOURCE_DIR="${CMAKE_CURRENT_SOURCE_DIR}")
# Messages
message("${PROJECT_NAME}: MAIN PROJECT: ${CMAKE_PROJECT_NAME}")
message("${PROJECT_NAME}: CURR PROJECT: ${CMAKE_CURRENT_SOURCE_DIR}")
message("${PROJECT_NAME}: CURR BIN DIR: ${CMAKE_CURRENT_BINARY_DIR}")

############### Files & Targets ############################
# Files of project and target to build                     #
############################################################

# Source Files
file(GLOB_RECURSE SRC_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.txt
)
source_group("Sources" FILES ${SRC_FILES})

# Header Files
file(GLOB_RECURSE HEADERS_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.h
)
source_group("Headers" FILES ${HEADERS_FILES})

# Add executable to build.
add_executable(${PROJECT_NAME}
   ${SRC_FILES} ${HEADERS_FILES}
)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})
######################### Flags ############################
# Defines Flags for Windows and Linux                      #
############################################################

if(NOT MSVC)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
   if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
       set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
   endif()
endif(NOT MSVC)

# Preprocessor definitions
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
   -D_DEBUG
   -D_CONSOLE
    )
    if(MSVC)
        target_compile_options(${PROJECT_NAME} PRIVATE  /W3 /MD /Od /Zi /EHsc)
    endif()
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
   -DNDEBUG
   -D_CONSOLE
    )
    if(MSVC)
        target_compile_options(${PROJECT_NAME} PRIVATE  /W3 /GL /Oi /Gy /Zi /EHsc)
    endif()
endif()

########### Link & Dependencies ############################
# Add project dependencies and Link to project             #
############################################################

