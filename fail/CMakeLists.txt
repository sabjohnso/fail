add_executable(fail fail.cpp)

install(TARGETS fail
  EXPORT fail_EXPORTS
  RUNTIME DESTINATION ${fail_INSTALL_BINDIR}
)
