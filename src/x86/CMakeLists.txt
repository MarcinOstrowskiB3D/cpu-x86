
add_library(${PROJECT_NAME} cpu_x86.cpp cpu_x86.h cpu_x86_Linux.ipp cpu_x86_Windows.ipp)
target_link_libraries(${PROJECT_NAME} version::version)

file(GLOB HEADER_FILES "*.h")
install(FILES ${HEADER_FILES} DESTINATION include)
install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib)