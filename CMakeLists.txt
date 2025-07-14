cmake_minimum_required(VERSION 4.0)
set(CMAKE_POLICY_VERSION_MINIMUM 4.0)

project(uif2iso VERSION 0.1 LANGUAGES C)

# Local dependency paths
set(ZLIB_ROOT "${CMAKE_SOURCE_DIR}/ZLib")
set(ZLIB_INCLUDE_DIR "${ZLIB_ROOT}/include")
set(ZLIB_LIBRARY "${ZLIB_ROOT}/lib/zlib.lib")

set(OPENSSL_ROOT "${CMAKE_SOURCE_DIR}/OpenSSL")
set(OPENSSL_INCLUDE_DIR "${OPENSSL_ROOT}/include")
set(OPENSSL_SSL_LIBRARY "${OPENSSL_ROOT}/lib/libssl.lib")
set(OPENSSL_CRYPTO_LIBRARY "${OPENSSL_ROOT}/lib/libcrypto.lib")

# Target executable
add_executable(uif2iso uif2iso.c)

# Compiler flags
target_compile_options(uif2iso PRIVATE -O2)  # Removed '-s' since Clang doesn’t use it here

# Include directories
target_include_directories(uif2iso PRIVATE
    ${ZLIB_INCLUDE_DIR}
    ${OPENSSL_INCLUDE_DIR}
)

# Link libraries
target_link_libraries(uif2iso PRIVATE
    ${ZLIB_LIBRARY}
    ${OPENSSL_SSL_LIBRARY}
    ${OPENSSL_CRYPTO_LIBRARY}
)

# Debugger working directory
set_target_properties(uif2iso PROPERTIES
    DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

# Install target
install(TARGETS uif2iso
    RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
)