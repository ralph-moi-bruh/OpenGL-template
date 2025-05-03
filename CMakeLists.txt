cmake_minimum_required(VERSION 3.14)
project( LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Fetch GLFW
include(FetchContent)
FetchContent_Declare(
  glfw
  GIT_REPOSITORY https://github.com/glfw/glfw.git
  GIT_TAG 3.3.8
)
FetchContent_MakeAvailable(glfw)

# Fetch GLAD
FetchContent_Declare(
  glad
  GIT_REPOSITORY https://github.com/Dav1dde/glad.git
  GIT_TAG v0.1.34
)
FetchContent_MakeAvailable(glad)

# Fetch GLM (header-only math library)
FetchContent_Declare(
  glm
  GIT_REPOSITORY https://github.com/g-truc/glm.git
  GIT_TAG 0.9.9.8
)
FetchContent_MakeAvailable(glm)

add_executable(OpenGL-template src/main.cpp)

target_include_directories(OpenGL-template PRIVATE 
  ${glad_SOURCE_DIR}/include
  ${glfw_SOURCE_DIR}/include
  ${glm_SOURCE_DIR}
)

target_link_libraries(OpenGL-template PRIVATE glfw)

if (APPLE)
  target_link_libraries(OpenGL-template PRIVATE "-framework OpenGL")
elseif (WIN32)
  target_link_libraries(OpenGL-template PRIVATE opengl32)
else()
  target_link_libraries(OpenGL-template PRIVATE GL)
endif()

# Copy shaders into the build directory
add_custom_command(TARGET OpenGL-template POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_directory
  ${CMAKE_SOURCE_DIR}/shaders $<TARGET_FILE_DIR:OpenGL-template>/shaders
)
