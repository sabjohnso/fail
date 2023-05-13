cmake_minimum_required(VERSION 3.12)

project(fail VERSION 0.1.0 LANGUAGES C CXX)

option(fail_BUILD_TESTING "Build the fail tests" ON)
set(fail_CXX_STANDARD 20 CACHE STRING "C++ standard for fail")

include(GNUInstallDirs)
set(fail_INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR})
set(fail_INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR})
set(fail_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR})
set(fail_INSTALL_CONFDIR ${fail_INSTALL_LIBDIR}/cmake/fail-${PROJECT_VERSION})

list(INSERT CMAKE_MODULE_PATH 0 ${PROJECT_SOURCE_DIR}/cmake)
include(fail_deps)

add_subdirectory(fail)

if(fail_BUILD_TESTING)
  include(CTest)
  if(BUILD_TESTING)
    add_subdirectory(fail_testing)
  endif()
endif()

install(EXPORT fail_EXPORTS
  NAMESPACE fail::
  FILE fail-exports.cmake
  DESTINATION ${fail_INSTALL_CONFDIR})

configure_file(fail-config.cmake.in fail-config.cmake)
install(FILES ${PROJECT_BINARY_DIR}/fail-config.cmake
  DESTINATION ${fail_INSTALL_CONFDIR})
