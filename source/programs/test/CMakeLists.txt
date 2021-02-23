file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")
foreach(file ${files})
    get_filename_component(bfile ${file} NAME_WE)
    if(NOT ${bfile} MATCHES "something_you_dont_want")

        add_executable(${bfile} ${file})

        if(UNIX)
            if(${CROSS_TYPE} MATCHES "arm")
                target_link_libraries(${bfile}   ${COSMOS_LIBS} dl rt localzlib) #pthread


                if(${DEPLOY_BIN_FILES_TO_REMOTE} MATCHES "all")
                    #add_deployment_binary(${bfile} "bin")
                endif()

                if(${DEPLOY_SOURCE_FILES_TO_REMOTE} MATCHES "yes")
                    #add_deployment_source(${bfile}.cpp "src")
                endif()

            else()
                target_link_libraries(${bfile}  ${COSMOS_LIBS} localzlib )
            endif()
        else()
            target_link_libraries(${bfile}  ${COSMOS_LIBS})
        endif()
        install(TARGETS ${bfile} DESTINATION bin)

    endif()
endforeach()


add_executable(netspeed "${COSMOS_SOURCE}/core/programs/tests/netspeed.cpp")
target_link_libraries(netspeed CosmosSupport)
install(TARGETS netspeed DESTINATION bin)

add_executable(netspeedd "${COSMOS_SOURCE}/core/programs/tests/netspeedd.cpp")
target_link_libraries(netspeedd CosmosSupport)
install(TARGETS netspeedd DESTINATION bin)

add_executable(filespeed "${COSMOS_SOURCE}/core/programs/tests/filespeed.cpp")
target_link_libraries(filespeed CosmosSupport)
install(TARGETS filespeed DESTINATION bin)

add_executable(mathspeed "${COSMOS_SOURCE}/core/programs/tests/mathspeed.cpp")
target_link_libraries(mathspeed CosmosTime CosmosSupport)
install(TARGETS mathspeed DESTINATION bin)

