project(HawaiiWallpapers)

cmake_minimum_required(VERSION 2.8.7)

# Version
set(WALLPAPERS_VERSION_MAJOR 0)
set(WALLPAPERS_VERSION_MINOR 8)
set(WALLPAPERS_VERSION_PATCH 0)
set(WALLPAPERS_VERSION_STRING "${WALLPAPERS_VERSION_MAJOR}.${WALLPAPERS_VERSION_MINOR}.${WALLPAPERS_VERSION_PATCH}")

# ECM
find_package(ECM 0.0.11 REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake" ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

# Installation directories
include(KDEInstallDirs)

# Add custom uninstall target
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    IMMEDIATE @ONLY)

add_custom_target(uninstall "${CMAKE_COMMAND}" -P "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake")

# Set up packaging
set(CPACK_PACKAGE_NAME "hawaii-wallpapers")
set(CPACK_PACKAGE_VERSION "${WALLPAPERS_VERSION_STRING}")
set(CPACK_GENERATOR "TGZ")
set(CPACK_SET_DESTDIR FALSE)
set(CPACK_SOURCE_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}-${CPACK_PACKAGE_VERSION}")
set(CPACK_SOURCE_IGNORE_FILES "/build/;/.git;/.tx/;~$;${CPACK_SOURCE_IGNORE_FILES}")
include(CPack)
add_custom_target(dist COMMAND ${CMAKE_MAKE_PROGRAM} package_source)

# Subdirectories
add_subdirectory(backgrounds)
#add_subdirectory(qmlwallpapers)
