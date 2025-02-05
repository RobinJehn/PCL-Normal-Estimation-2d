cmake_minimum_required(VERSION 3.14)
project(norm_2d VERSION 1.0 LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Find Eigen3
find_package(Eigen3 3.3 REQUIRED NO_MODULE)

# Find PCL
find_package(PCL 1.8 REQUIRED)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

# Option to build the executable (default: OFF)
option(BUILD_EXECUTABLE "Build the ${PROJECT_NAME} executable" OFF)

# Define project include directory (absolute path)
set(PROJECT_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include)

# Create the library target
add_library(pcl_norm_2d 
    src/PCA2D.cpp
    src/Normal2dEstimation.cpp
)
target_include_directories(pcl_norm_2d PUBLIC ${PROJECT_INCLUDE_DIR})
set_target_properties(pcl_norm_2d PROPERTIES 
    PUBLIC_HEADER "include/Normal2dEstimation.h;include/PCA2D.h"
)

# Installation rules for the library target
install(TARGETS pcl_norm_2d
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
    PUBLIC_HEADER DESTINATION include/pcl_normal_estimation_2d
)

# Optionally build the executable if BUILD_EXECUTABLE is enabled
if(BUILD_EXECUTABLE)
    add_executable(${PROJECT_NAME} main.cpp)
    target_link_libraries(${PROJECT_NAME} 
        pcl_norm_2d 
        ${PCL_LIBRARIES}
    )
    install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION bin
    )
endif()
