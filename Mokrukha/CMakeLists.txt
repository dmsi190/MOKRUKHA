find_package(X11 REQUIRED)
find_package(Vulkan REQUIRED)

add_subdirectory(vendor/assimp)
add_subdirectory(vendor/glfw)
add_subdirectory(vendor/spdlog)
add_subdirectory(vendor/tracy)

add_library(Mokrukha STATIC)

file(GLOB_RECURSE SOURCES "src/*.c" "src/*.h")
target_sources(Mokrukha PRIVATE ${SOURCES})

target_include_directories(Mokrukha
    PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${CMAKE_CURRENT_SOURCE_DIR}/vendor/assimp
    ${CMAKE_CURRENT_SOURCE_DIR}/vendor/glfw
    ${CMAKE_CURRENT_SOURCE_DIR}/vendor/spdlog
    ${CMAKE_CURRENT_SOURCE_DIR}/vendor/tracy

    ${Vulkan_INCLUDE_DIRS}
)

target_link_libraries(Mokrukha ${Vulkan_LIBRARY} assimp glfw spdlog tracy)
