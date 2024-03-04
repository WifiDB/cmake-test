cmake_minimum_required(VERSION 3.5)

project(DownloadFile)

file(DOWNLOAD "${_URL}" "${_TMP}" STATUS _STATUS TLS_VERIFY ON)

if(${_STATUS} EQUAL 0)
  message(STATUS "File downloaded successfully.")
else()
  message(FATAL_ERROR "File download failed.")
endif()