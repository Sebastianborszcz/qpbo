cmake_minimum_required (VERSION 2.8)
project (QPBO)


# default build-type (release)
IF(DEFINED CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE} CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ELSE()
   SET(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ENDIF()


set(${PROJECT_NAME}_VERSION_MAJOR 0)
set(${PROJECT_NAME}_VERSION_MINOR 3)
set(${PROJECT_NAME}_VERSION_PATCH 11)


set(${PROJECT_NAME}_VERSION 
    ${${PROJECT_NAME}_VERSION_MAJOR}.${${PROJECT_NAME}_VERSION_MINOR}.${${PROJECT_NAME}_VERSION_PATCH}
)


set(QPBO_SRC_FILES
    QPBO_extra.cpp
    QPBO.cpp
    QPBO_maxflow.cpp
    QPBO_postprocessing.cpp
)

set(QPBO_HEADERS
    QPBO.h
    block.h
)




ADD_LIBRARY(qpbo SHARED ${QPBO_SRC_FILES})


include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

# install(TARGETS qpbo
#     RUNTIME DESTINATION bin         COMPONENT libraries
#     LIBRARY DESTINATION lib         COMPONENT libraries
#     ARCHIVE DESTINATION lib/static  COMPONENT libraries)

# install (TARGETS qpbo
#         ARCHIVE DESTINATION lib
#         LIBRARY DESTINATION lib
#         RUNTIME DESTINATION bin)

install(TARGETS qpbo 
    DESTINATION ${CMAKE_INSTALL_LIBDIR})

install(FILES ${QPBO_HEADERS}
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/qpbo)


set(QPBO_CMAKECONFIG_INSTALL_DIR "${CMAKE_INSTALL_LIBDIR}/cmake/QPBO" CACHE
    STRING "install path for QPBOConfig.cmake")

configure_package_config_file(QPBOConfig.cmake.in
                              "${CMAKE_CURRENT_BINARY_DIR}/QPBOConfig.cmake"
                              INSTALL_DESTINATION ${QPBO_CMAKECONFIG_INSTALL_DIR})


write_basic_package_version_file(${CMAKE_CURRENT_BINARY_DIR}/QPBOConfigVersion.cmake
                                 VERSION ${QPBO_VERSION}
                                 COMPATIBILITY AnyNewerVersion)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/QPBOConfig.cmake
              ${CMAKE_CURRENT_BINARY_DIR}/QPBOConfigVersion.cmake
        DESTINATION ${QPBO_CMAKECONFIG_INSTALL_DIR})
