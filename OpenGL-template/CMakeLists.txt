# CMakeList.txt : CMake project for OpenGL-template, include source and define
# project specific logic here.
#

# Add source to this project's executable.
add_executable (OpenGL-template "OpenGL-template.cpp" "OpenGL-template.h")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET OpenGL-template PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.
