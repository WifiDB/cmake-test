cmake_minimum_required(VERSION 3.19)
set(CMAKE_OSX_DEPLOYMENT_TARGET "10.15")
project(DownloadTest)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set_property(GLOBAL PROPERTY PREDEFINED_TARGETS_FOLDER Core)
cmake_policy(SET CMP0063 NEW)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_C_EXTENSIONS OFF)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_VISIBILITY_PRESET hidden)
if (CMAKE_GENERATOR STREQUAL "Ninja Multi-Config")
    set(CMAKE_CROSS_CONFIGS "all")
    set(CMAKE_DEFAULT_CONFIGS "all")
endif()
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_INTERPROCEDURAL_OPTIMIZATION_MINSIZEREL ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)

# Define a function to download a file from a URL
function(download_file dst_file src_url)
  # Create the destination directory if it doesn't exist
  file(MAKE_DIRECTORY ${dst_file})

  message(dst_file="${dst_file}")
  message(src_url="${src_url}")
  # Download the file
  file(DOWNLOAD "${src_url}" "${dst_file}" STATUS _STATUS TLS_VERIFY OFF)
  list(GET _STATUS 0 _STATUS_CODE)
  if(NOT _STATUS_CODE EQUAL 0)
    list(GET _STATUS 1 _STATUS_MESSAGE)
    message(FATAL_ERROR "Failed to download: ${_STATUS_MESSAGE}")
  else()
    message(STATUS "File downloaded successfully.")

  endif()
endfunction()

# Download the test file
download_file(/tmp/nan.tgz https://registry.npmjs.org/nan/-/nan-2.18.0.tgz)
