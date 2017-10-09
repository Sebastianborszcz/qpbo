cmake_minimum_required (VERSION 2.8)
project (qpbo)


# default build-type (release)
IF(DEFINED CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE} CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ELSE()
   SET(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ENDIF()


set(QPBO_SRC_FILES
    QPBO_extra.cpp
    QPBO.cpp
    QPBO_maxflow.cpp
    QPBO_postprocessing.cpp
)
   

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR} )



ADD_LIBRARY(qpbo SHARED ${QPBO_SRC_FILES})


install(TARGETS qpbo
    RUNTIME DESTINATION bin         COMPONENT libraries
    LIBRARY DESTINATION lib         COMPONENT libraries
    ARCHIVE DESTINATION lib/static  COMPONENT libraries)

# install (TARGETS qpbo
#         ARCHIVE DESTINATION lib
#         LIBRARY DESTINATION lib
#         RUNTIME DESTINATION bin)


install(FILES QPBO.h DESTINATION include/qpbo)
install(FILES block.h DESTINATION include/qpbo)