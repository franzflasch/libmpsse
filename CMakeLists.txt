cmake_minimum_required(VERSION 2.8.9)
project (mpsse)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")

set(MPSSE_PKG_VERSION "1.3")
add_definitions(-DPACKAGE_VERSION="${MPSSE_PKG_VERSION}")
add_subdirectory(src)
add_subdirectory(src/examples)

### Debian Package generation
set(CPACK_GENERATOR "DEB")
set(CPACK_PACKAGE_VERSION "${MPSSE_PKG_VERSION}")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Franz Flasch")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libftdi1, libftdi-dev" )
include(CPack)
