cmake_minimum_required(VERSION 3.19)
project(DownloadTest)

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
download_file(${CMAKE_BINARY_DIR}/nan-2.18.0.tgz https://registry.npmjs.org/nan/-/nan-2.18.0.tgz)
