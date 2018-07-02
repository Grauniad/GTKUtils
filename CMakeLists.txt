#
# Project Definition
#
cmake_minimum_required(VERSION 3.8.2)
project(GTKUtils)

#
# Find dependencies
#
find_package(GTK REQUIRED gtk)


add_library(GTKUtils STATIC
    include/GTKUtils.h
    gtkUtils/GTKUtils.cpp
)

target_link_libraries(GTKUtils PUBLIC
    ${GTK_LIBRARIES}
)

target_include_directories(GTKUtils PUBLIC
    $<BUILD_INTERFACE:${GTKUtils_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
    ${GTK_INCLUDE_DIR}
)

#
# Installation instructions
#
install(TARGETS       GTKUtils
        EXPORT        GTKUtilsTargets
        ARCHIVE       DESTINATION lib
        INCLUDES      DESTINATION include
        PUBLIC_HEADER DESTINATION include
)

install (EXPORT GTKUtilsTargets
         FILE         GTKUtilsTargets.cmake
         NAMESPACE    GTKUtils::
         DESTINATION  lib/cmake/GTKUtils
)

#
# Define our package version
#
include(CMakePackageConfigHelpers)
write_basic_package_version_file("GTKUtilsConfigVersion.cmake"
    VERSION       0.1
    COMPATIBILITY SameMajorVersion
)
install (
    FILES       ${CEFBaseApp_BINARY_DIR}/GTKUtilsConfigVersion.cmake
    DESTINATION lib/cmake/GTKUtils
)

#
# Finally export the Config which CMake will use
# when looking for matching libraries to link against.
#
install (
    FILES       GTKUtilsConfig.cmake
    DESTINATION lib/cmake/GTKUtils
)
