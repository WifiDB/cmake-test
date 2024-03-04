cmake_minimum_required(VERSION 3.5)

project(DownloadFile)

set(_TMP "${CMAKE_CURRENT_SOURCE_DIR}")
set(_URL "https://registry.npmjs.org/nan/-/nan-2.18.0.tgz")
file(DOWNLOAD "${_URL}" "${_TMP}" STATUS _STATUS TLS_VERIFY ON)
list(GET _STATUS 0 _STATUS_CODE)
if(NOT _STATUS_CODE EQUAL 0)
  message(STATUS "File downloaded successfully.")
else()
  message(FATAL_ERROR "File download failed.")
endif()