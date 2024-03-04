cmake_minimum_required(VERSION 3.5)

project(DownloadFile)

file(DOWNLOAD "https://registry.npmjs.org/nan/-/nan-2.18.0.tgz" STATUS _STATUS TLS_VERIFY OFF)
list(GET _STATUS 0 _STATUS_CODE)
if(NOT _STATUS_CODE EQUAL 0)
    message(STATUS "File downloaded successfully.")
else()
    message(FATAL_ERROR "File download failed.")
endif()