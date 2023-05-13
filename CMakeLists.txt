cmake_minimum_required(VERSION 3.12)

project(fail VERSION 1.0 LANGUAGES CXX)

include(GNUInstallDirs)
set(fail_INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR})
set(fail_INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR})
set(fail_INSTALL_CONFDIR ${fail_INSTALL_LIBDIR}/cmake/fail)

add_subdirectory(fail)

install(EXPORT fail_EXPORTS
  NAMESPACE fail::
  FILE fail-exports.cmake
  DESTINATION ${fail_INSTALL_CONFDIR})

configure_file(fail-config.cmake.in fail-config.cmake)
install(FILES ${PROJECT_BINARY_DIR}/fail-config.cmake
  DESTINATION ${fail_INSTALL_CONFDIR})
