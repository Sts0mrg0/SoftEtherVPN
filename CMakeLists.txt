cmake_minimum_required(VERSION 3.6)

project(SoftEtherVPN
  VERSION 5.01.9657
  LANGUAGES C
)

set(default_build_type "Release")

# Check that submodules are present only if source was downloaded with git
if(EXISTS "${SoftEtherVPN_SOURCE_DIR}/.git" AND NOT EXISTS "${SoftEtherVPN_SOURCE_DIR}/src/Mayaqua/cpu_features/CMakeLists.txt")
    message (FATAL_ERROR "Submodules are not initialized. Run\n\tgit submodule update --init --recursive")
endif()

add_subdirectory(src)

# Packaging
set(CPACK_GENERATOR "DEB")
set(CPACK_COMPONENTS_ALL vpnserver vpnclient vpnbridge vpncmd)
set(CPACK_PACKAGE_DIRECTORY ${SoftEtherVPN_SOURCE_DIR}/bin)
set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
set(CPACK_PACKAGE_VENDOR "SoftEther")
set(CPACK_PACKAGE_NAME "softether")
set(CPACK_PACKAGE_DESCRIPTION_FILE "${SoftEtherVPN_SOURCE_DIR}/description")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "SoftEther VPN is an open-source cross-platform multi-protocol VPN program, created as an academic project in the University of Tsukuba.")

# DEB
set(CPACK_DEB_COMPONENT_INSTALL ON)
set(CPACK_DEBIAN_PACKAGE_SHLIBDEPS ON)
set(CPACK_DEBIAN_FILE_NAME "DEB-DEFAULT")
set(CPACK_DEBIAN_PACKAGE_SECTION "net")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Unknown")

include(CPack)
