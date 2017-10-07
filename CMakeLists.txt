cmake_minimum_required (VERSION 2.8)
project (qpbo)

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