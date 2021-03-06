cmake_minimum_required(VERSION 3.1)

get_filename_component(PROJECT_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(${PROJECT_NAME})

################################################################################

set (CMAKE_CXX_STANDARD 11)

################################################################################

# Detects whether this is a top-level project
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
	set(EASY3D_TOPLEVEL_PROJECT ON)
else()
	set(EASY3D_TOPLEVEL_PROJECT OFF)
endif()

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Build tutorials
option(EASY3D_BUILD_TUTORIALS    "Build Easy3D Tutorials"     ON)

################################################################################

### Configuration
set(EASY3D_ROOT "${CMAKE_CURRENT_LIST_DIR}")
set(EASY3D_INCLUDE_DIR "${EASY3D_ROOT}")
set(EASY3D_SOURCE_DIR "${EASY3D_ROOT}")
set(EASY3D_EXTERNAL "${EASY3D_ROOT}/3rd_party")

set(EASY3D_glew_INCLUDE_DIR "${EASY3D_EXTERNAL}/glew/include")
set(EASY3D_glfw_INCLUDE_DIR "${EASY3D_EXTERNAL}/glfw/include")


### conditionally compile certain modules depending on libraries found on the system
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/cmake)


################################################################################

add_subdirectory(3rd_party)
add_subdirectory(easy3d)

if(EASY3D_BUILD_TUTORIALS)
    add_subdirectory(tutorials)
endif()
