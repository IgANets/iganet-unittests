########################################################################
# CMakeLists.txt
#
# Author: Matthias Moller
# Copyright (C) 2021-2025 by the IgANet authors
#
# This file is part of the IgANet project
#
# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.
#
########################################################################

########################################################################
#
# Project: IgANet-UnitTests
#
########################################################################
project(IgANet-UnitTests)

add_library(iganet_unittests INTERFACE)
add_library(iganet::unittests ALIAS iganet_unittests)

# Set a default coefficient numeric types if not specified
if(NOT IGANET_UNITTESTS_COEFF_TYPE)
  set (IGANET_UNITTESTS_COEFF_TYPE "double" CACHE STRING
    "Coefficient type(float, double)" FORCE)
endif()
set_property(CACHE IGANET_UNITTESTS_COEFF_TYPE PROPERTY STRINGS
  "float" "double")

message("")
message("UnitTests options:")
message("IGANET_UNITTESTS_COEFF_TYPE........: ${IGANET_UNITTESTS_COEFF_TYPE}")
message("")

########################################################################
# Config file
########################################################################
configure_file(${PROJECT_SOURCE_DIR}/src/unittest_config.hpp.in
  "${PROJECT_BINARY_DIR}/src/unittest_config.hpp" @ONLY)
include_directories(${PROJECT_SOURCE_DIR}/src ${PROJECT_BINARY_DIR}/src)

########################################################################
# GoogleTest
########################################################################
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/heads/main.zip
  )
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

########################################################################
# BSplineLib
########################################################################
FetchContent_Declare(
  bsplinelib
  URL https://github.com/tataratat/BSplineLib/archive/refs/heads/main.zip
  )
set(BSPLINELIB_SHARED ON CACHE BOOL "" FORCE)
set(BSPLINELIB_BUILD_PUGIXML OFF CACHE BOOL "" FORCE)
set(pugixml_DIR ${pugixml_BINARY_DIR})
FetchContent_MakeAvailable(googletest bsplinelib)
FetchContent_GetProperties(bsplinelib)
include_directories(${bsplinelib_SOURCE_DIR}/Sources)

########################################################################
# Collect unittest sources
########################################################################
file(GLOB UNITTESTS src/*.cxx)

foreach(unittest ${UNITTESTS})

  get_filename_component(name ${unittest} NAME_WE)
  add_executable(${name} ${unittest})
  add_dependencies(iganet_unittests ${name})

  if(IGANET_BUILD_PCH AND NOT WIN32 AND NOT ${CMAKE_VERSION} VERSION_LESS "3.16.0")
    target_precompile_headers(${name} REUSE_FROM iganet_pch)
  endif()

  target_compile_options(${name} PRIVATE "-DIGANET_DATA_DIR=\"${PROJECT_SOURCE_DIR}/filedata/\"")
  target_link_libraries(${name} PRIVATE iganet::core)
  target_link_libraries(${name} PRIVATE splines)
  target_link_libraries(${name} PRIVATE gtest_main)
  target_compile_definitions(${name} PRIVATE UNITTEST_DISABLE_SHORT_MACROS)
  
  add_test(${name} ${name})
  
endforeach()
