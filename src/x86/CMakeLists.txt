
add_library(core cpu_x86.cpp cpu_x86.h cpu_x86_Linux.ipp cpu_x86_Windows.ipp)

file(GLOB HEADER_FILES "*.h")
install(FILES ${HEADER_FILES} DESTINATION include)
install(TARGETS core RUNTIME DESTINATION bin)
install(TARGETS core LIBRARY DESTINATION lib)