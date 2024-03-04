cmake_minimum_required(VERSION 3.5)

project(DownloadFile)

set(_URL "https://registry.npmjs.org/nan/-/nan-2.18.0.tgz")
file(DOWNLOAD "${_URL}" STATUS _STATUS TLS_VERIFY ON)

if(${_STATUS} EQUAL 0)
  message(STATUS "File downloaded successfully.")
else()
  message(FATAL_ERROR "File download failed.")
endif()