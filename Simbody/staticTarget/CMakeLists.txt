## This whole directory exists just so I could define these extra 
## preprocessor values.

add_definitions(-DSimTK_SIMBODY_BUILDING_STATIC_LIBRARY)

if(BUILD_UNVERSIONED_LIBRARIES)

    add_library(${STATIC_TARGET} STATIC 
                ${SOURCE_FILES} ${SOURCE_INCLUDE_FILES} 
                ${API_ABS_INCLUDE_FILES})
    
    target_link_libraries(${STATIC_TARGET} 
                 ${SimTKMATH_STATIC_LIBRARY}
                 ${SimTKCOMMON_STATIC_LIBRARY}
                 ${MATH_LIBS_TO_USE})
    
    set_target_properties(${STATIC_TARGET} PROPERTIES
        PROJECT_LABEL "Code - ${STATIC_TARGET}")

    target_compile_definitions(${STATIC_TARGET} PUBLIC SimTK_USE_STATIC_LIBRARIES)
    
    # install library
    
    install(TARGETS ${STATIC_TARGET} EXPORT SimbodyTargets
                     PERMISSIONS OWNER_READ OWNER_WRITE 
                     GROUP_READ GROUP_WRITE 
                     WORLD_READ 
                     ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
                     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
                     RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

    target_include_directories(${STATIC_TARGET} INTERFACE
        $<INSTALL_INTERFACE:${SIMBODY_INCLUDE_INSTALL_DIR}>
        )

endif()



if(BUILD_VERSIONED_LIBRARIES)

    add_library(${STATIC_TARGET_VN} STATIC 
                ${SOURCE_FILES} ${SOURCE_INCLUDE_FILES} 
                ${API_ABS_INCLUDE_FILES})
    
    target_link_libraries(${STATIC_TARGET_VN} 
                 ${SimTKMATH_STATIC_LIBRARY_VN}
                 ${SimTKCOMMON_STATIC_LIBRARY_VN}
                 ${MATH_LIBS_TO_USE_VN})
    
    set_target_properties(${STATIC_TARGET_VN} PROPERTIES
        PROJECT_LABEL "Code - ${STATIC_TARGET_VN}")

    target_compile_definitions(${STATIC_TARGET_VN} PUBLIC SimTK_USE_STATIC_LIBRARIES)
    
    # install library
    
    install(TARGETS ${STATIC_TARGET_VN} EXPORT SimbodyTargets
                     PERMISSIONS OWNER_READ OWNER_WRITE 
                     GROUP_READ GROUP_WRITE 
                     WORLD_READ 
                     ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
                     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
                     RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

    target_include_directories(${STATIC_TARGET_VN} INTERFACE
        $<INSTALL_INTERFACE:${SIMBODY_INCLUDE_INSTALL_DIR}>
        )

endif()
