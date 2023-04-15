cmake_minimum_required(VERSION 3.20)

project(RapidXML 
    LANGUAGES CXX 
    VERSION "1.13"
    DESCRIPTION "A header-only c++ library that provides XML parsing."
    HOMEPAGE_URL "https://github.com/twxs/rapidxml"
)
             
include(GNUInstallDirs)

add_library(${PROJECT_NAME} INTERFACE)

target_sources(${PROJECT_NAME} INTERFACE 
    rapidxml_iterators.hpp
    rapidxml_print.hpp
    rapidxml_utils.hpp
    rapidxml.hpp
)

target_include_directories(${PROJECT_NAME} 
    INTERFACE $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
              $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}> )

install(TARGETS ${PROJECT_NAME}
        EXPORT ${PROJECT_NAME}_Targets )


include(CMakePackageConfigHelpers)
write_basic_package_version_file("${PROJECT_NAME}ConfigVersion.cmake"
                                 VERSION ${PROJECT_VERSION}
                                 COMPATIBILITY SameMajorVersion)

configure_package_config_file(
    "${PROJECT_SOURCE_DIR}/${PROJECT_NAME}Config.cmake.in"
    "${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
    INSTALL_DESTINATION
    ${CMAKE_INSTALL_DATAROOTDIR}/${PROJECT_NAME}/cmake
)

install(FILES "${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
              "${PROJECT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
        DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/${PROJECT_NAME}/cmake)

# get_target_property()
install(FILES 
    "${CMAKE_CURRENT_SOURCE_DIR}/rapidxml_iterators.hpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/rapidxml_print.hpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/rapidxml_utils.hpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/rapidxml.hpp"
        DESTINATION include)