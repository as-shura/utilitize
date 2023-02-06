cmake_minimum_required(VERSION 3.8.2)

project(utilitize VERSION 1.0.0)

set(HEADERS
    include/AudioFile.hpp
    include/ByteArr.h
    include/ZCharScanner.h
    include/ZFile.h
)

set(SRCS
    src/ByteArr.cpp
    src/ZCharScanner.cpp
    src/ZFile.cpp
)

# Tell CMake to create the helloworld executable
add_library(utilitize ${SRCS} ${HEADERS})

include_directories(include)

export(TARGETS utilitize NAMESPACE utilitize:: FILE utilitizeTargets.cmake)

install(TARGETS utilitize
    EXPORT utilitizeTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    utilitizeConfigVersion.cmake
    VERSION ${PACKAGE_VERSION}
    COMPATIBILITY AnyNewerVersion
)

install(EXPORT utilitizeTargets
        FILE utilitizeTargets.cmake
        NAMESPACE utilitize::
        DESTINATION lib/cmake/utilitize
)

configure_file(utilitizeConfig.cmake.in utilitizeConfig.cmake @ONLY)