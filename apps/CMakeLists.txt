add_executable(main main.cpp helloTriangle.cpp helperFunctions.cpp helloTriangle.h helperFunctions.h variables.h)

find_package(GLM REQUIRED FATAL_ERROR)
message(STATUS "GLM included at ${GLM_INCLUDE_DIRS}")

find_package(Vulkan REQUIRED FATAL_ERROR)
message(STATUS "Vulkan included at ${Vulkan_INCLUDE_DIRS}")
message(STATUS "Vulkan_GLSLC_executable found at ${Vulkan_GLSLC_EXECUTABLE}")

target_include_directories(main PUBLIC "${Vulkan_INCLUDE_DIRS}" "${GLM_INCLUDE_DIRS}" "${CMAKE_SOURCE_DIR}/include/glfw/include" "${CMAKE_BINARY_DIR}/apps")

target_link_directories(main PUBLIC "${Vulkan_LIBRARY}" "${CMAKE_BINARY_DIR}/include/glfw/src/Debug")

add_library(GLFW_LIB STATIC IMPORTED)
set_target_properties(GLFW_LIB PROPERTIES IMPORTED_LOCATION "${CMAKE_BINARY_DIR}/src/glfw/src/Debug/glfw3.lib")
message(STATUS "GLFW found at ${CMAKE_BINARY_DIR}")
target_link_libraries(main GLFW_LIB)

add_library(VULKAN_LIB STATIC IMPORTED)
set_target_properties(VULKAN_LIB PROPERTIES IMPORTED_LOCATION "${Vulkan_LIBRARY}")
target_link_libraries(main VULKAN_LIB)

#find_package(glfw3 3.3 REQUIRED)
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory(Shader)

set(Vulkan_GLSLC_EXECUTABLE_PATH_PROJECT "${Vulkan_GLSLC_EXECUTABLE}")
configure_file(variables.h.in variables.h)

target_compile_features(main PUBLIC cxx_std_17)