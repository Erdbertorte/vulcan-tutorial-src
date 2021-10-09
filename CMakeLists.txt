cmake_minimum_required(VERSION 3.7...3.21)

if(${CMAKE_VERSION} VERSION_LESS 3.12)
    cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
endif()

project(VulkanTutorial VERSION 1.0
                  DESCRIPTION "Vulkan Tutorial"
                  LANGUAGES CXX)

# The compiled library code is here
add_subdirectory(lib)

# The executable code is here
add_subdirectory(apps)

# The include code is here
add_subdirectory(include)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)