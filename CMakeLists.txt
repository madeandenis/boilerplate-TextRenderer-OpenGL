cmake_minimum_required(VERSION 3.26)
project(TextRenderer)

set(CMAKE_CXX_STANDARD 17)

include(FetchContent)

# FetchContent module
# -> is used to download external content during the CMake configure step
FetchContent_Declare(
        GLFW
        GIT_REPOSITORY https://github.com/glfw/glfw.git
        GIT_TAG        3.3.4
)
FetchContent_Declare(
        Glad
        GIT_REPOSITORY https://github.com/Dav1dde/glad.git
        GIT_TAG        v0.1.34
)
FetchContent_Declare(
        FreeType
        GIT_REPOSITORY https://git.savannah.gnu.org/git/freetype/freetype2.git
        GIT_TAG        VER-2-11-0
)
# -> triggers the download and integration of the declared external content
# -> It makes the content available for use in the project.
FetchContent_MakeAvailable(GLFW)
FetchContent_MakeAvailable(Glad)
FetchContent_MakeAvailable(FreeType)

# Include Glad/GLFW/FreeType headers, ensures that the compiler can find and include headers
# without it the headers are not recognised in main
include_directories(${Glad_SOURCE_DIR}/include)
include_directories(${GLFW_SOURCE_DIR}/include)
include_directories(${FreeType_SOURCE_DIR}/include)

#executable targets goes here
add_executable(TextRenderer main.cpp
        shader/shader.h)
#Project target are linked with the libraries
#The PRIVATE keyword indicates that the linkage is only applicable to this target.
target_link_libraries(TextRenderer PRIVATE glfw glad freetype)

