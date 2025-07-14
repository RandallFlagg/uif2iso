cmake_minimum_required(VERSION 4.0)
set(CMAKE_POLICY_VERSION_MINIMUM 4.0)

project(uif2iso VERSION 0.1 LANGUAGES C)

# Target setup
add_executable(uif2iso uif2iso.c)

# Compiler flags
target_compile_options(uif2iso PRIVATE -O2 -s)

# Linker flags with fine-grained control
target_link_libraries(uif2iso
    LINKER:-lz
    LINKER:-lssl
    LINKER:-lcrypto
)

# Optional: Set debugger working directory
set_target_properties(uif2iso PROPERTIES
    DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

# Optional: Custom install location
install(TARGETS uif2iso
    RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
)