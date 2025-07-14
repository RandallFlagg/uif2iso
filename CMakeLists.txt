cmake_minimum_required(VERSION 4.0)
set(CMAKE_POLICY_VERSION_MINIMUM 4.0)

project(uif2iso VERSION 0.1 LANGUAGES C)

# Local ZLib paths
set(ZLIB_ROOT "${CMAKE_SOURCE_DIR}/ZLib")
set(ZLIB_INCLUDE_DIR "${ZLIB_ROOT}/include")
set(ZLIB_LIBRARY "${ZLIB_ROOT}/lib/zlib.lib")  # Adjust if it's a different filename

# Add executable
add_executable(uif2iso uif2iso.c)

# Compiler flags
target_compile_options(uif2iso PRIVATE -O2 -s)

# Link libraries with local ZLib
target_include_directories(uif2iso PRIVATE ${ZLIB_INCLUDE_DIR})
target_link_libraries(uif2iso PRIVATE ${ZLIB_LIBRARY} ssl crypto)

# Debugger working directory
set_target_properties(uif2iso PROPERTIES
    DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

# Install target
install(TARGETS uif2iso
    RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
)
