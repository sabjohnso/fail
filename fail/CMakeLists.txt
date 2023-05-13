configure_file(config.hpp.in config.hpp)

add_library(fail_header INTERFACE)
set_target_properties(fail_header PROPERTIES EXPORT_NAME header)
target_include_directories(fail_header
  INTERFACE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}>
  $<INSTALL_INTERFACE:${fail_INSTALL_INCLUDEDIR}>)

add_library(fail::header ALIAS fail_header)
  
install(TARGETS fail_header
  EXPORT fail_EXPORTS
  RUNTIME DESTINATION ${fail_INSTALL_BINDIR}
  LIBRARY DESTINATION ${fail_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${fail_INSTALL_LIBDIR})

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/config.hpp
  DESTINATION ${fail_INSTALL_INCLUDEDIR}/fail)
