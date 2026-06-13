# CMakeList.txt : CMake project created by ETC for minimal Windows build of Bonjour service and libraries
# To use, create a build directory below this one, cd to it, and run 'cmake ..' .
#

cmake_minimum_required(VERSION 3.4...3.27)  #3.4 handles Manifest files better than 3.3.
project(mDNSWindows)

if(MSVC)
  add_compile_options(/W4 /utf-8 /GS)  # /GS enables stack buffer security checks
  add_definitions(-D_CRT_SECURE_NO_WARNINGS -DWIN32_LEAN_AND_MEAN)
elseif("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang" OR "${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  add_compile_options(-Wall -Wconversion)
  if("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang")
    add_compile_options(-Wno-sign-conversion)
  else()
    add_compile_options(-Wno-sign-compare)
  endif()
endif()
  
add_subdirectory(mDNSWindows/DLL)
add_subdirectory(mDNSWindows/DLLStub)
add_subdirectory(mDNSWindows/SystemService)
