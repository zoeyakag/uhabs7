set(LIBNAME Test)



FILE(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
FILE(GLOB INCLUDES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)


##################################################################
# Add Library - Install List
##################################################################
add_library(Test STATIC ${SOURCES} ${INCLUDES})

install(TARGETS Test DESTINATION lib)
#install(FILES ${INCLUDES} DESTINATION include/neutron1/globalstar)

if(${DEPLOY_SOURCE_FILES_TO_REMOTE} MATCHES "yes")
    add_deployment_source_directory(${CMAKE_CURRENT_SOURCE_DIR} "src")
endif()


message("Build ${LIBNAME} from ${CMAKE_CURRENT_SOURCE_DIR}")
