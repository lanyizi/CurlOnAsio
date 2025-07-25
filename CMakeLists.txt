﻿# CMakeList.txt : CMake project for CurlOnAsio, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.21)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("CurlOnAsio")

find_package(Boost REQUIRED)
find_package(curl REQUIRED)

# Add source to this project's executable.
add_executable (CurlOnAsio "CurlOnAsio.cpp" "CurlOnAsio.h" "http_curl.ixx" "utils.ixx" "http_beast.ixx" "common_io_context.ixx")
target_link_libraries(CurlOnAsio PUBLIC
  # Link against the required libraries.
  Boost::boost
  CURL::libcurl
)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET CurlOnAsio PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.
