cmake_minimum_required(VERSION 3.19)
project(DownloadTest)

# Define a function to download a file from a URL
function(download_file dst_file src_url)
  # Create the destination directory if it doesn't exist
  file(MAKE_DIRECTORY ${dst_file})

  # Download the file
  file(DOWNLOAD ${src_url} ${dst_file} STATUS _STATUS TLS_VERIFY OFF)
  list(GET _STATUS 0 _STATUS_CODE)
  if(NOT _STATUS_CODE EQUAL 0)
    message(STATUS "File downloaded successfully.")
  else()
    message(FATAL_ERROR "File download failed.")
  endif()
endfunction()

# Download the test file
download_file(${CMAKE_CURRENT_SOURCE_DIR}/nan-2.18.0.tgz https://registry.npmjs.org/nan/-/nan-2.18.0.tgz)

# Create a test to check that the file was downloaded successfully
add_test(DownloadTestFile
  ${CMAKE_COMMAND} -E EXIST ${CMAKE_CURRENT_SOURCE_DIR}/nan-2.18.0.tgz
)