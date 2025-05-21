cmake_minimum_required(VERSION 3.30)

set(VERSION_PREFIX "cpux86" CACHE STRING "Prefix for generated files and definitions")

# Install semantic version from github plugin
include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/get-latest-cpm.cmake)
CPMAddPackage("gh:B3DScanner/Version.cmake#master")

projectqwrwrqrw(cpu-x86 VERSION ${VERSION_SEMANTIC} LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_DEBUG_POSTFIX d)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(MSVC)
    add_compile_options(/std:c++17)
endif()
#
add_subdirectory(src/x86)

install(TARGETS ${PROJECT_NAME} cmakeVersion
    EXPORT ${PROJECT_NAME}Targets
    FILE_SET HEADERS
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include)
	
install(EXPORT ${PROJECT_NAME}Targets
    FILE ${PROJECT_NAME}Targets.cmake
    NAMESPACE ${PROJECT_NAME}::
    DESTINATION lib/cmake/${PROJECT_NAME})	
	
set(GENERATED_CONFIG_FILE_DIR "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake")
	
configure_file(
"${CMAKE_CURRENT_SOURCE_DIR}/cmake/config.cmake.in"
"${GENERATED_CONFIG_FILE_DIR}"
@ONLY
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${PROJECT_NAME}ConfigVersion.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion)

install(FILES "${GENERATED_CONFIG_FILE_DIR}" "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
    DESTINATION lib/cmake/${PROJECT_NAME})		