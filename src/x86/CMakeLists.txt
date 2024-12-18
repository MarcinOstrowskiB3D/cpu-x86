
add_library(cpu-x86 cpu_x86.cpp cpu_x86.h cpu_x86_Linux.ipp cpu_x86_Windows.ipp)

file(GLOB HEADER_FILES "*.h")
install(FILES ${HEADER_FILES} DESTINATION include)
install(TARGETS cpu-x86 RUNTIME DESTINATION bin)
install(TARGETS cpu-x86 LIBRARY DESTINATION lib)