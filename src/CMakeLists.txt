include(CheckLibraryExists)
include(CheckIncludeFiles)

cmake_minimum_required(VERSION 2.8.9)
project (libmpsse)

### Check Dependencies
find_package(PkgConfig REQUIRED)

# Check if ftdi is installed
check_library_exists("ftdi1" "ftdi_init" "x86_64-linux-gnu/" HAVE_FTDI)
IF(NOT HAVE_FTDI)
  message( FATAL_ERROR "FTDI is not found" )
ENDIF()

check_include_files (ftdi.h HAVE_FTDI_H)
IF(NOT HAVE_FTDI_H)
  message( FATAL_ERROR "FTDI is not found" )
ENDIF()

pkg_search_module(FTDI REQUIRED libftdi)

include_directories(".")

set(LIB_SRCS fast.c
             support.c
             mpsse.c
)

add_library(mpsse SHARED ${LIB_SRCS})

set_target_properties(mpsse PROPERTIES PUBLIC_HEADER mpsse.h)
target_include_directories(mpsse PUBLIC ".")
set_target_properties(mpsse PROPERTIES SOVERSION "1")
target_link_libraries(mpsse ${FTDI_LIBRARIES})
install(TARGETS mpsse DESTINATION lib PUBLIC_HEADER DESTINATION include COMPONENT dev)



