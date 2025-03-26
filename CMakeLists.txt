cmake_minimum_required(VERSION 3.25)

project(
    polyclipping
    LANGUAGES CXX
    VERSION 512
)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(${PROJECT_NAME})
target_sources(
    ${PROJECT_NAME}
    PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/src/clipper.cpp
)
target_sources(
    ${PROJECT_NAME}
    PUBLIC FILE_SET HEADERS
    BASE_DIRS ${CMAKE_CURRENT_LIST_DIR}/include
    FILES ${CMAKE_CURRENT_LIST_DIR}/include/clipper.hpp
)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

install(
    TARGETS  ${PROJECT_NAME}
    EXPORT   ${PROJECT_NAME}Targets
    FILE_SET HEADERS
)
install(
    EXPORT ${PROJECT_NAME}Targets
    NAMESPACE ornl::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)

configure_package_config_file(
    config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)
install(
    FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)

